# Netzwerk- und Adressplanung (v1.5)

## Heimnetz (192.168.1.0/24)

### dock-mirror (Lenovo ThinkCentre M910q, K3s Worker)

eth0: 192.168.1.10
wlp*: 192.168.1.11

### dock-edge (Dell Optiplex 3070, Home/LLM)

eth0: 192.168.1.12
wlp*: 192.168.1.13

### synology214 (DS214+)

eth0: 192.168.1.14
Reserve: 192.168.1.15

---

## WireGuard Mesh (10.99.99.0/24)

### Schema

- A = primäre WG-IP
- B = reservierte WG-IP
- Start bei 10.99.99.1
- nur Cluster Nodes + Backup brauchen Wireguard

## Rechenzentrum

### dock-prod (Root G12, K3s Worker, DRBD Primary)

A: 10.99.99.1
B: 10.99.99.101

### dock-load (Root G12, K3s Control Plane / Quorum)

A: 10.99.99.2
B: 10.99.99.102

### dock-dash (VPS nano, Monitoring)

A: 10.99.99.4
B: 10.99.99.104

---

## Heimnetz

### dock-mirror

A: 10.99.99.3
B: 10.99.99.103

### synology214

A: 10.99.99.5
B: 10.99.99.105

---

## kurze Rollenübersicht

### Rechenzentrum

#### dock-prod

- K3s Worker
- DRBD Primary
- SDB Fencing

#### dock-load

- K3s Control Plane
- Quorum Node
- Loadbalancing für OpenCloud
- SDB Fencing

#### dock-dash

- Monitoring Node (Prometheus / Grafana)

### Heimnetz

#### dock-mirror

- K3s Worker
- DRBD Secondary
- SDB Fencing

#### dock-edge

- Ollama
- Libvirt
- Containerd Runtime (n8n, AdGuard, Anytype, HA)

#### synology214

- Backup

---

## Empfehlung /etc/hosts

```bash
192.168.1.10 dock-mirror
192.168.1.12 dock-edge
192.168.1.14 synology214

10.99.99.1 dock-prod
10.99.99.2 dock-load
10.99.99.3 dock-mirror
10.99.99.4 dock-dash
10.99.99.5 synology214

```
