# Runbook SSH Hardening mit Hardware Token

## Scope

SSH Zugriff für Headless Server
Key only Authentifizierung mit FIDO2 Hardware Token
Kein Root Login
Keine Passwörter
Kein Banner

---

## Client Voraussetzungen

* OpenSSH Version ≥ 8.2
* FIDO2 Hardware Token
* Resident ED25519 SK Key vorhanden
* Private Key Datei lokal vorhanden

Pfad:

```bash
~/.ssh/id_ed25519_sk_rk
```

---

## Client Konfiguration

Datei:

```bash
~/.ssh/config
```

Inhalt:

```bash
Host <HostName>
    User <User>
    IdentityFile ~/.ssh/id_ed25519_sk_rk
    IdentitiesOnly yes
    PubkeyAuthentication yes
    PreferredAuthentications publickey
    AddKeysToAgent no

Host <HostName>
    HostName <IP>

Host <HostName>
    HostName <IP>

Host <HostName>
    HostName <IP>

Host <HostName>
    HostName <IP>
```

---

## Server Key Ablage

Pfad:

```bash
/home/<User>/.ssh/authorized_keys
```

Inhalt:

```bash
sk-ssh-ed25519@openssh.com AAAA... comment
```

Rechte:

```bash
chmod 700 /home/<User>/.ssh
chmod 600 /home/<User>/.ssh/authorized_keys
chown -R <User>:<User> /home/<User>/.ssh
```

---

## SSH Server Hardening

Datei:

```bash
/etc/ssh/sshd_config.d/10-hardening.conf
```

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

---

## Aktivierung

Syntax prüfen:

```bash
sshd -t
```

Konfiguration laden:

```bash
systemctl reload sshd
```

---

## Verifikation

Effektive Konfiguration prüfen:

```bash
sshd -T | grep -E 'permitrootlogin|passwordauthentication|x11forwarding|allowagentforwarding|allowtcpforwarding|banner|authenticationmethods'
```

Login Test:

```bash
ssh <HostName>
```

Erwartung:

* Kein Text vor Authentifizierung
* Token Touch
* PIN Abfrage
* Login erfolgreich

---

## Sicherheitshinweise

* `.ssh` Verzeichnis muss ausführbar sein
* `authorized_keys` darf nur dem Login User gehören
* Zu offene Rechte führen zu stiller Ablehnung
* Banner betrifft nur Pre Auth
* MOTD ist davon unabhängig

---

## Status

SSH Zugriff gehärtet
Hardware Token only

---
