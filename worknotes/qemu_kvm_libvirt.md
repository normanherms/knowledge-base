
# Virtualisierung mit KVM, QEMU und libvirt

## Anmerkung

Dieses Cheatbook basiert auf dem von ChatGPT (GPT-5) begleiteten Lernmodul zur Linux-Virtualisierung
Es dokumentiert die Inhalte und Praxisbeispiele rund um KVM, QEMU und libvirt in komprimierter, nachvollziehbarer Form
Ziel ist ein klarer Überblick über Architektur, Installation und Zusammenspiel der Komponenten

---

## Einführung

Die Linux-Virtualisierung basiert auf einer Kombination mehrerer Komponenten, die sich gegenseitig ergänzen:

**KVM (Kernel-based Virtual Machine)**
Stellt die eigentliche Virtualisierung im Linux-Kernel bereit. Keine Emulation, sondern nutzt Hardware-Virtualisierung (Intel VT-x / AMD-V).

**QEMU (Quick Emulator)**
Führt virtuelle Maschinen aus, emuliert CPU, Geräte und Speicher. In Kombination mit KVM wird echte Hardwarebeschleunigung verwendet.

**libvirt**
Stellt eine einheitliche API und CLI bereit (z. B. `virsh`, `virt-manager`), um verschiedene Hypervisor (QEMU, Xen, Hyper-V, VMWare usw.) zu verwalten. Macht den Hypervisor austauschbar.

**virt-manager**
Grafische Oberfläche zur Verwaltung von libvirt-VMs. Für Desktop- oder Testsysteme gedacht.

---

## Funktionsweise (vereinfacht)

1. **KVM** wird als Kernelmodul geladen (`kvm.ko`, `kvm_intel.ko` oder `kvm_amd.ko`).
2. **QEMU** nutzt KVM über das `/dev/kvm`-Interface, um Hardwarebeschleunigung zu aktivieren.
3. **libvirt** steuert QEMU über eine standardisierte API.
4. **virt-manager** oder `virsh` greifen wiederum auf libvirt zu, um VMs zu starten, stoppen oder verwalten.

---

## Installation (Beispiel: Debian / Ubuntu)

### Mit GUI (z. B. Desktop)

```bash
sudo apt install qemu-system libvirt-daemon-system qemu-utils virt-manager
```

### Ohne GUI (z. B. Server)

```bash
sudo apt install --no-install-recommends qemu-system libvirt-clients \
libvirt-daemon-system qemu-utils dnsmasq-base
```

### Validierung der Umgebung

```bash
sudo virt-host-validate
```

### Benutzerrechte anpassen

Damit der Benutzer VMs ohne `sudo` verwalten kann:

```bash
sudo usermod -aG libvirt $USER
sudo usermod -aG kvm $USER
```

Danach ab- und wieder anmelden.

### Dienst prüfen

```bash
sudo systemctl status libvirtd
```

Wenn der Daemon nicht läuft:

```bash
sudo systemctl enable --now libvirtd
```

---

## Zusätzliche Hinweise

* Das Netzwerk für VMs wird meist durch **dnsmasq** und **bridge-utils** bereitgestellt (Standardnetz: `virbr0`).
* VMs werden standardmäßig unter `/var/lib/libvirt/images/` gespeichert.
* CLI-Werkzeuge:

  * `virsh` (Steuerung über Terminal)
  * `virt-install` (VM-Erstellung per Kommandozeile)
* KVM setzt CPU-Virtualisierung voraus. Prüfen mit:

  ```bash
  lscpu | grep Virtualization
  ```
