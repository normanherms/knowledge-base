# Runbook – K3s Cluster Update

---

## Scope

Rolling Update des K3s Clusters ohne Downtime des Portfolios.
Control-Plane zuerst, dann Worker ohne aktive Pods, dann Worker mit aktiven Pods.

---

## Architektur

| Node | Rolle | Standort |
|---|---|---|
| load | control-plane | Netcup |
| prod | worker | Netcup |
| mirror | worker | Homelab |

WireGuard Mesh: `10.99.99.0/24`
Pod CIDR: `10.42.0.0/16`
Service CIDR: `10.43.0.0/16`

---

## Voraussetzungen

### Aktuelle Version prüfen

```bash
# Auf load
sudo kubectl get nodes
# Aktuelle stable Version
curl -s https://api.github.com/repos/k3s-io/k3s/releases/latest | grep tag_name
```

### Startparameter dokumentieren

**Kritisch:** Die k3s Install-Skripte überschreiben die Service-Datei. Parameter müssen beim Update mitgegeben werden, sonst gehen `--flannel-iface wg0` und `--node-ip` verloren – dann bricht das gesamte Pod-Netzwerk.

Aktuelle Parameter aus History sichern:

```bash
history | grep "get.k3s.io"
```

---

## Update Reihenfolge

```
1. load  (control-plane)
2. prod  (worker, keine aktiven Pods)
3. mirror  (worker, portfolio Pod läuft hier)
```

---

## Schritt 1 – load (control-plane)

```bash
ssh admin@load

curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION="vX.XX.X+k3s1" sh -s - server \
  --node-name load \
  --node-ip <WG_IP_CP> \
  --advertise-address <WG_IP_CP> \
  --tls-san <WG_IP_CP> \
  --tls-san <PUBLIC_IP_CP> \
  --disable-cloud-controller \
  --flannel-backend vxlan \
  --flannel-iface wg0 \
  --cluster-cidr 10.42.0.0/16 \
  --service-cidr 10.43.0.0/16 \
  --kube-proxy-arg "proxy-mode=nftables"
```

Warten bis k3s wieder Ready:

```bash
sudo kubectl get nodes
sudo kubectl get pods -A
```

Flannel Interface prüfen – muss `dev wg0` zeigen, nicht `dev eth0`:

```bash
ip -d link show flannel.1 | grep "local\|dev"
# Erwartung: local <WG_IP_CP> dev wg0
```

**Wenn `dev eth0` erscheint:** k3s wurde ohne `--flannel-iface wg0` gestartet. Sofort mit den korrekten Parametern neu installieren. Pod-Netzwerk zwischen den Nodes funktioniert sonst nicht.

---

## Schritt 2 – prod (worker)

```bash
ssh admin@prod

# Optional: System-Updates
sudo apt update && sudo apt upgrade -y

curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION="vX.XX.X+k3s1" sh -s - agent \
  --server https://<WG_IP_CP>:6443 \
  --token <TOKEN> \
  --node-name prod \
  --node-ip <WG_IP_W1> \
  --flannel-iface wg0 \
  --kube-proxy-arg "proxy-mode=nftables"
```

Token auslesen auf load:

```bash
sudo cat /var/lib/rancher/k3s/server/node-token
```

Reboot nach Kernel-Update:

```bash
sudo reboot
```

Auf load prüfen:

```bash
sudo kubectl get nodes
```

---

## Schritt 3 – mirror (worker, aktive Pods)

Portfolio wegschedulen:

```bash
# Auf load
sudo kubectl cordon mirror
sudo kubectl drain mirror --ignore-daemonsets --delete-emptydir-data

# Portfolio läuft jetzt auf prod
sudo kubectl get pods -o wide
```

Update auf mirror:

```bash
ssh admin@mirror

sudo apt update && sudo apt upgrade -y

curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION="vX.XX.X+k3s1" sh -s - agent \
  --server https://<WG_IP_CP>:6443 \
  --token <TOKEN> \
  --node-name mirror \
  --node-ip <WG_IP_W2> \
  --flannel-iface wg0 \
  --kube-proxy-arg "proxy-mode=nftables"

sudo reboot
```

Nach Reboot mirror wieder freigeben:

```bash
# Auf load
sudo kubectl uncordon mirror
sudo kubectl get nodes
sudo kubectl get pods -o wide
```

---

## Verifikation

