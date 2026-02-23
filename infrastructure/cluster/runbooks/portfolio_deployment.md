# Runbook – Portfolio Deployment via GitLab CI/CD auf K3s

## Scope

Automatisiertes Deployment einer Astro Portfolio Website über GitLab CI/CD auf den bestehenden K3s Cluster.
Image Build via Kaniko, Registry über GitLab Container Registry, Deployment über kubectl.

---

## Ausgangslage

- K3s Cluster läuft auf `load` (Control Plane), `prod`, `mirror` (Worker)
- Traefik als Ingress Controller bereits installiert (K3s Default)
- GitLab Repository `normanherms/portfolio` vorhanden
- Domain `portfolio.dockseed.io` zeigt auf `<LOAD_PUBLIC_IP>` (load)

---

## Architektur

```
git push → GitLab CI → Kaniko baut Image → GitLab Registry
→ kubectl apply → K3s Deployment → Traefik Ingress → portfolio.dockseed.io
```

Komponenten:

- Astro (Static Site Generator, Output: nginx Image)
- GitLab Container Registry (`registry.gitlab.com/normanherms/portfolio`)
- Kaniko (Imagebuild ohne Docker Daemon, läuft im GitLab Runner)
- K3s Deployment mit 1 Replica
- Traefik Ingress mit Let's Encrypt TLS

---

## Dateien im Repository

| Datei | Zweck |
|---|---|
| `Dockerfile` | Multi-Stage Build (Node → nginx:alpine) |
| `.gitlab-ci.yml` | Pipeline Definition (build + deploy) |
| `k8s/deployment.yaml` | K8s Deployment, Service, Ingress |
| `k8s/tls.yaml` | Traefik HelmChartConfig für Let's Encrypt |

---

## Dockerfile

Pfad: `Dockerfile`

```dockerfile
FROM node:24-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
```

Multi-Stage: Node nur zum Bauen, finales Image ist minimales nginx (~20 MB).

---

## Pipeline (.gitlab-ci.yml)

Pfad: `.gitlab-ci.yml`

```yaml
stages:
  - build
  - deploy

variables:
  IMAGE: registry.gitlab.com/normanherms/portfolio
  TAG: $CI_COMMIT_SHA

build:
  stage: build
  image:
    name: gcr.io/kaniko-project/executor:v1.23.2-debug
    entrypoint: [""]
  script:
    - mkdir -p /kaniko/.docker
    - echo "{\"auths\":{\"registry.gitlab.com\":{\"auth\":\"$(echo -n $CI_REGISTRY_USER:$CI_REGISTRY_PASSWORD | base64)\"}}}" > /kaniko/.docker/config.json
    - /kaniko/executor
      --context $CI_PROJECT_DIR
      --dockerfile $CI_PROJECT_DIR/Dockerfile
      --destination $IMAGE:$TAG
      --destination $IMAGE:latest
  only:
    - main

deploy:
  stage: deploy
  image:
    name: bitnami/kubectl:latest
    entrypoint: [""]
  before_script:
    - mkdir -p ~/.kube
    - cp $KUBECONFIG_CONTENT ~/.kube/config
  script:
    - kubectl apply -f k8s/
    - kubectl set image deployment/portfolio portfolio=$IMAGE:$TAG --namespace=default
  only:
    - main
```

---

## Kubernetes Manifeste

Pfad: `k8s/deployment.yaml`

Enthält drei Ressourcen in einer Datei:

- `Deployment` – 1 Replica, portfolio Container, imagePullSecret für GitLab Registry
- `Service` – ClusterIP auf Port 80
- `Ingress` – Traefik, Host `portfolio.dockseed.io`, TLS via Let's Encrypt

Pfad: `k8s/tls.yaml`

HelmChartConfig für Traefik – aktiviert den `letsencrypt` certResolver mit TLS-Challenge.

---

## Voraussetzungen

### GitLab CI/CD Variablen

Unter: `Repository → Settings → CI/CD → Variables`

| Variable | Typ | Beschreibung |
|---|---|---|
| `KUBECONFIG_CONTENT` | File | kubeconfig des K3s Clusters (server auf externe IP gesetzt) |

Kubeconfig vorbereiten auf `load`:

```bash
sudo cat /etc/rancher/k3s/k3s.yaml | sed 's/127.0.0.1/<LOAD_PUBLIC_IP>/g'
```

Output als Variable hinterlegen. Protected anhaken, Masked nicht möglich (Whitespace).

### Image Pull Secret im Cluster

Damit K3s das Image aus der privaten GitLab Registry ziehen kann:

```bash
sudo kubectl create secret docker-registry gitlab-registry \
  --docker-server=registry.gitlab.com \
  --docker-username=normanherms \
  --docker-password=GITLAB_TOKEN \
  --namespace=default
```

