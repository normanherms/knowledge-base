# LPIC-101 Cheatbook

---

## Anmerkung

Dies ist ein persönliches Cheatbook.
Es dient als Nachschlagewerk für meine eigenen Lerninhalte und erhebt keinen Anspruch auf Vollständigkeit.
Die Inhalte wurden teilweise mit Unterstützung von ChatGPT geglättet und ergänzt.
Auch wenn ich auf Richtigkeit achte, können Fehler enthalten sein.

---

## Einführung

* LPIC-1 besteht aus zwei Prüfungen: 101 und 102.
* Themen: Systemarchitektur, Installation, GNU/Linux-Kommandos, Devices, Filesystem, Systemstart und Runlevels.
* Dieses Cheatbook basiert auf meinen handschriftlichen Mitschriften und ist als strukturierte Lernhilfe gedacht.

---

## Thema 101.01 – Systemarchitektur

### Virtuelle Umgebung

* VirtualBox oder VMware zur Simulation verwendet.
* Ubuntu und Fedora wurden als Testsysteme genutzt.

### Systeminformationen anzeigen

* `uname` → Kernel-Informationen anzeigen.

  * `uname -r` → Kernel-Version.
  * `uname -m` → Machine-Type.
  * `uname -a` → Alle Infos.
* `lscpu` → CPU-Informationen.
* Zu jedem Befehl kann die manpage gelesen werden: `man uname`.

---

### Pseudo-Dateisysteme

* `/proc` → nur zur Laufzeit verfügbar, zeigt laufende Prozesse und Kernelmodule.

  * Beispiel: `cat /proc/modules`
* `/sys` → Laufzeitinformationen zu Kernelmodulen und Hardware.
* `/dev` → Geräteverzeichnis, z. B. `sda` (Festplatte), `sda1` (Partition).

#### Weitere Begriffe

* `udev` → verwaltet User-Geräte.
* **Hot Plug** → Gerät, das zur Laufzeit erkannt und verwendet werden kann.
* **Cold Plug** → Gerät, das nur im ausgeschalteten Zustand installiert wird.
* **D-Bus-System** → Anwendung, die Nachrichten zwischen Anwendungen austauscht.

---

## Thema 101.02 – Partitionen und Dateisysteme

### Partitionen

* Festplatten heißen z. B. `/dev/sda`, `/dev/sdb`, `/dev/nvme0n1` usw.
* Partitionen: `/dev/sda1`, `/dev/sda2`, usw.
* Es gibt maximal 4 primäre Partitionen, alle weiteren sind logisch und beginnen z. B. bei `/dev/sda5`.
* Wichtige Befehle:

  * `lsblk` → Blockdevices anzeigen.
  * `df` → Speicherbelegung anzeigen.
  * `blkid` → zeigt UUID (Universal Unique Identifier).
* EFI-Partition ist immer FAT32-formatiert und als ESP markiert.

### Mounten von Dateisystemen

* Befehl: `mount`

---

## Thema 101.03 – Dateisystem nach FHS (Filesystem Hierarchy Standard)

| Verzeichnis | Bedeutung                              |
| ----------- | -------------------------------------- |
| `/`         | Root-Verzeichnis (Wurzel des Systems)  |
| `/bin`      | Befehle für alle User                  |
| `/sbin`     | Systembefehle (root only)              |
| `/boot`     | Bootloader-Dateien                     |
| `/dev`      | Gerätedateien                          |
| `/etc`      | Host-spezifische Konfigurationen       |
| `/lib`      | Dynamische Bibliotheken & Kernelmodule |
| `/media`    | Mountpoint für Wechselmedien           |
| `/mnt`      | Temporäre Mountpoints                  |
| `/opt`      | Optionale Anwendungen                  |
| `/run`      | Laufzeitdaten                          |
| `/srv`      | Daten für Dienste                      |
| `/tmp`      | Temporäre Dateien                      |
| `/usr`      | Sekundäre Hierarchie (Programme, Doku) |
| `/var`      | Variable Daten (Logs, Caches)          |
| `/home`     | Benutzerverzeichnisse                  |
| `/lib64`    | 64-Bit-spezifische Bibliotheken        |
| `/root`     | Root-User-Home                         |

