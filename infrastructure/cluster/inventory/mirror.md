# Host Inventar vom 17.01.2026

## Hostname

`mirror`

### Rolle

DRBD Node für blockbasiertes Storage Sync und K3s Worker Node für Cluster Workloads. Baseline Hardening, Logging, Fail2ban und auditd aktiv.

### System

- OS: Debian GNU Linux 13 trixie
- Kernel: 6.12.63+deb13-amd64
- Standort: Lenovo ThinkCentre M910q im Heimnetz
- Uptime Erwartung: 24/7 oder nach Bedarf

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
- rsyslog
  - Startmethode: systemd service
  - Status: running
  - Ports: keine
- ssh
  - Startmethode: systemd service
  - Status: running
  - Ports: 22 TCP IPv4 und IPv6
- systemd networkd
  - Startmethode: systemd service
  - Status: running
  - Ports: DHCP Client Ports UDP 68 und IPv6 DHCP UDP 546
- wpa supplicant
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
  - Aktive Dateien: 10-hardening.conf
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
  - keine eigenen gefunden
- systemd Timer
  - apt-daily.timer
  - apt-daily-upgrade.timer
  - logrotate.timer
  - dpkg-db-backup.timer
  - e2scrub_all.timer
  - fstrim.timer
  - man-db.timer
  - systemd-tmpfiles-clean.timer
- Externe Trigger
  - keine

### Abhängigkeiten

- Andere Hosts
  - Teil des Cluster Verbunds
- Externe Dienste
  - apt Repositories für Updates
  - Heimnetz Gateway
- Netzwerke
  - LAN IPv4: anonymisiert
  - WLAN IPv4: anonymisiert
  - IPv6: aktiv im Heimnetz
