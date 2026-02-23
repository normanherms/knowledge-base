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

## 2026-02-23 – Portfolio CI/CD Pipeline deployed

**Was:** Astro Portfolio Website mit GitLab CI/CD Pipeline, Kaniko Image Build, Deployment auf K3s, Traefik Ingress vorbereitet für `portfolio.dockseed.io`
**Wo:** load, GitLab SaaS, zimtlab
**Warum:** Erstes produktives Deployment auf K3s, Portfolio für Jobsuche
**Auswirkung:** Push auf `main` triggert automatisch Build und Deployment. Port 6443 und 443 in nftables geöffnet.
**Fix:** K3s TLS-Zertifikat um externe IP als SAN erweitert. GitLab Registry Pull Secret angelegt. Pipeline auf `kubectl apply -f k8s/` umgestellt damit tls.yaml mitdeployt wird.
**Referenz:** `infrastructure/cluster/runbooks/portfolio_deployment.md`

---

## 2026-01-24 3/3 - Erster K8s Service deployed

**Was:** nginx Test-Deployment mit Ingress, Load Balancing und Node-Selector
**Wo:** K3s Cluster (namespace: test)
**Warum:** Proof-of-Concept für K3s Deployments, Traefik Ingress, Cross-Node Scheduling
**Auswirkung:** 2 nginx Replicas auf mirror, öffentlich erreichbar via Traefik auf Port 80
**Referenz:** `kubectl get pods -n test -o wide`, Ingress Hostbasiert: nginx.test.local

---

## 2026-01-24 2/3 – Cluster Security Audit Baseline

**Was:** Durchführung eines einheitlichen Security Audits inkl. Portscan, Service Analyse und Konfigurationsprüfung
**Wo:** load, dash, prod
**Warum:** Objektive Bewertung des aktuellen Sicherheitszustands
**Auswirkung:** Transparenz über exponierte Dienste, aktive Ports, Firewall Regeln und SSH Härtung pro Node
**Fix:** Keine direkten Fixes, reine Bestandsaufnahme als Entscheidungsgrundlage für priorisierte Härtung
**Referenz:** /var/log/security-risk-* sowie /etc/nftables.conf und /etc/ssh/sshd_config.d/10-hardening.conf

---

## 2026-01-24 1/3 - Reboot-Tests und Finalisierung

**Was:** Cluster Reboot-Tests, finale Config-Validierung, DNS sauber
**Wo:** load, prod, mirror
**Warum:** Sicherstellen dass Firewall + Cluster nach Reboot funktionieren
**Auswirkung:** Cluster überlebt Reboots, nftables lädt korrekt, DNS stabil
**Referenz:** `kubectl exec test-dns -- nslookup google.com`

---

## 2026-01-23 - CNI Interface Rules gefunden

**Was:** CNI Bridge Interfaces (cni0, flannel.1) explizit in nftables erlaubt
**Wo:** load, prod, mirror
**Warum:** Pod-to-Host Traffic läuft über CNI Interfaces, nicht nur über IPs
**Auswirkung:** DNS funktioniert endlich, alle Pods Running, Cluster stabil
**Fix:** `iifname "cni0" accept` + `iifname "flannel.1" accept` in Input Chain
**Referenz:** /etc/nftables.conf - finale Working Config

---

## 2026-01-22 - nftables Debugging, port-spezifische Rules

**Was:** nftables Input Rules iterativ angepasst - erst port-spezifisch (`tcp dport 10250 ip saddr 10.42.0.0/16`), dann CIDR-weit
**Wo:** load, prod, mirror
**Warum:** Pods brauchen Host-Zugriff für kubelet, DNS, API - port-spezifische Rules funktionierten nicht
**Auswirkung:** 20+ nftables Reloads, 8 Reboots, Cluster instabil
**Fix:** Port-Filter entfernt → `ip saddr 10.42.0.0/16 accept` (ALLE Ports von Pod CIDR)
**Referenz:** K3s Docs "ufw allow from 10.42.0.0/16 to any" = nicht port-spezifisch!

---

## 2026-01-21 - Worker Nodes joinen, Pods crashen

**Was:** prod und mirror als Worker Nodes gejoint, alle Pods in CrashLoopBackOff
**Wo:** prod (WG 10.99.99.1), mirror (WG 10.99.99.3)
**Warum:** CoreDNS, metrics-server, traefik starten nicht - DNS funktioniert nicht
**Auswirkung:** Cluster komplett non-functional, 5x K3s Reinstalls, Flannel Backend-Wechsel versucht (wireguard-native)
**Fix:** Temporär `nft flush ruleset` → Pods laufen → Firewall ist das Problem
**Referenz:** `kubectl get pods -A` - alle Pods CrashLoopBackOff mit aktivierter Firewall

