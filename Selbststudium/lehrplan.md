# Lehrplan: Virtualisierung · Container · Automation · Orchestrierung

Version 1.0 | Stand: 2025-10-12

Ein praxisorientierter Lernpfad, der dich von den Grundlagen der Virtualisierung bis zum Betrieb deines eigenen K3s-Clusters führt.
Ziel ist ein solides, alltagstaugliches Verständnis – kein Expertenwissen, sondern funktionales Können.

---

## Level 0 – KVM & Libvirt (Virtualisierung verstehen)

**Ziel:**
Grundlagen der Virtualisierung begreifen und einfache VMs sicher betreiben.

**Themen:**

* Funktionsweise von KVM & QEMU
* Verwaltung über libvirt (`virsh`, `virt-manager`)
* Storage Pools, Volumes und Netzwerke
* Snapshots & Backup-Grundlagen

**Praxis:**

* VM mit `virt-install` oder `virt-manager` erstellen
* Netzwerktyp „default“ prüfen
* Volume anlegen, Snapshot testen
* Doku: *„Meine erste VM mit Libvirt“*

**Hinweis:**
`virt-manager` ist optional hilfreich zur Visualisierung, die CLI sollte aber bevorzugt genutzt werden, um später den Terraform-Vergleich besser nachvollziehen zu können.

**Praktische Übungen:**

* Erstelle zwei VMs mit unterschiedlichen Speichergrößen und beobachte deren Performance.
* Exportiere eine VM als qcow2 und importiere sie erneut auf einem anderen Host.

**Troubleshooting:**

* VM startet nicht → Berechtigungen auf qcow2 prüfen
* Netzwerk nicht erreichbar → Bridge/NAT-Status prüfen

**Aufräumen:**

* VM mit `virsh destroy` und `virsh undefine` sauber entfernen

---

## Level 1 – Fundament (Linux-Isolation)

**Ziel:**
Verstehen, wie Linux Container und Prozesse voneinander trennt.

**Themen:**

* Namespaces, cgroups, OverlayFS
* Vergleich: VM vs. Container
* Netzwerkkonzepte (veth, bridge)

**Praxis:**

* `unshare` & `chroot` ausprobieren
* Bridge-Netz erstellen und testen
* Doku: *„Wie Linux isoliert“*

**Praktische Übungen:**

* Starte mit `unshare --pid --fork bash` eine isolierte Prozessumgebung und vergleiche Prozesslisten.
* Simuliere eine eigene Root-Umgebung mit `debootstrap` + `chroot`.

**Troubleshooting:**

* Prozess bleibt sichtbar → falsche Namespace-Option gewählt
* Kein Internet im isolierten Netz → Bridge falsch konfiguriert

**Aufräumen:**

* Erstellte Namespaces und Netzwerkgeräte mit `ip link delete` entfernen

---

## Level 2 – containerd & nerdctl

**Ziel:**
Container mit containerd ohne Docker verstehen und nutzen.

**Themen:**

* Architektur: containerd, runc, nerdctl
* Images, Layers und Volumes
* Rootless vs. Rootful Container

**Praxis:**

* `containerd` + `nerdctl` installieren
* `nerdctl run alpine` starten
* Rootless-Modus einrichten (`containerd-rootless-setuptool.sh install`)
* Unterschiede in Ports, Storage und Berechtigungen beobachten
* Doku: *„Container ohne Docker“*

**Hinweis:**
Optional kann hier `nerdctl compose` eingebaut werden, um Docker-Compose-Konzepte und Multi-Container-Workloads früh verständlich zu machen.

**Praktische Übungen:**

* Starte zwei Container (nginx und redis) und verbinde sie über ein eigenes CNI-Netzwerk.
* Führe denselben Container einmal rootless und einmal rootful aus und vergleiche Logs und Storage-Pfade.

**Troubleshooting:**

* Container startet nicht → CNI-Plugins prüfen
* Rootless schlägt fehl → `$XDG_RUNTIME_DIR` prüfen

