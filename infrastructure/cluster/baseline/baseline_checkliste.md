# Baseline Bootstrap Process

## Warum dieses Dokument existiert

Nach 7 Cluster-Iterationen und mehrfachen kompletten Neuaufbauten
habe ich gelernt: Ein konsistenter, getesteter Bootstrap-Prozess
ist essentiell. Der Checkliste sind kleine Hilfestellungen hinzugefügt.

**Problem aus früheren Iterationen:**

- Inkonsistente SSH-Konfigurationen zwischen Nodes
- Fehlerhafte Firewall Config führt zum aussperren vom System
- Vergessene Firewall-Rules nach Reboot
- fstab-Fehler führten zu unbootbaren Systemen
- Keine Reproduzierbarkeit (jeder Node anders aufgesetzt)

**Diese Baseline löst:**

- Reproduzierbarer Prozess für alle Nodes
- Definierte Checkpoints (keine vergessenen Schritte)
- Fail-Safe Design (zweite SSH Session, fstab-Test vor Reboot)
- Dokumentierte Reihenfolge (Storage → User → Firewall)

**Ergebnis:**

Von "5 Stunden pro Node mit Fehlern" zu "1 Stunde pro Node, zero Issues".

---

## Definition: Wann ist die Baseline abgeschlossen

Die Baseline gilt als abgeschlossen, wenn:

- SSH nur per Key erreichbar ist
- Root Login deaktiviert ist
- Firewall aktiv ist mit Default Drop
- Logging und Audit aktiv sind
- Ein Reboot erfolgreich durchgeführt wurde
- Zugriff nach Reboot möglich ist
- Verifizierung erfolgreich abgeschlossen

---

## Phase 0: Ausgangszustand

- Frisches OS installiert
- Speicher weitgehend partitioniert (meist kleine Root Partition)
- Konsolenzugriff vorhanden (VPS Konsole, IPMI oder physisch)
- Keine produktiven Dienste aktiv

---

## Phase 1: Systemgrundlage

- Einloggen (root oder initialer User)
- Paketindex aktualisieren
  apt update && apt upgrade
- Reboot durchführen (immer, zur Sicherheit)
- Hostname setzen
  hostnamectl set-hostname <hostname>
- Zeitzone setzen
  timedatectl set-timezone Europe/Berlin
- NTP aktivieren
  timedatectl set-ntp true
- Basistools installieren
  `sudo apt install parted sudo curl wget rsyslog auditd nftables fail2ban restic htop btop nano`

---

## Phase 2: Storage Basis

- Partitionen anlegen oder anpassen
- fstab Einträge schreiben für:
  - Root
  - Zusätzliche Datenpartitionen
  - Optional Swap
- Mounts testen ohne Reboot
  mount -a
- Fehler korrigieren falls vorhanden
- Reboot durchführen
- Nach Reboot Mounts erneut prüfen

Hinweis:
Fehler in dieser Phase können das System unbootbar machen.

---

## Phase 3: Netzwerk Validierung

- Interfaces prüfen
  ip a
- Routing prüfen
  ip route
- IP Konnektivität prüfen
  ping 1.1.1.1
- DNS prüfen
  ping google.com
- Zeitstatus prüfen
  timedatectl status

---

## Phase 4: User und SSH Zugriff

- Admin User anlegen
  useradd -m -s /bin/bash <user>
- User zur sudo Gruppe hinzufügen
  usermod -aG sudo <user>

### SSH Vorbereitung

- SSH Keys lokal (Client) erzeugen
- Verzeichnis anlegen
  mkdir -p /home/<user>/.ssh
- Public Key in authorized_keys eintragen
- Ownership setzen
  chown -R <user>:<user> /home/<user>/.ssh
- Permissions setzen
  chmod 700 /home/<user>/.ssh
  chmod 600 /home/<user>/.ssh/authorized_keys

### SSH Hardening

Datei: /etc/ssh/sshd_config.d/10-hardening.conf
*Achtung bei der Dateibenennung, je höher die Zahl umso später wird die Config geladen.*

