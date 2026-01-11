# Homelab-Cluster - Iterationshistorie

## Warum dieses Projekt existiert

**Dezember 2024:** Ich habe angefangen, mit ChatGPT einen ESP32-Gartensensor für meine Freundin zu bauen. Die Idee war, das System zumindest in einen Prototypen zu verwandeln – mit Server-Backend, Datenverarbeitung und allem was dazugehört. Zum ersten Mal dachte ich ernsthaft über Infrastruktur nach.

**Januar 2025:** Geopolitisch ist die Welt im Wandel, die gesamte IT-Welt läuft zum Großteil über US-Infrastruktur. Cloud-Dienste, KI-Plattformen, Datenspeicher und so weiter, alles USA. Das hat mich zum Nachdenken gebracht: Was kann man mit Open Source selbst bauen? Welche Alternativen gibt es? Wie kann man Datenhoheit zurückgewinnen?

**Februar 2025:** Daraus entstand mein erster Homelab-Server. Ein alter PC, viel zu stromhungrig, aber der Anfang. Die Faszination blieb – also kaufte ich einen Lenovo M910q ThinkCentre, rüstete ihn auf und begann ernsthaft zu lernen.

**Juni 2025** Ich dachte wenn ich das schaffe mache ich eine Website draus wo jeder Anfänger nachlesen kann und Hilfe bekommen kann. Ich wollte, dass Menschen selbst entscheiden können, wo sie ihre Daten lassen. Das Thema habe ich inzwischen wieder halb verworfen. Der Aufwand wäre so groß das ich es nicht bewältigen könnte. Zumal ich selbst noch Anfänger bin.

**Die Realität:** Das alles passierte neben einer Vollzeitstelle im Einzelhandel. 10-Stunden-Schichten, Start um 5 Uhr morgens. Jeden Tag. Nach Hause kommen, mit der Partnerin einen Kaffee trinken und versuchen, aus dem restlichen Tag noch etwas zu machen, so gut es ging. Um 20 Uhr ins Bett, weil der Wecker früh klingelt.

**Die Erkenntnis:** Während ich durch die Iterationen ging, Server aufsetzte, alles wieder abriss, neu baute, scheiterte, lernte wurde mir klar: **Ich will in die IT.** Nicht nur als Hobby. Sondern als Karriere. Raus aus dem Einzelhandel, rein in eine Branche wo technisches Verständnis und Problemlösung zählen.

**Was folgte:** 11 Monate intensives Lernen neben dem Job. Parallel: Linux Essentials, LPIC-1 angefangen, Python, Git, Ansible, Bash. 7 Cluster-Iterationen mit mehreren kompletten Neuaufbauten. Die Erkenntnis, dass echtes Infrastruktur-Verständnis nicht aus Tutorials kommt – sondern aus Fehlern, Reflexion und Durchhaltevermögen.

Diese Dokumentation zeigt nicht nur mein aktuelles Setup, sondern den gesamten Weg – mit Umwegen, Fehlern und Learnings. Leider ist nicht alles mehr enthalten aber für einen groben Abriss reicht es.

---

## Die Iterationen

Eine dokumentierte Geschichte meiner Homelab-Cluster-Iterationen. Das ist kein Erfolgs-Portfolio – es ist ein ehrlicher Lernweg mit gescheiterten Versuchen, kompletten Neuaufbauten und hart erkämpften Erkenntnissen über Infrastruktur-Design.

---

## Iteration 0: "Das Dachboden-Lab" (Anfang Februar 2025)

**Hardware:**

- Alter PC auf dem Dachboden
- 2× HDDs
- Realtek WLAN-Chip
- LAN über Fritz Repeater

**Konzept:**

- Debian
- NordVPN Meshnet (sogar im LAN verschlüsselt)
- SSH mit ed25519 Keys statt Passwörter
- Wake-on-LAN

**Was funktionierte:**

- SSH Login
- Wake-on-LAN
- Grundlegendes System

**Warum abgerissen:**

- "Dieses Rumgeier nervt mich"
- Zig mal neu installiert
- Kein Plan, keine Struktur
- Copy-Paste ohne Verständnis

**Learning:**
> Trial-and-Error ohne Plan führt zu Frust

---

## Iteration 1:  (Feb/März 2025)

**Hardware:**

