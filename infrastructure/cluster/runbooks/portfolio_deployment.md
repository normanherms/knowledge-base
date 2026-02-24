# Runbook – Portfolio Deployment via GitLab CI/CD auf K3s

---

## Scope

Automatisiertes Deployment der Astro Portfolio Website auf den K3s Cluster.
Image Build via Kaniko, Registry via GitLab, Deployment via kubectl.
HTTP wird auf HTTPS redirected. TLS via Let's Encrypt.

---

## Architektur

```bash
git push → GitLab CI → Kaniko baut Image → GitLab Registry
→ kubectl apply → K3s Deployment (mirror) → Traefik Ingress → portfolio.dockseed.io
```

---

## Repository Struktur

| Datei | Zweck |
|---|---|
| `Dockerfile` | Multi-Stage Build: Node baut, nginx liefert aus |
| `.gitlab-ci.yml` | Pipeline: build + deploy |
| `k8s/deployment.yaml` | Deployment, Service, Middleware, Ingress (HTTP + HTTPS) |

`k8s/tls.yaml` existiert nicht mehr – certResolver läuft über HelmChartConfig in kube-system.

---

## Voraussetzungen

### GitLab CI Variable

| Variable | Typ | Beschreibung |
|---|---|---|
| `KUBECONFIG_CONTENT` | File | kubeconfig mit externer IP als Server |

Kubeconfig vorbereiten auf load:

```bash
sudo cat /etc/rancher/k3s/k3s.yaml | sed 's/127.0.0.1/<LOAD_PUBLIC_IP>/g'
```

### Image Pull Secret

```bash
sudo kubectl create secret docker-registry gitlab-registry \
  --docker-server=registry.gitlab.com \
  --docker-username=normanherms \
  --docker-password=<GITLAB_TOKEN> \
  --namespace=default
```

Token Scope: `read_registry`

### Firewall auf load

```bash
# K8s API für GitLab Runner
sudo nft add rule inet filter input tcp dport 6443 accept

# HTTPS für Let's Encrypt und Clients
sudo nft add rule inet filter input tcp dport 443 accept
```

Permanent in `/etc/nftables.conf` eintragen.

### K3s Zertifikat (externe IP als SAN)

```bash
sudo nano /etc/rancher/k3s/config.yaml
```

```yaml
tls-san:
  - <LOAD_PUBLIC_IP>
  - 10.99.99.2
  - 127.0.0.1
```

```bash
sudo rm /var/lib/rancher/k3s/server/tls/serving-kube-apiserver.crt
sudo rm /var/lib/rancher/k3s/server/tls/serving-kube-apiserver.key
sudo systemctl restart k3s
```

Verifikation:

```bash
echo | openssl s_client -connect <LOAD_PUBLIC_IP>:6443 2>/dev/null | openssl x509 -noout -text | grep -A1 "Subject Alternative"
```

---

## Kubernetes Manifeste

Pfad: `k8s/deployment.yaml`

Enthält in einer Datei:

- `Deployment` – 1 Replica, revisionHistoryLimit 3, imagePullSecret gitlab-registry
- `Service` – ClusterIP Port 80
- `Middleware` – redirect-https, HTTP → HTTPS permanent (301)
- `Ingress portfolio-http` – Entrypoint web (80), wendet Middleware an
- `Ingress portfolio` – Entrypoint websecure (443), TLS via letsencrypt certResolver

### Traefik HelmChartConfig

Pfad: `/var/lib/rancher/k3s/server/manifests/traefik-config.yaml` auf load

```yaml
apiVersion: helm.cattle.io/v1
kind: HelmChartConfig
metadata:
  name: traefik
  namespace: kube-system
spec:
  valuesContent: |-
    certificatesResolvers:
      letsencrypt:
        acme:
          email: norman.herms@proton.me
          storage: /data/acme.json
          tlsChallenge: true
```

---

## Normaler Workflow

```bash
cd ~/portfolio
# Änderungen machen
git add .
git commit -m "beschreibung"
git push
```

Pipeline läuft automatisch. Build ~1 Minute, Deploy ~30 Sekunden.

Pipeline Status: GitLab → CI/CD → Pipelines

---

## Cluster prüfen

```bash
# Pods inkl. Node
sudo kubectl get pods -o wide

# Ingress
sudo kubectl get ingress -n default

# Node Auslastung
sudo kubectl top nodes

# Logs Portfolio
sudo kubectl logs -l app=portfolio

# Logs Traefik
sudo kubectl logs -n kube-system deployment/traefik | tail -30
```

---

## Redirect prüfen

```bash
curl -v http://portfolio.dockseed.io 2>&1 | grep "< HTTP\|Location"
# Erwartung: 301 + Location: https://portfolio.dockseed.io/
```

---

## Troubleshooting

### ImagePullBackOff

```bash
sudo kubectl describe pod -l app=portfolio | grep -A10 "Events:"
```

Secret prüfen:

```bash
sudo kubectl get secret gitlab-registry -o jsonpath='{.data.\.dockerconfigjson}' | base64 -d
```

Secret neu anlegen:

```bash
sudo kubectl delete secret gitlab-registry
sudo kubectl create secret docker-registry gitlab-registry \
  --docker-server=registry.gitlab.com \
  --docker-username=normanherms \
  --docker-password=<NEUER_TOKEN> \
  --namespace=default
sudo kubectl rollout restart deployment/portfolio
```

### Port 6443 nicht erreichbar

```bash
sudo nft list ruleset | grep 6443
```

### x509 Fehler bei kubectl

Externe IP nicht im K3s Zertifikat → siehe Voraussetzungen → K3s Zertifikat.

### HTTP redirectet nicht auf HTTPS

Middleware oder Ingress portfolio-http prüfen:

```bash
sudo kubectl get middleware -n default
sudo kubectl get ingress -n default
sudo kubectl describe ingress portfolio-http -n default
```

---

## DNS

| Record | Typ | Ziel | TTL |
|---|---|---|---|
| `portfolio.dockseed.io` | A | `<LOAD_PUBLIC_IP>` | 300 |

Provider: INWX – Zone muss im MASTER Mode laufen, sonst keine Propagation.

---

## Credentials

| Was | Wo | Scope |
|---|---|---|
| GitLab Token (Push) | `~/.git-credentials` auf zimtlab | `write_repository` |
| GitLab Token (Registry) | K3s Secret `gitlab-registry` | `read_registry` |
| kubeconfig | GitLab CI Variable `KUBECONFIG_CONTENT` | Cluster Admin |

---

## Node Rollen

| Node | Rolle | Standort |
|---|---|---|
| load | control-plane | Netcup |
| prod | worker | Netcup |
| mirror | worker | Homelab |

Pods landen aktuell auf mirror (meiste freie RAM).

---

## Status

- Pipeline aktiv, deployt auf push
- HTTP → HTTPS Redirect aktiv (301)
- TLS via Let's Encrypt aktiv
- revisionHistoryLimit auf 3 gesetzt
- Node Labels gesetzt (worker)

## Ausbaustufen

### Ausbaustufe 1 – Security Header

Ziel: HSTS, X-Frame-Options, CSP via Traefik Middleware setzen.

### Ausbaustufe 2 – Monitoring

Ziel: Uptime und Response Time des Portfolios in Grafana sichtbar machen.

### Ausbaustufe 3 – Multi-Replica

Ziel: 2 Replicas auf verschiedenen Nodes für Ausfallsicherheit.
Voraussetzung: Pod Affinity Rules damit nicht beide auf mirror landen.