Inhalt:

```bash
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
AuthenticationMethods publickey

KbdInteractiveAuthentication no
UsePAM yes

X11Forwarding no
AllowAgentForwarding no
AllowTcpForwarding no

AuthorizedKeysFile .ssh/authorized_keys
AllowUsers <User>

LogLevel VERBOSE
Banner none

ClientAliveInterval 300
ClientAliveCountMax 2
```

- Permissions setzen
  chmod 600 /etc/ssh/sshd_config.d/10-hardening.conf
  chown root:root /etc/ssh/sshd_config.d/10-hardening.conf

- Syntax prüfen
  sshd -t

- Zweite SSH Session offen lassen
- SSH Konfiguration neu laden
  systemctl reload sshd
- Neuer Login Test durchführen
- Erst danach alte Session schließen

---

## Phase 5: Firewall Basis (nftables)

Datei: /etc/nftables.conf

Minimal Baseline Regelwerk:

```bash
#!/usr/sbin/nft -f

flush ruleset

table inet filter {

    chain input {
        type filter hook input priority 0;
        policy drop;

        # loopback
        iif lo accept

        # established / related
        ct state established,related accept

        # ICMPv4
        ip protocol icmp accept

        # ICMPv6 (Pflicht für IPv6!)
        ip6 nexthdr icmpv6 accept

        # SSH
        tcp dport 22 accept
    }

    chain forward {
        type filter hook forward priority 0;
        policy drop;
    }

    chain output {
        type filter hook output priority 0;
        policy accept;
    }
}
```

- Permissions setzen
  chmod 600 /etc/nftables.conf
  chown root:root /etc/nftables.conf

- Konfiguration testen
  nft -c -f /etc/nftables.conf

- Zweite SSH Session offen lassen
- Regelwerk laden
  nft -f /etc/nftables.conf

- SSH Verbindung testen
- Ping testen

- nftables dauerhaft aktivieren
  systemctl enable nftables
  systemctl start nftables

---

## Phase 6: Fail2Ban Basis

Datei: /etc/fail2ban/jail.local

Inhalt:

```bash
[DEFAULT]
bantime  = 72h
findtime = 10m
maxretry = 3
backend  = systemd

[sshd]
enabled = true
```

Hinweis:
Fail2Ban erst aktivieren, wenn SSH final stabil getestet wurde.

- Fail2Ban aktivieren
  systemctl enable fail2ban

---

## Phase 7: Logging und Audit

Minimale Audit Regeln
Datei: /etc/audit/rules.d/baseline.rules

Inhalt:

```bash
-w /etc/ssh/sshd_config -p wa -k sshd_config
-w /etc/ssh/sshd_config.d -p wa -k sshd_config

-w /etc/nftables.conf -p wa -k nftables

-w /etc/passwd -p wa -k passwd_changes
-w /etc/shadow -p wa -k shadow_changes
```

- Regeln laden
  augenrules --load
- auditd Status prüfen

---

## Phase 8: sysctl Basis Hardening

Datei: /etc/sysctl.d/10-hardening.conf

Inhalt:

```bash
net.ipv4.tcp_syncookies = 1

net.ipv4.conf.all.accept_redirects = 0
net.ipv6.conf.all.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0

net.ipv4.conf.all.accept_source_route = 0
net.ipv6.conf.all.accept_source_route = 0

net.ipv4.ip_forward = 0
net.ipv6.conf.all.forwarding = 0
```

Hinweis:
Diese Einstellungen müssen vor WireGuard oder Routing überprüft werden.

- Konfiguration laden
  sysctl -p /etc/sysctl.d/10-hardening.conf

---

## Phase 9: Finalisierung

- Vollständigen Reboot durchführen
- Nach Reboot prüfen:
  - SSH erreichbar
  - nftables aktiv
  - fail2ban aktiv
  - auditd aktiv
- Backup machen!

---

## Abschluss

- Betriebsinventar für diesen Host erstellen
- Baseline Abschlussdatum dokumentieren
- Node freigeben für Rollen Setup

