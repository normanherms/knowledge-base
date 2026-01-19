# Host Inventar (sanitized) vom 19.01.2026

Diese Dokumentation ist für öffentliche Nutzung bereinigt. Sie enthält keine sensiblen oder identifizierenden Daten.

## 2.1 Hosts Übersicht

| Hostname | Rolle | OS | IP | Kritikalität |
|----------|-------|----|----|--------------|
| edge-node | Homelab Host | Debian 13 | DHCP (Bridge) | HIGH |
| home-automation (VM) | Home Automation | HAOS | Private LAN IP | HIGH |

---

## 2.2 Sicherheit und Betrieb (Homelab Baseline)

### Netzwerk

- Betrieb ausschließlich im internen Heimnetz
- Keine öffentliche Erreichbarkeit von Diensten
- Gateway und NAT über Router
- DNS zentral über lokalen DNS Resolver
- Bridge Netzwerk für Host, Container und VMs

### Zugriff

- SSH nur im Heimnetz
- Authentifizierung via SSH Key
- Root Login deaktiviert
- Privilegien über sudo

### Hardening

- Standard Debian Hardening
- Keine erweiterten Maßnahmen wie fail2ban oder auditd
- Fokus auf Stabilität und Wartbarkeit

### Logging

- systemd journald aktiv
- rsyslog aktiv
- Logs lokal ausgewertet (journalctl, Web UI)

### Monitoring

- Kein zentrales Monitoring
- Systemüberwachung manuell

### Backups

- Regelmäßige Backups via restic
- Lokales Backup Ziel
- Backup Logs vorhanden

### Abgrenzung

- Nicht Teil eines externen Clusters
- Keine Zero Trust oder Cluster Sicherheitsrichtlinien

---

## 2.3 Host edge-node

### Hostname

`edge`

### Rolle

Primärer Homelab Host. Führt containerisierte Dienste, Medienserver und Management Tools aus.

### System

- OS: Debian 13
- Kernel: 6.x
- Hardware: Mini PC (SFF)
  - CPU: Intel Core i5 Klasse (6C 6T)
  - RAM: 32 GB
  - Storage
    - NVMe: 1 TB
    - SATA SSD: 240 GB
- Standort: Heimnetzwerk
- Uptime Erwartung: 24/7, Reboots nur für Updates

### Zugriff

- SSH User: admin
- Auth Methode: SSH Key
- Root Zugriff: via sudo
- SSH Port: 22
- Management Web UI: aktiv (nur intern)

---

## 2.4 Laufende Dienste auf edge-node

### Container (nerdctl und containerd)

| Name | Image | Ports | User | Autostart |
|------|-------|-------|------|-----------|
| adguardhome | adguard/adguardhome | intern | root | restart: unless-stopped |
| traefik | traefik | intern | root | restart: unless-stopped |
| wikijs | requarks/wiki | intern | node | restart: unless-stopped |
| wikijs-db | postgres | intern | postgres | restart: unless-stopped |
| tandoor-web | vabene1111/recipes | intern | app user | restart: unless-stopped |
| tandoor-db | postgres | intern | postgres | restart: unless-stopped |
| any-sync-* | anyproto/* | intern | anytype | restart: unless-stopped |
| mongo | mongo | intern | mongodb | restart: unless-stopped |
| redis | redis-stack-server | intern | redis | restart: unless-stopped |
| minio | minio | intern | minio | restart: unless-stopped |

### Bare Metal (systemd)

| Service | Type | Status | Autostart |
|---------|------|--------|-----------|
| jellyfin | Media Server | active | enabled |
| audiobookshelf | Media Server | active | enabled |
| ollama | AI Runtime | active | enabled |
| containerd | Container Runtime | active | enabled |
| libvirtd | VM Host | active | enabled |
| systemd-networkd | Network | active | enabled |
| management-ui | Admin UI | active | enabled |

### VMs (libvirt)

| VM Name | OS | vCPU | RAM | Status | Autostart |
|---------|----|------|-----|--------|-----------|
| home-automation | Home Assistant OS | 2 | 4 GB | running | yes |

---

## 2.5 Konfigurationen (edge-node)

### Container Compose Files

```bash
/cont/*/compose.yml
````

### Netzwerk

```bash
/etc/systemd/network/*.netdev
/etc/systemd/network/*.network
```

### Container Runtime

```bash
/etc/containerd/config.toml
/etc/cni/net.d/*.conflist
```

### Service Configs

```bash
/etc/*/
/data/*/
/cont/*/
```

---

## 2.6 Daten und Logs (edge-node)

### Persistente Daten

```bash
/data/*/        → App Daten
/cont/*/        → Compose Files und Configs
/images/*/      → VM Images
/backup/*/      → Backups (restic)
```

### Logs

```bash
/var/log/*
journalctl -u <service>
nerdctl logs <container>
```

---

## 2.7 Automatik (edge-node)

### Cronjobs

```bash
# System Backup (täglich)
<daily> /home/admin/helper/restic-snap.sh > /var/log/backup.log 2>&1
```

### Autostart Mechanik Container

- Container Runtime startet beim Boot
- Container mit restart policy starten automatisch

---

## 2.8 Abhängigkeiten (edge-node)

### Netzwerk

- Router: DHCP, Gateway, WAN
- Lokaler DNS Resolver: DNS für alle Container plus Host

### Storage

- NVMe muss gesund sein (alle Services)
- SATA SSD muss gesund sein (Backups)

### Externe Dienste

- Keine (alles lokal)

---

## 2.9 VM home-automation (Home Assistant)

### VM Name

`home-automation`

### Zweck

Home Automation. Steuerung von Smart Home Geräten.

### Host

Läuft auf edge-node via libvirt KVM

### Ressourcen

- vCPU: 2
- RAM: 4 GB
- Disk: 32 GB
- Network: Bridge

### Zugriff

- Web UI: intern erreichbar
- SSH: optional (falls aktiviert)
- Console: virsh console

### Autostart

```bash
virsh autostart home-automation
```

### Storage

```bash
/images/home-automation.qcow2
```

---

## 2.10 Service Matrix (Quick Reference)

```bash
| Service          | Type       | Access | Status      | Autostart |
| ---------------- | ---------- | ------ | ----------- | --------- |
| DNS Filter       | Container  | intern | Production  | Yes       |
| Reverse Proxy    | Container  | intern | Partial     | Yes       |
| Wiki             | Container  | intern | Production  | Yes       |
| Recipes          | Container  | intern | Production  | Yes       |
| Sync Platform    | Container  | intern | Production  | Yes       |
| Media Server     | Bare Metal | intern | Production  | Yes       |
| Audiobook Server | Bare Metal | intern | Production  | Yes       |
| AI Runtime       | Bare Metal | intern | Development | Yes       |
| Management UI    | Bare Metal | intern | Production  | Yes       |
| Home Assistant   | VM         | intern | Production  | Yes       |
| n8n              | -          | -      | Planned     | -         |
```
