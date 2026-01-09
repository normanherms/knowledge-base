# Homelab-Cluster: Aufbauphasen

---

## Phase 1 – Baseline Cluster (Minimal stabiler Zustand)

### Ziel

Ein funktionierender, klar abgegrenzter Grundcluster ohne automatische Failover-Mechaniken.
Fokus liegt auf Netzwerk, K3s, Storage-Layout und klarer Rollentrennung.

### Schritte

• Monitoring-Stack auf dock-dash
• WireGuard-Mesh vollständig auf allen Hosts einrichten
• /etc/hosts und DNS definieren
• K3s Control Plane auf dock-load installieren
• K3s Worker auf dock-prod und dock-mirror
• OpenCloud auf dock-prod deployen
• Keine DRBD-Produktivnutzung
• Kein Pacemaker
• Kein automatisches Failover

### Erwartetes Ergebnis

Cluster läuft, Pods starten, Storage lokal auf prod.
System ist testbar, reproduzierbar und nachvollziehbar.

---

## Phase 2 – Storage-Replikation und Datenhoheit

### Ziel

Replizierter Storage zwischen Home und RZ ohne Komplexität durch HA-Stack.
Priorität: Datenhoheit über deine Daten, nicht Zero-Downtime.

### Schritte

• DRBD zwischen dock-prod (Primary) und dock-mirror (Secondary) konfigurieren
• Asynchrone Replikation
• Quorum/Arbitrator auf dock-load
• K3s-PVCs bleiben auf dock-prod
• Mirror erhält Replikation ohne aktiven Zugriff
• Dokumentiertes manuelles Failover-Prozedere erstellen

### Erwartetes Ergebnis

Daten liegen an zwei Standorten.
Bei Ausfall von prod sind Daten nicht verloren, aber Failover ist manuell.

---

## Phase 3 – Hochverfügbarkeit (Optional)

### Ziel

Echte HA-Funktionalität über automatisiertes Failover – aber **nur**, wenn Phase 1 und 2 stabil sind und getestet sowie reproduzierbar

### Schritte

• Pacemaker + Corosync auf prod/mirror/load
• SDB-Stonith aktivieren
• DRBD in Primary/Secondary mit Auto-Failover
• Storage-Device als hochverfügbare Resource veröffentlichen
• Pods migrieren automatisch je nach Worker-Verfügbarkeit
• K3s bleibt weiterhin Single Control Plane (bewusster SPOF)

### Erwartetes Ergebnis

Automatisches Umschalten von Storage und Workloads.
Komplexität steigt stark, aber erfüllt echtes HA-Verhalten.

---

## Offene Baustellen / Risiken

1. Control Plane ist bewusst ein SPOF
Akzeptabel, aber Ausfall von dock-load bedeutet Cluster-Neustart.

2. DRBD über WAN
Asynchron notwendig. Wireguard Verschlüsselung sowie Latenz und Bandbreite beeinflussen Catch-Up.

3. CPU-Last durch Ollama
LLM-Last darf nicht in den Worker-Bereich eingreifen.
Die Trennung in dock-edge ist richtig gesetzt.

4. Monitoring-Node als VPS nano
Ressourcen knapp bei Prometheus + Grafana.
Loki könnte Grenzlast erzeugen.

5. Netzwerkkomplexität
Der Mix aus Libvirt, Containerd, flannel und lokalen Bridges bleibt ein Fehlerfaktor daher ist die Auslagerung auf dock-edge korrekt.

6. Keine Persistent Volume - übergreifende Storage-Klassen
K3s bleibt auf prod als PVC-Heimat beschränkt.
Das ist normal in Hybrid-Cluster, aber wichtig zu wissen.

---

## Phasen-Ziele als Checkliste

### Phase 1 (ab jetzt)

[x] dock-dash grundlegend bereit
[ ] dock-prod grundlegend bereit
[ ] dock-mirror grundlegend bereit
[ ] dock-load grundlegend bereit
[ ] WG-Mesh
[ ] K3s Control Plane
[ ] K3s Worker
[ ] OpenCloud Deployment
[ ] Monitoring stabil
[ ] Dokumentation komplett

### Phase 2 (später)

[ ] DRBD Setup Basis
[ ] Replikation testen
[ ] Manuelles Failover testen
[ ] Backups in Synology integrieren
[ ] Dokumentation komplett

### Phase 3 (optional)

[ ] Pacemaker/Corosync
[ ] SDB/STONITH
[ ] Auto-Failover testen
[ ] Endgültige HA-Konfiguration
[ ] Dokumentation komplett