Benötigter Token Scope: `read_registry`

### Firewall auf load

Port 6443 (K8s API) muss für GitLab Runner erreichbar sein:

```bash
sudo nft add rule inet filter input tcp dport 6443 accept
```

Permanent in `/etc/nftables.conf` eintragen.

Port 443 für Let's Encrypt:

```bash
sudo nft add rule inet filter input tcp dport 443 accept
```

### K3s Zertifikat (externe IP als SAN)

Damit kubectl von außen ohne TLS-Fehler funktioniert:

```bash
# Config setzen
sudo nano /etc/rancher/k3s/config.yaml
```

Inhalt:

```yaml
tls-san:
  - <LOAD_PUBLIC_IP>
  - 10.99.99.2
  - 127.0.0.1
```

```bash
# Altes Zertifikat löschen und K3s neu starten
sudo rm /var/lib/rancher/k3s/server/tls/serving-kube-apiserver.crt
sudo rm /var/lib/rancher/k3s/server/tls/serving-kube-apiserver.key
sudo systemctl restart k3s
```

Verifikation:

```bash
echo | openssl s_client -connect <LOAD_PUBLIC_IP>:6443 2>/dev/null | openssl x509 -noout -text | grep -A1 "Subject Alternative"
```

Erwartung: `IP Address:<LOAD_PUBLIC_IP>` ist im Output enthalten.

---

## Deployment Workflow

### Normaler Push (täglich)

```bash
# Änderung machen
cd ~/portfolio
# ... editieren ...
git add .
git commit -m "update content"
git push
```

GitLab startet automatisch die Pipeline. Build ~1 Minute, Deploy ~30 Sekunden.

### Pipeline Status prüfen

GitLab → Repository → CI/CD → Pipelines

### Cluster Status prüfen

```bash
# Auf load
sudo kubectl get pods
sudo kubectl get pods -w   # watch mode
```

---

## Troubleshooting

### ImagePullBackOff

```bash
sudo kubectl describe pod -l app=portfolio | grep -A 10 "Events:"
```

Häufige Ursache: Pull Secret fehlt oder Token abgelaufen.

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
  --docker-password=NEUER_TOKEN \
  --namespace=default
sudo kubectl rollout restart deployment/portfolio
```

### Deploy Job schlägt fehl: dial tcp timeout

Port 6443 nicht erreichbar. Firewall prüfen:

```bash
sudo nft list ruleset | grep 6443
```

Temporär öffnen:

```bash
sudo nft add rule inet filter input tcp dport 6443 accept
```

### Deploy Job schlägt fehl: x509 certificate

Externe IP nicht im K3s Zertifikat. Zertifikat neu ausstellen (siehe Voraussetzungen → K3s Zertifikat).

### Traefik: nonexistent certificate resolver

`k8s/tls.yaml` wurde nicht deployed. Prüfen:

```bash
sudo kubectl get helmchartconfig -n kube-system
```

Falls leer: sicherstellen dass `.gitlab-ci.yml` `kubectl apply -f k8s/` (nicht `k8s/deployment.yaml`) verwendet.

### Seite nicht erreichbar (DNS)

DNS Propagation abwarten. Extern prüfen:

```bash
dig portfolio.dockseed.io @8.8.8.8
```

Lokal testen ohne DNS:

```bash
curl -H "Host: portfolio.dockseed.io" http://<LOAD_PUBLIC_IP>
```

---

## Cluster Ressourcen

```bash
# Pods
sudo kubectl get pods -n default

# Ingress
sudo kubectl get ingress -n default

# Services
sudo kubectl get services -n default

# Logs
sudo kubectl logs -l app=portfolio

# Traefik Logs
sudo kubectl logs -n kube-system deployment/traefik | tail -30
```

---

## Credentials und Secrets

Alle Werte ohne echte Credentials dokumentiert.

| Was | Wo | Scope |
|---|---|---|
| GitLab Token (Push) | `~/.git-credentials` auf zimtlab | `write_repository` |
| GitLab Token (Registry) | K3s Secret `gitlab-registry` | `read_registry` |
| kubeconfig | GitLab CI Variable `KUBECONFIG_CONTENT` | Cluster Admin |

Hinweis: Nach Token-Ablauf oder Rotation müssen `gitlab-registry` Secret im Cluster und ggf. `~/.git-credentials` auf zimtlab aktualisiert werden.

---

## DNS

| Record | Typ | Ziel | TTL |
|---|---|---|---|
| `portfolio.dockseed.io` | A | `<LOAD_PUBLIC_IP>` | 300 |

Provider: INWX

---

## Status

Pipeline aktiv
Image Build via Kaniko funktioniert
Deployment auf K3s funktioniert
TLS via Let's Encrypt ausstehend (DNS Propagation)
