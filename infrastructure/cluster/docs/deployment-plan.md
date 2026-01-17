# Homelab-Cluster: Aufbauphasen

---

## Phase 1 – Baseline Cluster (Minimal stabiler Zustand)

### Ziel

Ein funktionierender, klar abgegrenzter Grundcluster ohne automatische Failover-Mechaniken.
Fokus liegt auf sichere Einrichtung ein klares Netzwerk, K3s, Storage-Layout und Rollentrennung.

### Schritte

- Baseline auf allen Nodes setzen
- Baseline kontrollieren ggf. Nacharbeiten falls Punkte nicht umgesetzt wurden
- WireGuard-Mesh vollständig auf allen Hosts einrichten
- Monitoring-Stack auf `dash`
- K3s Control Plane auf `load` installieren
- K3s Worker auf `prod` und `mirror`
- OpenCloud auf prod deployen


### Out of Scope

- DRBD-Produktivnutzung
- Pacemaker/Corosync
- automatisches Failover

### Erwartetes Ergebnis

Cluster läuft, Pods starten, Storage lokal auf prod.
System ist testbar, reproduzierbar und nachvollziehbar.

---

## Phase 2 – Storage-Replikation und Datenhoheit

### Ziel

Replizierter Storage zwischen Home und RZ ohne Komplexität durch HA-Stack.
Priorität: Datenhoheit über Daten, nicht Downtime. Mirror muss Secondary bleiben

### Schritte

- DRBD zwischen prod (Primary) und mirror (Secondary) konfigurieren
- Asynchrone Replikation
- Quorum-Deamon auf load
- K3s-PVCs bleiben auf prod
- Mirror erhält Replikation ohne aktiven Zugriff
- Backupsicherung auf Synology NAS
- Dokumentiertes manuelles Failover-Prozedere erstellen

### Erwartetes Ergebnis

Daten liegen an zwei Standorten.
Bei Ausfall von prod sind Daten nicht verloren, aber Failover ist manuell.

---

## Theoretische Phase 3 – Hochverfügbarkeit (umsetzung wird geprüft)

### Zielidee

Echte HA-Funktionalität über automatisiertes Failover – aber **nur**, wenn Phase 1 und 2 stabil sind und getestet sowie reproduzierbar

### Schritte theoretisch

• Pacemaker + Corosync auf prod/mirror/load
• DRBD in Primary/Secondary mit Auto-Failover
• Pods migrieren automatisch je nach Worker-Verfügbarkeit
• K3s bleibt weiterhin Single Control Plane (bewusster SPOF)

### Erwartetes Ergebnis

Automatisches Umschalten von Storage und Workloads.
Komplexität steigt stark, aber erfüllt echtes HA-Verhalten.

---

## Offene Baustellen / Risiken

1. Control Plane ist bewusst ein SPOF
Akzeptabel, aber Ausfall von load bedeutet Cluster-Neustart.

2. DRBD über WAN
Asynchron notwendig. Wireguard Verschlüsselung sowie Latenz und Bandbreite beeinflussen Catch-Up.

3. Monitoring-Node als VPS nano
Ressourcen knapp bei Prometheus + Grafana.

4. Keine Persistent Volume - übergreifende Storage-Klassen
K3s bleibt auf prod als PVC-Heimat beschränkt.
Das ist normal in Hybrid-Cluster, aber wichtig zu wissen.

5. Failover Logik geht nicht auf da keine Risikofreie Replikation möglich.
Fencing Mechanik nicht umsetzbar.

---

## Phasen-Ziele aktueller Stand

### Phase 1 (ab Januar)

[x] dash Baseline gesetzt
[x] prod Baseline gesetzt
[x] mirror Baseline gesetzt
[x] load Baseline gesetzt
[ ] WG-Mesh
[ ] K3s Control Plane
[ ] K3s Worker
[ ] OpenCloud Deployment
[ ] Monitoring stabil
[ ] Dokumentation komplett

### Phase 2 (später)

[ ] DRBD Setup
[ ] Daten Migration
[ ] Replikation testen
[ ] Manuelles Failover testen
[ ] Backups in Synology integrieren
[ ] Dokumentation komplett

### Phase 3 (optional)

- aktuell keine Lösung für Fencing Mechaniken
- mirror muss per policy Secondary bleiben
- Lösung für IPMI wird geprüft
