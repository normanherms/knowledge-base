# Host Inventar vom 17.01.2026

## Hostname

`dash`

### Rolle

Monitoring Node für das Staging Cluster. Prometheus Server plus Node Exporter für Systemmetriken. Baseline Hardening, Logging, Fail2ban und auditd aktiv.

### System

- OS: Debian GNU Linux 13 trixie
- Kernel: 6.12.63+deb13-amd64
- Standort: Netcup VPS KVM Server nano G11s
- Uptime Erwartung: 24/7

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
  - Ports: 9100 TCP nur localhost
- prometheus
  - Startmethode: systemd service
  - Status: running
  - Ports: 9090 TCP nur localhost
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
- fail2ban
  - Haupt Config Pfad: /etc/fail2ban/jail.local
  - Include Pfade: /etc/fail2ban/jail.d/
  - Aktive Dateien: jail.local
- auditd rules
  - Haupt Config Pfad: /etc/audit/rules.d/audit.rules
  - Include Pfade: /etc/audit/rules.d/
  - Aktive Dateien: audit.rules und baseline.rules

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

### Abhängigkeiten

- Andere Hosts
  - zieht Metriken von Cluster Nodes per Prometheus Scrape Targets
- Externe Dienste
  - apt Repositories für Updates
  - Netcup Infrastruktur
- Netzwerke
  - Public IPv4: anonymisiert
  - Public IPv6: anonymisiert
