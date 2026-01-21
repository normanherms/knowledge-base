# Norman Herms – IT-Infrastruktur Portfolio

## Zusammenfassung

- 11 Monate intensive Selbstausbildung neben Vollzeitjob im Einzelhandel
- Systematischer Aufbau von Linux- und Infrastruktur-Kenntnissen
- Praktische Projekte: Cluster-Baseline, WireGuard Mesh, Monitoring

## Skills (Stand Januar 2026)

| Bereich | Technologien | Status | Nachweis |
|---------|--------------|--------|----------|
| Linux Admin | Debian, systemd, nftables | Produktiv | [Baseline](/infrastructure/cluster/baseline/baseline_checkliste.md), [Runbooks](/infrastructure/cluster/runbooks/) |
| Netzwerk | WireGuard, VPN Mesh, Firewall | Produktiv | [WG Runbook](/infrastructure/cluster/runbooks/wireguard.md) |
| Monitoring | Prometheus, Grafana, Node Exporter | Produktiv | [Monitoring Runbook](/infrastructure/cluster/runbooks/monitoring.md) |
| Security | SSH Hardening, fail2ban, auditd | Produktiv | [SSH Runbook](/infrastructure/cluster/runbooks/ssh.md) |
| Container | containerd, nerdctl | Produktiv | [Homelab Inventory](/infrastructure/homelab/inventory/edge.md) |
| Automatisierung | Ansible | Gelernt | [Cheatbook](/cheatbooks/ansible.md) |
| Scripting | Python, Bash | Gelernt | [Cheatbooks](/cheatbooks/python-grundkurs.md) |
| Cluster | K3s, DRBD | In Planung | [Architecture](/infrastructure/cluster/docs/architecture.md) |

## Hauptprojekte

### 1. Cluster-Baseline (Jan 2026)

**Problem:** 7 gescheiterte Cluster-Iterationen durch inkonsistente Setups
**Lösung:** Reproduzierbarer Bootstrap-Prozess mit Checkpoints
**Ergebnis:** 4 Nodes sauber deployed, von "5h mit Fehlern" zu "1h zero issues"
**Stack:** Debian 13, nftables, systemd, SSH hardening
**Nachweis:** [Baseline Checkliste](/infrastructure/cluster/baseline/baseline_checkliste.md) | [Changelog](/infrastructure/cluster/CHANGELOG.md)

### 2. WireGuard Full Mesh (Jan 2026)

**Problem:** Sichere Cluster-Kommunikation über WAN + Heimnetz
**Lösung:** Full Mesh mit NAT-Node-Support, rebootfest, dokumentiert
**Ergebnis:** Funktionierendes privates Netzwerk für 4 Nodes
**Stack:** WireGuard, nftables, systemd
**Nachweis:** [WG Runbook](/infrastructure/cluster/runbooks/wireguard.md) | [Network Plan](/infrastructure/cluster/docs/network-plan.md)

### 3. Monitoring Stack (Jan 2026)

**Problem:** Keine Sichtbarkeit über Cluster-Zustand
**Lösung:** Zentrales Prometheus + Grafana + Node Exporter auf allen Nodes
**Ergebnis:** Vollständige Metriken, intern abgesichert, rebootfest
**Stack:** Prometheus, Grafana, nginx Reverse Proxy mit TLS
**Nachweis:** [Monitoring Runbook](/infrastructure/cluster/runbooks/monitoring.md)

### 4. Homelab Production Services (2025)

**Problem:** Self-hosted Alternativen zu Cloud-Diensten
**Lösung:** Multi-Container-Setup mit libvirt VMs
**Ergebnis:** 10+ Services produktiv (Wiki, Rezepte, Media Server, DNS, etc.)
**Stack:** containerd, nerdctl, libvirt, systemd-networkd
**Nachweis:** [Homelab Inventory](/infrastructure/homelab/inventory/edge.md)

## Lernweg (dokumentiert)

- **Linux Essentials** – abgeschlossen
- **LPIC-1** – abgeschlossen
- **Git** – abgeschlossen
- **Ansible** – abgeschlossen
- **Python Grundkurs** – abgeschlossen
- **Bash Scripting** – in Arbeit

Alle mit persönlichen Cheatbooks dokumentiert: [Cheatbooks](/cheatbooks/)

## Iterationshistorie

**7 Cluster-Neuaufbauten** mit dokumentierten Fehlern und Learnings:

- Iteration 0-3: Trial-and-Error ohne Plan
- Iteration 4-5: Funktionierende aber instabile Setups
- Iteration 6: Rollen-Konflikt-Erkenntnis
- Iteration 7: Saubere Architektur (aktuell)

Details: [Iterations History](/infrastructure/cluster/docs/iterations-history.md)

## Nächste Schritte (geplant)

- K3s Control Plane Deployment
- DRBD Storage Replication
- OpenCloud auf K3s
