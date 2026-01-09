# Homelab Cluster Architektur (v1.1)

## Ziel

Das Cluster dient der Souveränität über eigene Daten und Anwendungen.
Es ermöglicht das Erlernen von Clusterisierung, Containerisierung, Virtualisierung und Netzwerktechnik.
Im Vordergrund stehen Stabilität, Nachvollziehbarkeit und die Fähigkeit, Anwendungen hochverfügbar zu betreiben.

## Aufgabe des Clusters

- Hochverfügbare Bereitstellung von Anwendungen und Daten
- Fortlaufender Betrieb bei Ausfällen einzelner Komponenten
- Replizierte Datenhaltung über DRBD
- Automatisches Scheduling und Wiederherstellung von Diensten

## Probleme aus vorherigen Cluster-Builds

- Dienste teilten sich auf einzelnen Nodes dieselben Ressourcen (CPU, Netzwerk, Storage)
- Komplexe Fehleranalyse durch gemischte Rollen (VM-Host, Container-Host, Worker, KI Inferenz gleichzeitig)
- Grenzwerte wurden nicht frühzeitig eingehalten
- Architektur war nicht reproduzierbar

---

## Finale Architektur

## Lenovo ThinkCentre M910q (dock-mirror)

### Specs

- Intel i5-7500T
- 32 GB RAM
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

## Dell Optiplex 3070 Micro (dock-edge)

### Specs

- Intel i5-9500T
- 32 GB RAM
- 1 TB NVMe SSD

### Aufgaben

- Heim- / Compute-Node
- VM-Host
- Container Host
- Kein K3s
- Kein DRBD

### Anwendungen

- Ollama (Gemma3n:4b)
- Home Assistant (VM)
- AdGuard Home
- Anytype
- Weitere lokale Dienste

---

## Netcup Root Server G12 #1 (dock-prod)

### Specs

- AMD EPYC 9645 (4 dedizierte Kerne)
- 8 GB DDR5 ECC
- 256 GB NVMe SSD
- 2.5 Gbit/s Netzwerk

### Aufgaben

- K3s Worker Node
- DRBD Primary
- Persistenter Storage im Cluster

### Anwendungen

- OpenCloud (Pod)
- Worker-Workloads

---

## Netcup Root Server G12 #2 (dock-load)

### Specs

- AMD EPYC 9645 (4 dedizierte Kerne)
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
- Keine Container
- Keine VMs

---

## Netcup VPS nano (dock-dash)

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

## Netcup Reserve Node VPS nano

### Rolle

- Keine kritische Funktion
- Reserve Node (Test / Debug / temporäre Tools)

### Anwendungen

- frei einsetzbar für Experimente

---
