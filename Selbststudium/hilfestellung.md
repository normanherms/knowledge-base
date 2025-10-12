# Hilfestellungen zum Selbststudium

Diese Hilfestellungen sind als Leitfaden gedacht, um dich durch jedes Level zu führen, ohne dich mit endloser Theorie zu überfordern. Ziel: Du sollst *verstehen, tun und reflektieren* – nicht nur lesen.

## Es soll Spaß machen kein Krampf werden

---

### Level 0 – KVM & Libvirt (Virtualisierung verstehen)

**Selbststudiums-Hilfe:**

* Beginne mit einem kurzen Video oder Blogbeitrag über KVM vs. VirtualBox, um das Konzept der Hardwarevirtualisierung zu verstehen.
* Installiere `qemu-kvm`, `libvirt-daemon`, `virt-manager` auf einem Testsystem.
* Arbeite zuerst mit `virt-manager`, um visuell zu sehen, was passiert, dann wiederhole die Schritte mit `virsh` und `virt-install`.
* Dokumentiere jeden Schritt in einem Markdown-File (z. B. *erste_vm.md*).

**Lern-Tipp:**
Achte auf die Unterschiede zwischen Host und Gast. Führe `lsmod | grep kvm` aus, um zu prüfen, ob KVM geladen ist.

---

### Level 1 – Fundament (Linux-Isolation)

**Selbststudiums-Hilfe:**

* Lies ein Kapitel oder einen Artikel zu *Linux Namespaces* (z. B. von Red Hat oder Linux Foundation).
* Nutze `unshare`, um systematisch jede Namespace-Art zu testen: `pid`, `net`, `mnt`.
* Erstelle mit `debootstrap` ein Mini-System und chroote hinein, um echte Isolation zu verstehen.

**Lern-Tipp:**
Mach Screenshots oder Notizen zu jedem Experiment (vorher/nachher: `ps`, `ip link`, `mount`). So lernst du Ursache-Wirkung.

---

### Level 2 – containerd & nerdctl

**Selbststudiums-Hilfe:**

* Beginne mit einem Docker-Vergleich: Welche Komponenten entfallen? Lies kurz die containerd-Architektur im offiziellen GitHub-Repo.
* Installiere `containerd` + `nerdctl` und starte einfache Container (`alpine`, `nginx`).
* Wechsle danach in den Rootless-Modus und notiere Unterschiede in den Pfaden unter `/run/user/UID`.

**Lern-Tipp:**
Dokumentiere, welche Befehle *gleich* und welche *anders* als bei Docker sind. So prägst du dir Unterschiede leicht ein.

---

### Level 3 – Infrastruktur-Automation

**Selbststudiums-Hilfe:**

* Sieh dir ein Terraform-Beispiel mit Libvirt an (z. B. aus GitHub-Examples). Starte klein: Eine VM mit fester IP.
* Lies den Abschnitt zu *Cloud-Init User-Data* (YAML-Beispiele). Verstehe den Aufbau: `users`, `packages`, `runcmd`.
* Nutze `ansible --check` und `--diff`, um Änderungen sicher zu testen.

**Lern-Tipp:**
Führe bewusst Fehler ein (z. B. falsches YAML-Indent) und beobachte, wie Terraform/Ansible reagieren.

---

### Level 4 – KubeVirt (Hybrid-Virtualisierung)

**Selbststudiums-Hilfe:**

* Lies die offizielle KubeVirt-Quickstart-Doku.
* Installiere es im K3s-Testcluster (lokal oder in VMs). Beobachte mit `kubectl get pods -n kubevirt`, was gestartet wird.
* Teste `virtctl console` und prüfe Netzwerkverbindungen zu Pods.

**Lern-Tipp:**
Erkläre einem fiktiven Kollegen in eigenen Worten: *Was ist der Unterschied zwischen einem Pod und einer VM in KubeVirt?*

---

### Level 5 – K3s & Orchestrierung

**Selbststudiums-Hilfe:**

* Beginne mit `kubectl explain pod.spec`, um YAML-Felder zu verstehen.
* Führe kleine Deployments durch, überprüfe mit `kubectl get all`.
* Baue erst ein Single-Node-Cluster, dann erweitere auf zwei Nodes.

**Lern-Tipp:**
Nutze `kubectl describe` und `kubectl logs` so oft wie möglich. Debuggen ist 80% des Kubernetes-Alltags.

---

### Level 6 – DockSeed Production

**Selbststudiums-Hilfe:**

* Starte mit Netzaufbau: WireGuard-Tunnel üben (zwei VMs genügen).
* Setze DRBD im Sync-Modus auf und beobachte den Status mit `cat /proc/drbd`.
* Installiere Netdata und analysiere Systemmetriken im Browser.

**Lern-Tipp:**
Mach Screenshots deines Monitoring-Dashboards und erkläre dir selbst, was du siehst. So merkst du, ob du Zusammenhänge verstehst.

---

### Level 7 – DevOps Essentials

**Selbststudiums-Hilfe:**

* Lies eine einfache Helm-Einführung (z. B. DigitalOcean Tutorial).
* Klone ein bestehendes GitHub-Action-Beispiel und führe es aus, um CI/CD live zu sehen.
* Scanne dein eigenes Image mit `trivy image`.

**Lern-Tipp:**
Nutze Checklisten für YAML, Helm und CI: Einmal korrekt aufgebaut, kannst du sie für alle Projekte wiederverwenden.

---

### Begleitmodule

**Netzwerk & Security:**

* Zeichne dein aktuelles Homelab-Netz auf Papier und markiere VLANs, Bridges, Firewalls.
* Baue einen simplen WireGuard-Tunnel zwischen zwei VMs.

**Storage & Backup:**

* Teste `restic` lokal mit einem Dummy-Ordner.
* Übe das Wiederherstellen einer Datei aus einem Snapshot.

**Monitoring:**

* Installiere `netdata` oder `prometheus-node-exporter`.
* Beobachte CPU-, RAM- und Netzwerk-Graphen über Zeit.

---

**Abschluss-Tipp:**
Arbeite nie mehr als ein Level pro Woche. Dokumentiere alles in Markdown und erkläre dir die Schlüsselbegriffe selbst. Wenn du sie jemand anderem *erzählen* könntest, hast du sie verstanden.