---

## Warum dieser Prozess so aufgebaut ist

### Phasen-Reihenfolge ist nicht zufällig

**Storage VOR User/SSH:**

- fstab-Fehler würden System unbootbar machen
- Besser früh erkennen als nach SSH-Hardening

**Firewall NACH SSH-Hardening:**

- SSH muss stabil sein bevor Firewall aktiv wird
- Sonst Lockout-Risiko

**Fail2Ban NACH Firewall:**

- Fail2Ban braucht funktionierende Firewall
- Erst wenn SSH + nftables stabil

### Lessons Learned aus gescheiterten Iterationen

**Iteration 3:** fstab-Fehler → System unbootbar → VPS neu aufsetzen (2h)
**Iteration 5:** Firewall vor SSH getestet → Lockout → Rescue-Modus (1h)
**Iteration 6:** Fail2Ban ohne Firewall → Blocked eigene IP → Lockout

**Diese Baseline verhindert diese Fehler.**

---

## Verwendung

Dieser Prozess wurde verwendet für:

- prod (Netcup Root G12)
- load (Netcup Root G12)
- mirror (Lenovo M910q)
- dash (Netcup VPS nano)

Alle Nodes verwenden identische Baseline → konsistentes Cluster.

---

## Validation Abschnitt ist ein Draft aus KI Vorschlägen und wird später von mir verifiziert.

## Zweck

Einfache CLI-Befehle zur Validierung jeder Baseline-Phase.
Kein komplexes Tooling, nur Standard-Linux-Commands.

---

## Quick Master Check

### Minimaler Status-Check (alle Phasen)

```bash
echo "=== BASELINE STATUS ==="
echo ""
echo "[ System ]"
timedatectl | grep -q "NTP.*yes" && echo "  ✓ NTP active" || echo "  ✗ NTP inactive"
dpkg -l | grep -q "^ii.*sudo" && echo "  ✓ Tools installed" || echo "  ✗ Missing tools"
echo ""
echo "[ SSH ]"
systemctl is-active --quiet sshd && echo "  ✓ SSH running" || echo "  ✗ SSH down"
grep -qr "PermitRootLogin no" /etc/ssh/sshd_config.d/ && echo "  ✓ Root disabled" || echo "  ✗ Root enabled"
grep -qr "PasswordAuthentication no" /etc/ssh/sshd_config.d/ && echo "  ✓ Password auth off" || echo "  ✗ Password auth on"
echo ""
echo "[ Firewall ]"
systemctl is-active --quiet nftables && echo "  ✓ nftables active" || echo "  ✗ nftables inactive"
nft list ruleset | grep -q "policy drop" && echo "  ✓ Default DROP" || echo "  ✗ No DROP policy"
echo ""
echo "[ Security ]"
systemctl is-active --quiet fail2ban && echo "  ✓ fail2ban active" || echo "  ✗ fail2ban inactive"
systemctl is-active --quiet auditd && echo "  ✓ auditd active" || echo "  ✗ auditd inactive"
echo ""
```

---

## Phase 1: Systemgrundlage

### Hostname Check

```bash
hostnamectl | grep "Static hostname"
```

### NTP Check

```bash
timedatectl | grep "NTP"
timedatectl status
```

### Installierte Pakete

```bash
dpkg -l | grep -E "sudo|curl|wget|rsyslog|auditd|nftables|fail2ban|restic|htop"
```

### Quick Validation

```bash
echo "=== Phase 1 Check ==="
hostnamectl status | grep -q "$(hostname)" && echo "✓ Hostname set" || echo "✗ Hostname missing"
timedatectl | grep -q "NTP.*yes" && echo "✓ NTP active" || echo "✗ NTP inactive"
dpkg -l | grep -q "^ii.*sudo" && echo "✓ sudo installed" || echo "✗ sudo missing"
dpkg -l | grep -q "^ii.*nftables" && echo "✓ nftables installed" || echo "✗ nftables missing"
```

---