- Selber Dachboden-PC
- 2× HDDs (1TB System, 4TB Daten)
- Realtek WLAN (benötigte Backports-Kernel)

**Geplante Architektur:**

- Debian 12 Bookworm minimal, keine GUI
- Podman rootless-only (aus Alivestack Repos)
- Kernel aus Backports (wegen WLAN)
- Firewall: Alles standardmäßig blockiert
- SSH key-only, IPv6 deaktiviert

**Was umgesetzt wurde:**

- Debian 12 Installation ✓
- Benutzerstruktur ✓
- Storage-Trennung (/srv, /cont, /data) ✓
- Basis-Backup mit rsync ✓

**Was nicht fertig wurde:**

- SSH Key-only Setup
- Firewall-Konfiguration
- Rootless Podman Setup
- NordVPN Integration
- WLAN-Konfiguration
- Monitoring

**Warum abgerissen:**

- Podman aus Debian Repos zu alt
- Alivestack Repos zu kompliziert
- Entscheidung: Docker statt Podman

**Learning:**
> Copy-Paste von Befehlen ohne zu verstehen was sie tun, erzeugt nicht wartbare Systeme

---

## Iteration 2: "Die Cluster-Fantasie" (April/Mai 2025)

**Der Gedankengang:**

- "Was ist Kubernetes?"
- "Können wir High Availability machen?"
- "Dann hätten wir auch einen Cluster! 😂"

**Die Idee:**

- Zweiter Server für HA
- DRBD für Datensynchronisation
- Hetzner VPS + Heimserver = Cluster

**Ergebnis:**

- Verständnis, dass K8s Overkill für Homelab ist
- Plan für HA mit Corosync, Pacemaker
- Entscheidung für DRBD

**Learning:**
> Brauche zweiten Server für echte Cluster-Architektur

---

## Iteration 3: "Drei-Server-Hybrid-Cluster" (30. April 2025)

**Hardware:**

1. **Heimserver:** (Dachboden)
2. **Hetzner VPS:** (produktionsbereit)
3. **Contabo VPS:** (Loadbalancer)

**Alle mit identischer Security:**

- SSH Port 2222, key-only
- Root deaktiviert
- Fail2Ban aktiv
- IPv6 blockiert
- iptables: nur 2222, 80, 443 offen

**Warum abgerissen:**

- Zu komplex
- Unklar was wo läuft
- DRBD über Internet funktionierte nicht wie erwartet
- Wechsel zu Netcup

**Learning:**
> Drei Server sind zu viel für den Anfang. DRBD über Internet ist schwierig.

---

## Iteration 4: "Der Netcup-Pivot" (Mai 2025)

**Hardware:**

1. **Netcup Root Server** (zentrale Instanz)
2. **Netcup VPS Nano** (Loadbalancer, Traefik + Pangolin)
3. **Heimserver** (ThinkCentre)

**Deployed Services:**

- Vaultwarden (produktiv) ✓
- OpenCloud (produktiv) ✓
- Keycloak (Auth) ✓
- Redis, Mail, Uptime Kuma

**Infrastruktur:**

- Docker (kein Podman)
- Traefik v3 als Reverse Proxy
- Cloudflare Tunnel
- iptables mit Cloudflare-IP-Whitelist

**Status Mai 2025:**

- Funktioniert ✓
- Vaultwarden & OpenCloud produktiv
- Aber: Heimserver "zu energiehungrig"

**Warum abgerissen:**

- Zu viele Services gleichzeitig
- Nicht klar strukturiert
- Setup war funktional aber nicht stabil

**Learning:**
> Funktionierendes Setup ≠ stabiles Setup

---

## Iteration 4.5: (Mitte Mai 2025)

**klare Benennung:**

dock-load
dock-prod
dock-mirror (Heimserver)

**Geplante Roadmap:**

1. Vaultwarden WebAuthn fixen
2. OpenCloud einrichten (Prod + Mirror Backup)
3. Anytype Server (nur lokal auf Mirror)
4. Weitere Services: Keycloak, Outline, Mailcow, Watchtower, Portainer, Netdata
5. Synchronisation: rsync/rclone prod → mirror

**Status:**

- Basis läuft ✓
- Aber viele TODOs offen
- WebAuthn-Probleme
- Mirror noch leer

**Warum abgerissen:**