**Aufräumen:**

* `nerdctl system prune -a`

---

## Level 3 – Infrastruktur-Automation

**Ziel:**
Automatisiert VMs bereitstellen und konfigurieren.

**Themen:**

* Terraform & Libvirt-Provider
* Cloud-Init für SSH & User-Setup
* Ansible: Playbooks & Idempotenz
* Cloud-Init Debugging und YAML-Fallen

**Praxis:**

* VM per Terraform + Cloud-Init erstellen
* Ansible-Playbook für Basiskonfiguration
* SSH-Key-Fehler simulieren und beheben
* Doku: *„VM as Code“*

**Challenge:**
Erstelle mit Terraform eine VM, die beim Boot automatisch einen Nginx-Container startet (Cloud-Init + nerdctl). Der Nginx soll eine statische Seite mit ‘Hello from Automation’ anzeigen. Ergänze dazu eine Validierung über `ansible-lint` und `terraform validate`, um Qualitätssicherung zu üben.

**Praktische Übungen:**

* Erstelle mit Terraform eine VM, die automatisch `htop` via Cloud-Init installiert.
* Baue ein einfaches Ansible-Playbook, das Zeitzone, Benutzer und Basis-Pakete konfiguriert.

**Troubleshooting:**

* Keine SSH-Verbindung → `cloud-init` Logs prüfen (`/var/log/cloud-init.log`)

**Aufräumen:**

* `terraform destroy` + `virsh vol-delete`

---

## Level 4 – KubeVirt (Hybrid-Virtualisierung)

**Ziel:**
Virtuelle Maschinen in Kubernetes verstehen und nutzen.

**Themen:**

* KubeVirt-Architektur (Operator, CRDs, API)
* VMs als Kubernetes-Ressourcen
* Integration in K3s

**Praxis:**

* KubeVirt im K3s-Cluster installieren
* Erste VM im Cluster deployen
* Netzwerk und Storage testen
* Doku: *„VMs im Kubernetes-Cluster“*

**Hinweis:**
Installation von `virtctl` über kubevirt.io oder Paketmanager anmerken – notwendig für viele VM-Operationen.

**Praktische Übungen:**

* Deploye eine kleine Debian-VM in KubeVirt und überprüfe Zugriff per `virtctl console`.
* Teste, ob VMs und Pods sich über ClusterDNS gegenseitig erreichen.

**Troubleshooting:**

* VirtLauncher Fehler → `virtctl console` Logs prüfen

**Aufräumen:**

* `kubectl delete vm <name>` + `kubectl delete namespace kubevirt`

---

## Level 5 – K3s & Orchestrierung

**Ziel:**
Einen funktionierenden Container-Cluster aufbauen.

**Themen:**

* Kubernetes-Grundlagen (Pods, Deployments, Services)
* K3s-Architektur und CLI
* Container Networking (CNI)
* Ingress & LoadBalancer
* Ausblick: Service Mesh (Cilium, Linkerd)

**Praxis:**

* K3s-Cluster mit 2 Nodes (Server + Agent)
* Nginx-Deployment und Service
* Doku: *„Mein erster Cluster“*

**Hinweis:**
Debug-Kommandos wie `kubectl get nodes`, `kubectl describe pod` und `kubectl logs` unbedingt einüben – sie sind Schlüsselwerkzeuge im Alltag.

**Praktische Übungen:**

* Erstelle ein Multi-Container-Deployment mit Frontend und Backend.
* Implementiere einen Ingress für den Zugriff über Hostnamen.

**Troubleshooting:**

* Pod startet nicht → Events prüfen
* Netzwerkproblem → `kubectl exec` + `ping` zwischen Pods testen

**Aufräumen:**

* `k3s-uninstall.sh` + Agenten entfernen

---

## Level 6 – DockSeed Production

**Ziel:**
Dein Wissen auf reale Projekte anwenden.

**Themen:**