## Phase 2: Storage

### Mount Points

```bash
mount | grep -v "tmpfs\|devtmpfs\|proc\|sys"
```

### fstab Einträge

```bash
cat /etc/fstab | grep -v "^#"
```

### fstab Syntax-Check

```bash
mount -a 2>&1 && echo "✓ fstab valid" || echo "✗ fstab has errors"
```

### Disk Usage

```bash
df -h
lsblk
```

---

## Phase 3: Netzwerk

### Interfaces

```bash
ip a
```

### Routing

```bash
ip route
```

### Connectivity Check

```bash
ping -c 1 1.1.1.1 >/dev/null 2>&1 && echo "✓ Internet connectivity OK" || echo "✗ No internet"
```

### DNS Check

```bash
ping -c 1 google.com >/dev/null 2>&1 && echo "✓ DNS resolution OK" || echo "✗ DNS broken"
```

### NTP Status

```bash
timedatectl status | grep "NTP"
```

### Full Network Validation

```bash
echo "=== Phase 3 Check ==="
ip a | grep -q "inet " && echo "✓ IP configured" || echo "✗ No IP"
ip route | grep -q "default" && echo "✓ Default route exists" || echo "✗ No default route"
ping -c 1 1.1.1.1 >/dev/null 2>&1 && echo "✓ Internet OK" || echo "✗ No connectivity"
ping -c 1 google.com >/dev/null 2>&1 && echo "✓ DNS OK" || echo "✗ DNS broken"
```

---

## Phase 4: SSH

### User Validation

```bash
# User exists
id <username> >/dev/null 2>&1 && echo "✓ User exists" || echo "✗ User missing"

# Sudo group membership
groups <username> | grep -q sudo && echo "✓ User in sudo group" || echo "✗ Not in sudo group"
```

### SSH Configuration

```bash
# Root login disabled
grep -r "PermitRootLogin no" /etc/ssh/sshd_config.d/ && echo "✓ Root login disabled" || echo "✗ Root login enabled"

# Password authentication disabled
grep -r "PasswordAuthentication no" /etc/ssh/sshd_config.d/ && echo "✓ Password auth disabled" || echo "✗ Password auth enabled"

# Key authentication enabled
grep -r "PubkeyAuthentication yes" /etc/ssh/sshd_config.d/ && echo "✓ Pubkey auth enabled" || echo "✗ Pubkey auth disabled"

# AllowUsers configured
grep -r "AllowUsers" /etc/ssh/sshd_config.d/ && echo "✓ AllowUsers set" || echo "⚠ AllowUsers not set"
```

### SSH Keys

```bash
# Authorized keys exist
test -f /home/<username>/.ssh/authorized_keys && echo "✓ SSH keys configured" || echo "✗ No authorized_keys"

# Permissions check
stat -c "%a %U:%G" /home/<username>/.ssh
stat -c "%a %U:%G" /home/<username>/.ssh/authorized_keys
```

### SSH Service

```bash
systemctl is-active sshd && echo "✓ SSH service active" || echo "✗ SSH service inactive"
systemctl status sshd
```

---

## Phase 5: Firewall

### nftables Status

```bash
systemctl is-active nftables && echo "✓ nftables active" || echo "✗ nftables inactive"
systemctl status nftables
```

### Current Ruleset

```bash
nft list ruleset
```

### Policy Check

```bash
nft list ruleset | grep "policy drop" && echo "✓ Default DROP policy active" || echo "✗ No DROP policy"
```

### SSH Rule Check

```bash
nft list ruleset | grep "tcp dport 22" && echo "✓ SSH rule exists" || echo "✗ SSH rule missing"
```

### Permissions Check

```bash
stat -c "%a %U:%G" /etc/nftables.conf
```

---

## Phase 6: Fail2Ban

### Service Status

```bash
systemctl is-active fail2ban && echo "✓ fail2ban active" || echo "✗ fail2ban inactive"
systemctl status fail2ban
```

### Jail Status

```bash
fail2ban-client status
```