- Große Roadmaps helfen nicht, wenn man sie nicht abarbeitet

**Learning:**
> Planung ist einfach, Umsetzung ist schwer

---

## Iteration 5: (August 2025)

**Hardware:**

- dock-prod (Netcup Root VPS)
- dock-load (Netcup VPS)
- dock-web (Netcup VPS)
- dock-mirror (Lenovo M910q)

**Stack:**

- Debian 12 CLI auf allen Nodes
- Docker
- DRBD zwischen prod und mirror (geplant)
- K3s nur für OpenCloud (geplant)
- Checkmk Monitoring auf allen Nodes

**Erstellte Dokumentation:**

- stack.md
- k3s-plan.md
- recovery.md
- README.md

**Status August:**

- Dokumentation existiert
- Aber: System nicht deployed
- "Bereit für nächsten Schritt"

**Warum abgerissen:**

- Dokumentation ≠ Implementation
- System war "bereit" aber nicht "fertig"
- Zu komplex, zu viele Baustellen gleichzeitig

**Kern-Erkenntnis:**
> "Dienste teilten sich Ressourcen auf einzelnen Nodes"
> "Komplexe Fehleranalyse durch gemischte Rollen"
> "Architektur war nicht reproduzierbar"

---

## Iteration 6: (Ende November 2025)

**Die große Erkenntnis (24. November 2025):**

> "Deine alten Cluster waren nicht unsinnig - sie waren nur zu früh, zu viel parallel und zu viele Rollen pro Host."

**Was falsch war:**

- Zu früh in Komplexität (DRBD + K3s + WireGuard + Flannel gleichzeitig)
- Rollen vermischt (Storage + K3s + DNS + libvirt + Container auf einem Host)
- Falsche Reihenfolge (erst DRBD, dann K3s, dann DNS, dann wieder DRBD...)
- Gegen das System gearbeitet (Netzwerkbrücken + Flannel + WireGuard gleichzeitig)

**Identifizierte technische Probleme:**

- **containerd und K3s kloppen sich ums Netzwerk**
- **libvirt und K3s beißen sich beim Networking**
- **Overhead auf einzelnem System zu hoch**
- Fehlersuche dauert ewig - Fehler springen von einem Problem zum nächsten
- Wenn Lösungen unbekannt sind: Stunden suchen vs. Server in gleicher Zeit neu aufsetzen

**Die neue Strategie:**

- **Strikte Rollentrennung**
- **Nicht alles gleichzeitig**
- **Minimierung der Komplexität pro Node**

**Hardware-Neuverteilung:**

- **Dell Optiplex 3070** → dock-edge (Homelab-Node, KEIN K3s)
- **Lenovo M910q** → dock-mirror (K3s-Node, dediziert)
- **2× Netcup Root Server** → dock-prod, dock-load
- **1× Netcup VPS** → dock-dash (Monitoring)

**Runbook erstellt (25. November 2025):**

- Debian 13 Trixie
- Storage-Layout dokumentiert
- Netzwerk (systemd-networkd + NetworkManager)
- Bridge br0 für libvirt
- Mountpoints: /cont, /images, /data, /backup

**Status Ende November:**

- dock-edge dokumentiert
- Aber: Dezember = Weihnachtszeit im Handel
- Setup liegt brach

**Learning:**
> Jeder Server braucht eine einzelne, klare Rolle. Minimale Komplexität pro Node ist essentiell.

---

## Iteration 7: Finales geplantes Setup (Januar 2026 - AKTUELL)

**Hardware & Rollen (FINAL):**

| Host | Hardware | Rolle | Aufgaben |
|------|----------|-------|----------|
| **dock-prod** | Netcup Root G12 | K3s Worker, DRBD Primary | OpenCloud, Storage |
| **dock-load** | Netcup Root G12 | K3s Control Plane, Quorum | API, Ingress, DRBD Quorum |
| **dock-mirror** | Lenovo M910q | K3s Worker, DRBD Secondary | Worker Pods, Replikation |
| **dock-edge** | Dell Optiplex 3070 | Home/Compute (KEIN K3s!) | Ollama, HA VM, AdGuard, n8n, Anytype |
| **dock-dash** | Netcup VPS nano | Monitoring | Prometheus, Grafana |
| **synology214** | DS214+ | Backup | Cold Storage |

