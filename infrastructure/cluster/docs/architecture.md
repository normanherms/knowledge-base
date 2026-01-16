# Homelab Cluster Architektur (v1.2)

## Ziel

Das Cluster dient der Souveränität über eigene Daten und Anwendungen.
Es ermöglicht das Erlernen von Clusterisierung, Containerisierung, Virtualisierung und Netzwerktechnik.
Im Vordergrund stehen Stabilität, Nachvollziehbarkeit und die Fähigkeit, Anwendungen im späteren Verlauf hochverfügbar zu betreiben.

## Aufgabe des Clusters

- Bereitstellung von Anwendungen und Daten
- Fortlaufender Betrieb bei Ausfällen einzelner Komponenten
- Replizierte Datenhaltung über DRBD
- Automatisches Scheduling und Wiederherstellung von Diensten

## Probleme aus vorherigen Cluster-Builds

- Dienste teilten sich auf einzelnen Nodes dieselben Ressourcen (CPU, Netzwerk, Storage)
- Komplexe Fehleranalyse durch gemischte Rollen (VM-Host, Container-Host, Worker, KI Inferenz gleichzeitig)
- Grenzwerte wurden nicht frühzeitig eingehalten
- Architektur war nicht reproduzierbar

## Probleme bei aktueller Iteration

- mirror ist aktuell nicht fencebar da kein IPMI Modul
- aus Hochverfügbar wird höchstens Backup ähnlich

---

## Finale Architektur

## Lenovo ThinkCentre M910q (mirror)

### Specs

- Intel i5-7500T
- 32 GB DDR4 RAM
- 1 TB NVMe SSD

### Aufgaben

- K3s Worker Node
- DRBD Secondary

### Anwendungen

- Ausführung von Worker-Pods
- Keine VMs
- Keine Heimdienste
- Keine zusätzlichen Container

---

## Netcup Root Server G12 #1 (prod)

### Specs

- AMD EPYC (4 dedizierte Kerne)
- 8 GB DDR5 ECC
- 256 GB NVMe SSD
- 2.5 Gbit/s Netzwerk

### Aufgaben

- K3s Worker Node
- DRBD Primary

### Anwendungen

- OpenCloud (Pod)
- Worker-Workloads

---

## Netcup Root Server G12 #2 (load)

### Specs

- AMD EPYC (4 dedizierte Kerne)
- 8 GB DDR5 ECC
- 256 GB NVMe SSD
- 2.5 Gbit/s Netzwerk

### Aufgaben

- K3s Control Node
- Ingress
- API-Server
- DRBD Quorum-Daemon

### Anwendungen

- Keine produktiven Workloads
- Keine VMs

---

## Netcup VPS nano (dash)

### Specs

- 2 vCores
- 2 GB RAM
- 60 GB SSD

### Aufgaben

- Monitoring / Observability

### Anwendungen

- Node Exporter für alle Cluster-Nodes
- Prometheus (kleine Instanz)
- Grafana

---