### SSH Jail Check

```bash
fail2ban-client status sshd 2>/dev/null && echo "✓ SSH jail active" || echo "✗ SSH jail not configured"
```

### Banned IPs

```bash
fail2ban-client status sshd | grep "Banned"
```

### Configuration Check

```bash
cat /etc/fail2ban/jail.local | grep -A 5 "\[sshd\]"
```

---

## Phase 7: Logging und Audit

### rsyslog Status

```bash
systemctl is-active rsyslog && echo "✓ rsyslog active" || echo "✗ rsyslog inactive"
systemctl status rsyslog
```

### auditd Status

```bash
systemctl is-active auditd && echo "✓ auditd active" || echo "✗ auditd inactive"
systemctl status auditd
```

### Loaded Audit Rules

```bash
auditctl -l
```

### Rule Count

```bash
echo "Loaded audit rules: $(auditctl -l | wc -l)"
```

### Recent Auth Logs

```bash
tail -20 /var/log/auth.log
```

### Audit Logs

```bash
ausearch -m USER_LOGIN -ts recent
```

---

## Phase 8: sysctl Hardening

### Check Individual Settings

```bash
sysctl net.ipv4.tcp_syncookies
sysctl net.ipv4.conf.all.accept_redirects
sysctl net.ipv4.conf.all.send_redirects
sysctl net.ipv4.conf.all.accept_source_route
sysctl net.ipv4.conf.all.log_martians
sysctl net.ipv4.ip_forward
```

### Load and Verify All Settings

```bash
sysctl -p /etc/sysctl.d/10-hardening.conf
```

### Quick Validation

```bash
echo "=== Phase 8 Check ==="
sysctl net.ipv4.tcp_syncookies | grep -q "= 1" && echo "✓ SYN cookies enabled" || echo "✗ SYN cookies disabled"
sysctl net.ipv4.conf.all.accept_redirects | grep -q "= 0" && echo "✓ ICMP redirects disabled" || echo "✗ ICMP redirects enabled"
sysctl net.ipv4.ip_forward | grep -q "= 0" && echo "✓ IP forwarding disabled" || echo "✗ IP forwarding enabled"
```

---

## Phase 9: Final Validation

### System Uptime

```bash
uptime
```

### All Critical Services

```bash
systemctl is-active sshd nftables fail2ban rsyslog auditd
```

### Service Status Summary

```bash
echo "=== Critical Services ==="
for service in sshd nftables fail2ban rsyslog auditd; do
  systemctl is-active --quiet $service && echo "✓ $service" || echo "✗ $service"
done
```

### Disk Space

```bash
df -h /
df -h
```

### Last Reboot

```bash
who -b
last reboot | head -5
```

### Backup Check

```bash
# Example - adjust path
ls -lh /path/to/backups/ 2>/dev/null || echo "⚠ Backup path not configured"
```

---

## Complete Baseline Validation Script

### Save as: `/usr/local/bin/baseline-status`