```bash
# Alle Nodes auf neue Version
sudo kubectl get nodes

# Portfolio erreichbar
curl -sk https://<DOMAIN> | grep "<title>"

# Pod-Netzwerk funktioniert
ping -c 3 10.42.3.0   # prod Subnetz
ping -c 3 10.42.2.0   # mirror Subnetz

# DNS aus Pods funktioniert
sudo kubectl run dnstest --image=busybox --rm -it --restart=Never -- nslookup google.com
```

---

## Bekannte Fallstricke

### flannel läuft auf eth0 statt wg0

**Symptom:** Pod-zu-Pod Kommunikation zwischen Nodes schlägt fehl. DNS-Timeouts aus Pods. `kube-proxy` Tabelle fehlt in `nft list tables`.

**Ursache:** k3s Install ohne `--flannel-iface wg0` Parameter gestartet.

**Fix:**
```bash
ip -d link show flannel.1 | grep "local\|dev"
# Wenn dev eth0 → sofort neu installieren mit korrekten Parametern
```

### nftables flush ruleset killt k3s Netzwerk

**Symptom:** Nach `systemctl restart nftables` fehlt `table ip kube-proxy` in `nft list tables`. Pods können DNS-Service 10.43.0.10 nicht erreichen.

**Ursache:** `flush ruleset` in `/etc/nftables.conf` löscht alle k3s/kube-proxy Regeln.

**Fix:**
```bash
sudo systemctl restart k3s
sleep 30
sudo nft list tables | grep kube-proxy
```

**Dauerhafter Fix:** nftables nie neu starten ohne gleichzeitigen k3s Restart. Reihenfolge beim Reboot ist korrekt (systemd übernimmt das).

### Let's Encrypt Cert fehlt nach Traefik-Neustart

**Symptom:** Gateway Timeout oder TLS Fehler `unrecognized name`.

**Ursache:** acme.json im Pod-Filesystem wird bei Pod-Neustart geleert wenn kein PersistentVolume konfiguriert ist.

**Prüfen:**
```bash
sudo kubectl exec -n kube-system deployment/traefik -- cat /data/acme.json | python3 -c "
import sys, json
data = json.load(sys.stdin)
certs = data.get('letsencrypt', {}).get('Certificates', [])
print(f'Certs: {len(certs) if certs else 0}')
"
```

**Fix:** Traefik HelmChartConfig auf HTTP-01 Challenge umstellen, Redirect-Middleware temporär deaktivieren, Cert neu ausstellen lassen:

```bash
# Middleware temporär deaktivieren
sudo kubectl annotate ingress portfolio-http \
  traefik.ingress.kubernetes.io/router.middlewares- --overwrite

# Traefik neu starten
sudo kubectl rollout restart deployment/traefik -n kube-system

# Warten bis Cert da ist, dann Middleware wieder aktivieren
sudo kubectl annotate ingress portfolio-http \
  traefik.ingress.kubernetes.io/router.middlewares="default-redirect-https@kubernetescrd" \
  --overwrite
```

### k3s Agent startet ohne Verbindung

**Symptom:** `k3s-agent.service failed` nach neuem Install.

**Ursache:** env-Datei leer – Token und Server-URL fehlen wenn Install-Skript ohne Parameter aufgerufen wird.

**Fix:** Agent immer mit vollständigen Parametern installieren (siehe Schritt 2/3).

---

## Traefik HelmChartConfig

Pfad auf load: `/var/lib/rancher/k3s/server/manifests/traefik-config.yaml`

```yaml
apiVersion: helm.cattle.io/v1
kind: HelmChartConfig
metadata:
  name: traefik
  namespace: kube-system
spec:
  valuesContent: |-
    additionalArguments:
      - "--certificatesresolvers.letsencrypt.acme.email=<ACME_EMAIL>"
      - "--certificatesresolvers.letsencrypt.acme.storage=/data/acme.json"
      - "--certificatesresolvers.letsencrypt.acme.httpchallenge=true"
      - "--certificatesresolvers.letsencrypt.acme.httpchallenge.entrypoint=web"
```

---

## nftables auf load

Persistente Config: `/etc/nftables.conf`

Kritische Regeln die nach jedem k3s-Update geprüft werden müssen:

```
# In chain input:
tcp dport 443 accept      # HTTPS Portfolio
tcp dport 6443 accept     # K3s API für GitLab CI

# In chain forward:
iifname "wg0" accept      # WireGuard + Flannel VXLAN
oifname "wg0" accept
```

Nach Änderungen: `sudo nft -c -f /etc/nftables.conf && echo "OK"`

nftables **nicht** neu starten ohne danach k3s neu zu starten.
