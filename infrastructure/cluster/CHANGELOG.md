# Cluster Changelog

Das Changelog dient zur Übersicht der Arbeit am Cluster.

---

*Template:*

## YYYY-MM-DD - Titel

**Was:** Beschreibung der Änderung
**Wo:** Welcher Server
**Warum:** Grund/Motivation
**Auswirkung:** Technische Konsequenzen
**Fix:** Fixes und Issue Behebung
**Referenz:** Link oder Pfad zur Doku oder ähnlichem

---

### 2026-01-19 - Dokumentaion

**Was:** Erweiterung und Ergänzung der Inventorys der Cluster Nodes
**Referenz:** Zu finden hier: [Inventory](/infrastructure/cluster/inventory/)

### 2026-01-18 3/3 – Baseline: Swapfile für Monitoring Node ergänzt

**Was:** Ergänzung eines Swapfiles auf dem Monitoring Node zur Absicherung gegen Speicherengpässe bei Prometheus und Grafana.
**Wo:** dash
**Warum:** Der Monitoring Node verfügt über nur 2 GB RAM. Ohne Swap besteht bei Lastspitzen der Ausfall des Monitorings.
**Auswirkung:** Ein 1 GB Swapfile dient als Notpuffer. Das System degradiert kontrolliert unter Last statt Prozesse hart zu beenden. Monitoring bleibt stabil auch bei temporären Speicherpeaks.
**Fix:** Fehlender Swap als Baseline Lücke identifiziert und behoben. Swappiness reduziert um Swap nur als Notbremse zu nutzen.

### 2026-01-18 2/3 – Baseline: Monitoring Stack intern abgesichert

**Was:** Aufbau des vollständigen Monitoring Stacks mit Node Exporter auf allen Nodes sowie zentralem Prometheus und lokal gebundenem Grafana. Grafana über gehärteten Nginx Reverse Proxy mit TLS angebunden und Benutzerverwaltung bereinigt.
**Wo:** mirror, load, prod, dash
**Warum:** Verlässliche Sichtbarkeit des Systemzustands vor K3s bei minimaler externer Angriffsfläche.
**Auswirkung:** Alle Nodes liefern Metriken ausschließlich über das WireGuard Netz. Prometheus und Grafana sind nicht direkt öffentlich erreichbar. Monitoring ist rebootfest und reproduzierbar dokumentiert.
**Fix:** Fehlende nftables Freigabe für Node Exporter über wg0 ergänzt. Grafana Default Admin erkannt und durch dedizierte Benutzer ersetzt. Reverse Proxy, TLS und Fail2ban Absicherung ergänzt.

### 2026-01-18 1/3 - Baseline: WireGuard Full Mesh Netzwerk

**Was:** Aufbau eines vollständigen WireGuard Mesh zwischen allen Cluster Nodes inklusive NAT Node. Einführung von systemd Autostart, restriktiver nftables Freigaben und dokumentiertem Runbook.
**Wo:** mirror, load, prod, dash
**Warum:** Sichere, konsistente und vom Public Internet entkoppelte Cluster Kommunikation als Grundlage für DRBD, K3s und weitere Dienste.
**Auswirkung:** Interne Cluster Kommunikation läuft ausschließlich über das WireGuard Netz. Öffentliche Abhängigkeiten sind minimiert. Netzwerk ist rebootfest, nachvollziehbar und reproduzierbar.
**Fix:** NAT Fallstrick beim mirror Node identifiziert und durch Anpassung der nftables Regeln (state new für WireGuard UDP) behoben.

### 2026-01-17 - Baseline: Security Layer aktiv

**Was:** nftables, Fail2ban und auditd Baseline Rules aktiviert und geprüft. Host Inventare für alle Nodes erstellt.
**Wo:** mirror, load, prod, dash
**Warum:** Einheitlicher Security Standard vor DRBD und K3s Deployment.
**Auswirkung:** Nur SSH ist extern erreichbar, Fail2ban blockt SSH Bots via nftables, kritische Config Dateien werden auditiert, Baseline ist dokumentiert und vergleichbar.

### 2026-01-16 - Dokumentation

**Was:** Dokumentation reviewed und erweitert
**Warum:** Dokumentation meiner Aufbauphase
**Auswirkung:** Bessere Nachvollziehbarkeit was gemacht oder geändert wurde

### 2026-01-14 2/2 - Baseline: Storage Layout

**Was:** Einheitliches Storage-Layout eingerichtet und persistent eingebunden.
**Wo:** mirror, load, prod
**Warum:** Reproduzierbare Basis für Cluster, DRBD und sauberes Recovery.
**Auswirkung:** Logisches Standardlayout gewählt (256 GB)

- /root 64 GB
- swap 8 GB
- /cont 8 GB
- /data 128 GB
- /backup ~48 GB

Abweichungen:

- load: /root 128 GB, /data 64 GB (Control Plane, kein DRBD)
- mirror: physisch 1 TB, logisch erstmal auf 256 GB begrenzt

### 2026-01-14 1/2 - Baseline: User & SSH

**Was:** Einheitlicher Admin User angelegt, SSH gehärtet und System aktualisiert.
**Wo:** mirror, load, prod
**Warum:** Grundlage für einen konsistenten und sicheren Cluster Betrieb.
**Auswirkung:** Zentraler, abgesicherter SSH Zugriff auf allen Nodes.

### 2026-01-06 – Baseline & Monitoring Basis sowie Daily Backups

**Was:** Aufbau einer minimalen Monitoring Basis mit Node Exporter und Prometheus sowie Einführung eines Daily Backups
**Wo:** dash
**Warum:** Frühzeitige Beobachtbarkeit und Absicherung der Konfigurationen
**Auswirkung:** Neue Systemdienste aktiv, zusätzliche Ports nur lokal gebunden, tägliche Backup Jobs per Cron