```bash
#!/bin/bash
# Baseline Status Check
# Quick validation of all baseline phases

set -e

echo "========================================"
echo "    BASELINE STATUS CHECK"
echo "========================================"
echo ""

# Phase 1: System
echo "[ Phase 1: System Basics ]"
hostnamectl status | grep -q "$(hostname)" && echo "  ✓ Hostname configured" || echo "  ✗ Hostname not set"
timedatectl | grep -q "NTP.*yes" && echo "  ✓ NTP active" || echo "  ✗ NTP inactive"
dpkg -l | grep -q "^ii.*sudo" && echo "  ✓ Required packages installed" || echo "  ✗ Missing packages"
echo ""

# Phase 2: Storage
echo "[ Phase 2: Storage ]"
mount -a 2>&1 >/dev/null && echo "  ✓ fstab valid" || echo "  ✗ fstab errors"
echo ""

# Phase 3: Network
echo "[ Phase 3: Network ]"
ping -c 1 1.1.1.1 >/dev/null 2>&1 && echo "  ✓ Internet connectivity" || echo "  ✗ No internet"
ping -c 1 google.com >/dev/null 2>&1 && echo "  ✓ DNS resolution" || echo "  ✗ DNS broken"
echo ""

# Phase 4: SSH
echo "[ Phase 4: SSH Security ]"
systemctl is-active --quiet sshd && echo "  ✓ SSH service running" || echo "  ✗ SSH service down"
grep -qr "PermitRootLogin no" /etc/ssh/sshd_config.d/ && echo "  ✓ Root login disabled" || echo "  ✗ Root login enabled"
grep -qr "PasswordAuthentication no" /etc/ssh/sshd_config.d/ && echo "  ✓ Password auth disabled" || echo "  ✗ Password auth enabled"
echo ""

# Phase 5: Firewall
echo "[ Phase 5: Firewall ]"
systemctl is-active --quiet nftables && echo "  ✓ nftables active" || echo "  ✗ nftables inactive"
nft list ruleset | grep -q "policy drop" && echo "  ✓ Default DROP policy" || echo "  ✗ No DROP policy"
nft list ruleset | grep -q "tcp dport 22" && echo "  ✓ SSH rule configured" || echo "  ✗ SSH rule missing"
echo ""

# Phase 6: Fail2Ban
echo "[ Phase 6: Fail2Ban ]"
systemctl is-active --quiet fail2ban && echo "  ✓ fail2ban active" || echo "  ✗ fail2ban inactive"
fail2ban-client status sshd >/dev/null 2>&1 && echo "  ✓ SSH jail configured" || echo "  ✗ SSH jail missing"
echo ""

# Phase 7: Logging
echo "[ Phase 7: Logging & Audit ]"
systemctl is-active --quiet rsyslog && echo "  ✓ rsyslog active" || echo "  ✗ rsyslog inactive"
systemctl is-active --quiet auditd && echo "  ✓ auditd active" || echo "  ✗ auditd inactive"
RULES=$(auditctl -l | wc -l)
[ $RULES -gt 0 ] && echo "  ✓ Audit rules loaded ($RULES)" || echo "  ✗ No audit rules"
echo ""

# Phase 8: sysctl
echo "[ Phase 8: Kernel Hardening ]"
sysctl net.ipv4.tcp_syncookies | grep -q "= 1" && echo "  ✓ SYN cookies enabled" || echo "  ✗ SYN cookies disabled"
sysctl net.ipv4.ip_forward | grep -q "= 0" && echo "  ✓ IP forwarding disabled" || echo "  ⚠ IP forwarding enabled"
echo ""

# Overall Status
echo "========================================"
FAILED=0
for service in sshd nftables fail2ban rsyslog auditd; do
  systemctl is-active --quiet $service || ((FAILED++))
done

if [ $FAILED -eq 0 ]; then
  echo "STATUS: ✓ BASELINE COMPLETE"
else
  echo "STATUS: ✗ INCOMPLETE ($FAILED services down)"
fi
echo "========================================"
echo ""
echo "Uptime: $(uptime -p)"
echo "Last reboot: $(who -b | awk '{print $3, $4}')"
echo ""
```

### Installation

```bash
# Download/create the script
sudo nano /usr/local/bin/baseline-status

# Make executable
sudo chmod +x /usr/local/bin/baseline-status

# Run
baseline-status
```

---

## Quick Reference

### Check einzelne Phase

```bash
# Phase 1
timedatectl status

# Phase 4
systemctl status sshd

# Phase 5
nft list ruleset

# Phase 6
fail2ban-client status

# Phase 7
auditctl -l
```

### Check alle kritischen Services

```bash
systemctl is-active sshd nftables fail2ban rsyslog auditd
```

### Nach Reboot prüfen

```bash
baseline-status
```

---

## Exit Codes für Automation

```bash
# Check ob baseline complete (für Scripts)
if baseline-status | grep -q "BASELINE COMPLETE"; then
  echo "Ready for next phase"
  exit 0
else
  echo "Baseline incomplete"
  exit 1
fi
```

---