---

## 2026-01-20 - K3s Cluster Setup gestartet

**Was:** K3s Installation auf dock-load mit WireGuard-Bindung, Flannel VXLAN Backend, nftables kube-proxy mode
**Wo:** load (Control Plane, WG 10.99.99.2)
**Warum:** Basis für 3-Node Kubernetes Cluster über WireGuard Mesh
**Auswirkung:** Control Plane läuft, API Server erreichbar, Flannel deployt

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

---

### 2026-01-18 2/3 – Baseline: Monitoring Stack intern abgesichert

**Was:** Aufbau des vollständigen Monitoring Stacks mit Node Exporter auf allen Nodes sowie zentralem Prometheus und lokal gebundenem Grafana. Grafana über gehärteten Nginx Reverse Proxy mit TLS angebunden und Benutzerverwaltung bereinigt.
**Wo:** mirror, load, prod, dash
**Warum:** Verlässliche Sichtbarkeit des Systemzustands vor K3s bei minimaler externer Angriffsfläche.
**Auswirkung:** Alle Nodes liefern Metriken ausschließlich über das WireGuard Netz. Prometheus und Grafana sind nicht direkt öffentlich erreichbar. Monitoring ist rebootfest und reproduzierbar dokumentiert.
**Fix:** Fehlende nftables Freigabe für Node Exporter über wg0 ergänzt. Grafana Default Admin erkannt und durch dedizierte Benutzer ersetzt. Reverse Proxy, TLS und Fail2ban Absicherung ergänzt.

---

### 2026-01-18 1/3 - Baseline: WireGuard Full Mesh Netzwerk

**Was:** Aufbau eines vollständigen WireGuard Mesh zwischen allen Cluster Nodes inklusive NAT Node. Einführung von systemd Autostart, restriktiver nftables Freigaben und dokumentiertem Runbook.
**Wo:** mirror, load, prod, dash
**Warum:** Sichere, konsistente und vom Public Internet entkoppelte Cluster Kommunikation als Grundlage für DRBD, K3s und weitere Dienste.
**Auswirkung:** Interne Cluster Kommunikation läuft ausschließlich über das WireGuard Netz. Öffentliche Abhängigkeiten sind minimiert. Netzwerk ist rebootfest, nachvollziehbar und reproduzierbar.
**Fix:** NAT Fallstrick beim mirror Node identifiziert und durch Anpassung der nftables Regeln (state new für WireGuard UDP) behoben.

---

### 2026-01-17 - Baseline: Security Layer aktiv

**Was:** nftables, Fail2ban und auditd Baseline Rules aktiviert und geprüft. Host Inventare für alle Nodes erstellt.
**Wo:** mirror, load, prod, dash
**Warum:** Einheitlicher Security Standard vor DRBD und K3s Deployment.
**Auswirkung:** Nur SSH ist extern erreichbar, Fail2ban blockt SSH Bots via nftables, kritische Config Dateien werden auditiert, Baseline ist dokumentiert und vergleichbar.

---

### 2026-01-16 - Dokumentation

**Was:** Dokumentation reviewed und erweitert
**Warum:** Dokumentation meiner Aufbauphase
**Auswirkung:** Bessere Nachvollziehbarkeit was gemacht oder geändert wurde

---

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

---

### 2026-01-14 1/2 - Baseline: User & SSH

**Was:** Einheitlicher Admin User angelegt, SSH gehärtet und System aktualisiert.
**Wo:** mirror, load, prod
**Warum:** Grundlage für einen konsistenten und sicheren Cluster Betrieb.
**Auswirkung:** Zentraler, abgesicherter SSH Zugriff auf allen Nodes.

---

### 2026-01-06 – Baseline & Monitoring Basis sowie Daily Backups

**Was:** Aufbau einer minimalen Monitoring Basis mit Node Exporter und Prometheus sowie Einführung eines Daily Backups
**Wo:** dash
**Warum:** Frühzeitige Beobachtbarkeit und Absicherung der Konfigurationen
**Auswirkung:** Neue Systemdienste aktiv, zusätzliche Ports nur lokal gebunden, tägliche Backup Jobs per Cron
