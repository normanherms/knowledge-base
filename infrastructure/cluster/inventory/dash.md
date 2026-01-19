# Host Inventar vom 19.01.2026

Diese Dokumentation ist bereinigt und enthält keine sensiblen oder identifizierenden Daten.

## Hostname

`dash`

### Rolle

Monitoring Node für das Staging Cluster. Prometheus Server plus Node Exporter für Systemmetriken. Baseline Hardening, Logging, Fail2ban und auditd aktiv.

### System

- OS: Debian GNU Linux 13 trixie
- Kernel: 6.12.63+deb13-amd64
- Standort: Netcup VPS KVM Server nano G11s
- Uptime Erwartung: 24/7

### Ressourcen

- RAM: 2 GB
- Swap: 1 GB Swapfile (`/swapfile`)
- Swappiness: 10
- Zweck: Stabilitätspuffer für Monitoring Dienste bei Lastspitzen

### Zugriff

- SSH User: admin
- Auth Methode: SSH Key Login mit FIDO2 ED25519 SK
- Root Zugriff: Nein PermitRootLogin no
- Passwort Login: Nein PasswordAuthentication no
- Allowed Users: admin
- Forwarding: Agent no TCP no X11 no
- Session Keepalive: ClientAliveInterval 300 ClientAliveCountMax 2
- Logging: LogLevel VERBOSE

### Laufende Dienste

- auditd
  - Startmethode: systemd service
  - Status: running
  - Ports: keine
- cron
  - Startmethode: systemd service
  - Status: running
  - Ports: keine
- fail2ban
  - Startmethode: systemd service
  - Status: running
  - Ports: keine
- node_exporter
  - Startmethode: systemd service
  - Status: running
  - Ports: 9100 TCP gebunden an WireGuard IP
- prometheus
  - Startmethode: systemd service
  - Status: running
  - Ports: 9090 TCP nur localhost
- grafana-server
  - Startmethode: systemd service
  - Status: running
  - Ports: 3000 TCP auf localhost
- nginx
  - Startmethode: systemd service
  - Status: running
  - Ports: 443 TCP öffentlich
- nftables
  - Startmethode: systemd service
  - Status: active (exited)
  - Ports: gesteuert über Ruleset
- rsyslog
  - Startmethode: systemd service
  - Status: running
  - Ports: keine
- ssh
  - Startmethode: systemd service
  - Status: running
  - Ports: 22 TCP IPv4 und IPv6
- qemu guest agent
  - Startmethode: systemd service
  - Status: running
  - Ports: keine
- systemd timesyncd
  - Startmethode: systemd service
  - Status: running
  - Ports: keine
- wireguard (wg-quick)
  - Startmethode: systemd oneshot service
  - Unit: wg-quick@wg0
  - Status: enabled, active (exited)
  - Ports: 51820 UDP (eingehend, restriktiv)

### Konfigurationen

- sshd
  - Haupt Config Pfad: /etc/ssh/sshd_config
  - Include Pfade: /etc/ssh/sshd_config.d/
  - Aktive Dateien: 10-hardening.conf
- sysctl hardening
  - Haupt Config Pfad: /etc/sysctl.d/10-hardening.conf
  - Include Pfade: /etc/sysctl.d/
  - Aktive Dateien: 10-hardening.conf und 50-IPv6.conf und 99-nc-kernel.conf
- prometheus
  - Haupt Config Pfad: /etc/prometheus/prometheus.yml
  - Include Pfade: /etc/prometheus/
  - Aktive Dateien: prometheus.yml
- node_exporter
  - Haupt Config Pfad: systemd unit
  - Include Pfade: /etc/systemd/system/
  - Aktive Dateien: node_exporter.service
- grafana-server
  - Haupt Config Pfad: /etc/grafana/grafana.ini
  - Include Pfade: /etc/grafana/
  - Aktive Dateien: grafana.ini
- rsyslog
  - Haupt Config Pfad: /etc/rsyslog.conf
  - Include Pfade: /etc/rsyslog.d/
  - Aktive Dateien: 10-dash.conf
- nginx
  - Haupt Config Pfad: /etc/nginx/nginx.conf
  - Include Pfade: /etc/nginx/conf.d/ und /etc/nginx/sites-enabled/
  - Aktive Dateien: sites-enabled/grafana.domain.io
- nftables
  - Haupt Config Pfad: /etc/nftables.conf
  - Include Pfade: optional /etc/nftables.d/
  - Aktive Dateien: nftables.conf
- fail2ban
  - Haupt Config Pfad: /etc/fail2ban/jail.local
  - Include Pfade: /etc/fail2ban/jail.d/
  - Aktive Dateien: jail.local
- auditd rules
  - Haupt Config Pfad: /etc/audit/rules.d/audit.rules
  - Include Pfade: /etc/audit/rules.d/
  - Aktive Dateien: audit.rules und baseline.rules
- wireguard
  - Haupt Config Pfad: /etc/wireguard/wg0.conf
  - Key Pfad: /etc/wireguard/keys/
  - Autostart Unit: /usr/lib/systemd/system/wg-quick@.service
- TLS
  - Tools: certbot
  - Integration: nginx plugin
  - Zertifikat für: grafana.domain.io
  - Zertifikatspfad: /etc/letsencrypt/
- restic
  - Baseline Repo: /data/restic-baseline
  - Daily Repo: /data/restic-daily
  - Passwortdateien: /root/.restic-*-pass
  - Backup Script: /usr/local/sbin/restic-daily-monitoring.sh

### Daten und Logs

- Persistente Datenpfade
  - /var für Systemdaten und Logs
  - /data für Monitoring Daten oder zukünftige Persistenz
- Log Pfade
  - /var/log/
  - journald über systemd-journald
- Temporäre Daten
  - /tmp
  - /run

### Automatik

- Cronjobs
  - 02:30 täglich: /usr/local/sbin/restic-daily-monitoring.sh schreibt nach /var/log/restic-daily.log
- systemd Timer
  - apt-daily.timer
  - apt-daily-upgrade.timer
  - logrotate.timer
  - dpkg-db-backup.timer
  - e2scrub_all.timer
  - fstrim.timer
  - systemd-tmpfiles-clean.timer
- Externe Trigger
  - keine
- Zertifikatserneuerung
  - Mechanismus: certbot systemd timer
  - Status: aktiv

### Abhängigkeiten

- Andere Hosts
  - zieht Metriken von Cluster Nodes per Prometheus Scrape Targets
- Externe Dienste
  - apt Repositories für Updates
  - Netcup Infrastruktur
- Netzwerke
  - Public IPv4: anonymisiert
  - Public IPv6: anonymisiert
  - Cluster Netz: 10.99.99.0/24 (WireGuard)

### Netzwerk

#### Cluster Netzwerk

- Technologie: WireGuard
- Interface: wg0
- Cluster Netz: 10.99.99.0/24
- Autostart: wg-quick@wg0 enabled

#### Host-spezifisch

- Interne IP: 10.99.99.4
- NAT Rolle: nein
- Öffentlicher Endpoint: ja