### Swap

* Bereich (Partition oder Datei), in dem Daten ausgelagert werden, die nicht in den RAM passen.
* Empfehlung: ca. 50 % des RAM.
* Befehle:

  * `swapon` → Swap aktivieren.
  * `swapoff` → Swap deaktivieren.

---

## Thema 101.04 – Runlevel und Targets

### Klassische Runlevel (SysVinit)

* 0 → Shutdown
* 1 → Single User / Wartung
* 2 → Multi-User ohne Netzwerk
* 3 → Multi-User mit Netzwerk (Server-Modus)
* 4 → Nicht definiert (frei nutzbar)
* 5 → Multi-User + GUI
* 6 → Reboot

### Systemd Targets

* Systemd ersetzt klassische Runlevel.
* `systemctl isolate` → Ziel wechseln (z. B. `systemctl isolate multi-user.target`).
* `systemctl set-default` → Standard-Target setzen.
* `shutdown` und `reboot` → Fahren Systeme herunter bzw. starten neu.
* Mitteilung an User per `wall`.

```bash
shutdown -r 0:00 "Server wird neu gestartet"
```

---

## Thema 101.05 – Dienste und Systemstart

### SysVinit

* Alte Init-Methode unter `/sbin/init`.
* Konfiguration in `/etc/inittab`.
* Runlevel-Skripte in `/etc/init.d/`.

### Upstart

* Nachfolger von SysVinit.
* Startet unabhängige Prozesse parallel.
* Kompatibel zu SysVinit-Skripten.
* Konfiguration: `/etc/init/`.

### Systemd

* Aktueller Standard in modernen Distributionen.
* Verwaltet abhängige Dienste.
* Unit-Dateien:

  * `/etc/systemd/system` (lokale Units).
  * `/lib/systemd/system` (systemweite Units).
* Wichtige Befehle:

  * `systemctl list-units` → aktive Dienste anzeigen.
  * `systemctl status` → Status anzeigen.
  * `systemctl stop <dienst>` → Dienst stoppen.
  * `systemctl start <dienst>` → Dienst starten.
* Hauptkonfiguration: `/etc/systemd/system.conf`

### Journalctl

* `journalctl` → zeigt alle Systemd-Meldungen.
* `journalctl -k` → zeigt Kernel-Logs.

### Bootloader (GRUB2)

* Shift-Taste während des Bootvorgangs drücken für Menü.
* `e` → Edit-Modus.
* `c` → CLI-Modus.

---

## Thema 101.06 – Kernelmodule

### Module anzeigen & verwalten

* `lsmod` → listet aktive Kernelmodule.
* `modinfo <modul>` → zeigt Informationen über Modul.
* `modprobe` → Modul laden.
* `modprobe -r` → Modul entladen.
* `modinfo -a` → zeigt Autor.
* `modinfo -d` → Beschreibung.
* `modinfo -l` → Lizenz.

### Hardware anzeigen

* `lspci` → zeigt PCI-Geräte.
* `lspci -v` → verbose.
* `lsusb` → zeigt USB-Geräte.
* `lsusb -v` → verbose.

---

## Thema 101.07 – Systemstartprozess

### Bootprozess (Übersicht)

* BIOS → MBR (Bootloader) → Kernel → initrd/initramfs → init/systemd.
* Systemd ist der erste Prozess, der gestartet wird, und startet alle weiteren Prozesse.
* Kernel-Meldungen können über `dmesg` gelesen werden.

---

✅ **Ende von LPIC-1 101 Mitschriften (Teil 1)**