* Zero-Trust (WireGuard, SSH-Härtung)
* Monitoring (Netdata, Grafana)
* Backup & Replikation (DRBD, Restic)
* Basis CI/CD-Pipeline

**Praxis:**

* DockSeed-Cluster ausrollen
* Monitoring & Backup einrichten
* Doku: *„DockSeed MVP Deployment“*

**Hinweis:**
DRBD-Replikation sollte überprüft werden: Status Primary/Secondary, Sync-Zustand und automatisches Failover.

**Praktische Übungen:**

* Verbinde zwei Cluster-Knoten über WireGuard und prüfe Latenz.
* Führe ein automatisiertes Backup eines Containers über Restic aus.

**Troubleshooting:**

* DRBD-Sync hängt → `drbdadm status` prüfen

**Aufräumen:**

* Cluster-Knoten deregistrieren, Netzwerk-Cleanup

---

## Level 7 – DevOps Essentials

**Ziel:**
Ein realistisches Verständnis moderner DevOps-Praxis gewinnen.

**Themen:**

* Helm & GitOps (ArgoCD)
* BuildKit, Kaniko, Image Security (Trivy, Cosign)
* Automatisierte Tests & CI/CD (GitHub Actions)

**Praxis:**

* Eigene Helm-Charts einsetzen
* Pipeline für DockSeed konfigurieren
* `trivy image` in CI-Pipeline integrieren
* Doku: *„Continuous Deployment im Homelab“*

**Hinweis:**
Hier kann Cosign für ein Beispiel-Image eingesetzt werden, um Signierung und Verifikation praktisch zu lernen.

**Praktische Übungen:**

* Erstelle ein Helm-Chart für ein simples Nginx-Deployment.
* Integriere Trivy in eine GitHub Action und dokumentiere die Scan-Ergebnisse.

**Troubleshooting:**

* CI schlägt fehl → YAML-Indentation prüfen, Secrets validieren

**Aufräumen:**

* Alte Container-Images löschen, Workflows deaktivieren

---

## Begleitmodule (parallel zu allen Levels)

### Netzwerk & Security

* VLANs, Bridges, NAT, Routing, DNS
* nftables & Firewalls in Container-Setups
* SSH-Härtung, Schlüsselverwaltung, Fail2Ban
* Zero-Trust & VPN (WireGuard, Tailscale)

**Praxis:** Eigenes isoliertes Netz + VPN-Zugang aufbauen

### Storage & Backup

* Block vs. Object Storage (Ceph, MinIO)
* DRBD, NFS, iSCSI Grundlagen
* Snapshot-Strategien & Datenversionierung
* Backups mit `restic` oder `borg`

**Praxis:** Backup & Restore einer Test-VM oder Container-Volumes

### Observability & Monitoring

* Netdata, Prometheus, Grafana
* Log-Pipelines mit Loki & Promtail
* Health Checks & Alerting

**Praxis:** Mini-Monitoring für K3s oder lokale VMs

---

## Strukturvorschlag im Repo

```bash
learning/
 ├── level-0_kvm-libvirt/
 ├── level-1_fundament/
 ├── level-2_containerd/
 ├── level-3_automation/
 ├── level-4_kubevirt/
 ├── level-5_k3s/
 ├── level-6_dockseed/
 ├── level-7_devops/
 └── begleitmodule/
```

Jeder Level enthält:

* **README.md** – Theorie in Stichpunkten
* **practice.md** – Übungen & Kommandos
* **checklist.md** – Lernziele / Selbsttest
* **review.md** – Reflexion & Notizen
* **troubleshooting.md** – Typische Fehler & Lösungen
* **resources.md** – Kuratierte Lernlinks

---

**Empfohlener Ablauf:**
Starte mit `level-0_kvm-libvirt`, führe alle Übungen durch und dokumentiere.
Steige dann schrittweise weiter auf.
Ziel ist: Systeme verstehen, nicht nur bedienen.

---

TZ=Europe/Berlin | Datum 2025-10-12 17:00 | §lehrplan §virtualisierung §k3s
