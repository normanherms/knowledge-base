# Runbook – Grafana öffentlich anbinden und absichern (Nginx + TLS + Fail2ban)

## Ziel

Grafana sicher über eine eigene Domain öffentlich erreichbar machen.
TLS Termination über Nginx, interne Dienste bleiben auf localhost.
Absicherung mit Fail2ban.

---

## Ausgangslage

- Grafana läuft lokal auf `127.0.0.1:3000`
- DNS Eintrag `grafana.domain.io → Server IP` existiert
- Firewall restriktiv (Ports standardmäßig geschlossen)

---

## 1. Nginx installieren

```bash
sudo apt update
sudo apt install nginx
```

Status prüfen:

```bash
sudo systemctl status nginx --no-pager
```

---

## 2. Default Nginx Site deaktivieren

```bash
sudo rm /etc/nginx/sites-enabled/default
sudo nginx -t
```

---

## 3. Grafana Reverse Proxy vHost anlegen

Datei erstellen:

```bash
sudo nano /etc/nginx/sites-available/grafana.domain.io
```

Inhalt:

```nginx
server {
    server_name grafana.domain.io;

    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    listen 80;
}
```

Aktivieren:

```bash
sudo ln -s /etc/nginx/sites-available/grafana.domain.io /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

---

## 4. Funktionstest (HTTP)

```bash
curl http://grafana.domain.io
```

Erwartung:

- Redirect auf `/login`
- Kein Zertifikat notwendig

DNS Tests:

```bash
getent hosts grafana.domain.io
dig grafana.domain.io @1.1.1.1
```

---

## 5. TLS mit Let’s Encrypt einrichten

### Certbot installieren

```bash
sudo apt install certbot python3-certbot-nginx
```

### Firewall temporär Port 80 öffnen

(In nftables)

```nft
tcp dport 80 accept
```

Reload:

```bash
sudo nft -f /etc/nftables.conf
```

### Zertifikat holen

```bash
sudo certbot --nginx -d grafana.domain.io
```

Ergebnis:

- HTTPS Server Block wird automatisch erzeugt
- HTTP → HTTPS Redirect aktiv

---

## 6. Firewall wieder schließen

Port 80 Regel entfernen und nftables neu laden:

```bash
sudo nft -f /etc/nftables.conf
sudo systemctl restart nftables
```

---

## 7. Grafana korrekt hinter Reverse Proxy konfigurieren

Datei öffnen:

```bash
sudo nano /etc/grafana/grafana.ini
```

Abschnitt `[server]`:

```ini
[server]
http_addr = 127.0.0.1
http_port = 3000
domain = grafana.domain.io
root_url = https://grafana.domain.io
serve_from_sub_path = false
```

Neustart:

```bash
sudo systemctl restart grafana-server
```

---

## 8. Nginx Security Header ergänzen

Datei:

```bash
sudo nano /etc/nginx/sites-enabled/grafana.domain.io
```

Im **HTTPS server Block** ergänzen:

```nginx
add_header X-Frame-Options "SAMEORIGIN" always;
add_header X-Content-Type-Options "nosniff" always;
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
add_header Content-Security-Policy "frame-ancestors 'self'" always;
add_header Strict-Transport-Security "max-age=31536000" always;
```

Reload:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

Test:

```bash
curl -I https://grafana.domain.io
```

---

## 9. Fail2ban Absicherung

### Basis Konfiguration

`/etc/fail2ban/jail.local`

```ini
[DEFAULT]
bantime  = 72h
findtime = 10m
maxretry = 3
backend  = systemd

[sshd]
enabled = true
```

### Nginx Jails ergänzen

```ini
[nginx-http-auth]
enabled  = true
port     = http,https
filter   = nginx-http-auth
logpath  = /var/log/nginx/error.log
maxretry = 3

[nginx-bad-request]
enabled  = true
port     = http,https
filter   = nginx-bad-request
logpath  = /var/log/nginx/access.log
maxretry = 5
```

Aktivieren:

```bash
sudo systemctl restart fail2ban
sudo fail2ban-client status
```

---

## Status

Grafana öffentlich über HTTPS erreichbar
Interne Dienste bleiben isoliert
Reverse Proxy gehärtet
Automatische Zertifikatserneuerung
Brute Force und Scanner Schutz aktiv