**Netzwerk:**

- Heimnetz: 192.168.1.0/24
- WireGuard Mesh: 10.99.99.0/24
- Klare IP-Planung mit Primary + Reserve IPs

**3-Phasen-Plan:**

- **Phase 1:** Baseline Cluster (WG-Mesh, K3s, OpenCloud, Monitoring)
- **Phase 2:** Storage-Replikation (DRBD, manuelles Failover)
- **Phase 3:** Optional HA (Möglichkeiten werden geprüft)

**Architektur-Prinzipien:**

- Strikte Rollentrennung
- K3s nur für OpenCloud
- dock-edge bewusst AUSSERHALB des Clusters
- Keine Netzwerk-Kollisionen (libvirt auf dock-edge, nicht im Cluster)

**Dokumentation:**

- Architektur.md
- Netzwerk.md
- design.md (3-Phasen-Plan)

**Status Januar 2026:**

- dock-dash grundlegend bereit
- Fencing sowie Quorum aktuell nicht umsetzbar da kein Fence Machanismus vorhanden
- Alles andere: noch nicht deployed

---

## Parallel durchlaufener Lernweg

Während der Cluster-Iterationen gelernt:

- **Linux Essentials** - Grundlagen
- **LPIC-1** - Angefangen, in Arbeit
- **Python** - Scripting und Automatisierung
- **Git** - Versionskontrolle
- **Bash** - Shell-Scripting
- **Infrastruktur-Konzepte** - DNS, Networking, Storage, Clustering
- **ChatGPT** - ein Werkzeug keine interaktive Anleitung

---

## Wichtigste Erkenntnisse

### Technische Learnings

1. **Copy-Paste ohne Verständnis erzeugt technische Schulden**
   - Frühe Iterationen: Tutorials blind gefolgt
   - Ergebnis: Nicht wartbare Systeme

2. **Eine Rolle pro Server**
   - Gemischte Rollen (K3s + libvirt + Container + Storage) = nicht wartbar
   - Netzwerk-Stacks kollidieren (containerd vs K3s vs libvirt vs WireGuard)
   - Fehler-Isolation wird unmöglich

3. **Komplexität muss inkrementell sein**
   - Kann nicht DRBD + K3s + HA + Monitoring gleichzeitig deployen
   - Brauche: Baseline → Storage → HA (phasenbasierter Ansatz)

4. **Netzwerk ist der schwierigste Teil**
   - Mehrere Netzwerk-Layer (flannel, libvirt bridges, WireGuard, containerd) erzeugen Konflikte
   - Muss verstehen wer Default-Routes setzt, NAT-Regeln, iptables-Chains oder NFtables Ruleset

5. **Dokumentation ≠ Implementation**
   - Kann Architektur dokumentieren
   - Muss sie trotzdem noch bauen

### Prozess-Learnings

1. **Planung vs. Umsetzung**
   - Einfach große Roadmaps zu planen
   - Schwer sie Schritt für Schritt umzusetzen

2. **Troubleshooting-Zeit vs. Rebuild-Zeit**
   - Manchmal schneller neu aufzusetzen als kaskadierende Fehler zu debuggen
   - Besonders wenn Lösungen unbekannt sind

3. **Learning by doing (und scheitern)**
   - Jede gescheiterte Iteration hat etwas gelehrt

### Aktueller Status

- **7 Iterationen über ~11 Monate**
- **Mehrere komplette Neuaufbauten**
- **Aktuell:** Saubere Architektur definiert, minimales Deployment
- **Nächster Schritt:** Phase 1 Implementation

---

## Warum dieses Dokument existiert

Diese Dokumentation existiert weil:

1. **Ehrlichkeit beim Lernen** - Nicht jedes Homelab ist eine Erfolgsgeschichte
2. **Dokumentation von Fehlern** - Die wichtigsten Lektionen kommen aus dem was nicht funktioniert hat
3. **Zukünftige Referenz** - Wenn die Versuchung kommt wieder Rollen zu mischen, erinnern warum es gescheitert ist
4. **Bewerbungen** - Zeigt Lernprozess, Problem-Solving und Durchhaltevermögen
5. **Peer Review & Community** - Andere sollen aus meinen Fehlern lernen können

---

Zuletzt aktualisiert: 11. Januar 2026
