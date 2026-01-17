# Host Inventar vom 17.01.2026

## Hostname

`load`

### Rolle

K3s Control Plane Node für das Cluster. Zusätzlich DRBD Quorum Node zur Stabilisierung der DRBD Rollen und Cluster Entscheidungen. Baseline Hardening, Logging, Fail2ban und auditd aktiv.

### System

- OS: Debian GNU Linux 13 trixie
- Kernel: 6.12.63+deb13-amd64
- Standort: Netcup VPS KVM Server RS 1000 G12
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
- nftables
  - Startmethode: systemd service
  - Status: active exited
  - Ports: keine
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
- nftables
  - Haupt Config Pfad: /etc/nftables.conf
  - Include Pfade: optional /etc/nftables.d/
  - Aktive Dateien: nftables.conf
- fail2ban
  - Haupt Config Pfad: /etc/fail2ban/jail.local
  - Include Pfade: /etc/fail2ban/jail.d/
  - Aktive Dateien: jail.local
- sysctl hardening
  - Haupt Config Pfad: /etc/sysctl.d/10-hardening.conf
  - Include Pfade: /etc/sysctl.d/
  - Aktive Dateien: 10-hardening.conf und 50-IPv6.conf und 99-nc-kernel.conf
- auditd rules
  - Haupt Config Pfad: /etc/audit/rules.d/audit.rules
  - Include Pfade: /etc/audit/rules.d/
  - Aktive Dateien: audit.rules und baseline.rules

### Daten und Logs

- Persistente Datenpfade
  - /cont
  - /data
  - /backup
  - /var für Systemdaten und Logs
- Log Pfade
  - /var/log/
  - journald über systemd-journald
- Temporäre Daten
  - /tmp
  - /run

### Automatik

- Cronjobs
  - keine eigenen Cronjobs gefunden
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
  - Teil des Cluster Verbunds
  - Erwartet K3s Worker Nodes und DRBD Peer Nodes
- Externe Dienste
  - apt Repositories für Updates
  - Netcup Infrastruktur
- Netzwerke
  - Public IPv4: anonymisiert
  - Public IPv6: anonymisiert
