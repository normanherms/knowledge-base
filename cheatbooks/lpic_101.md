# LPIC-1 Cheatbook – Teil 101

---

## Anmerkung

Dies ist ein persönliches Cheatbook.
Es dient als Nachschlagewerk für meine eigenen Lerninhalte und erhebt keinen Anspruch auf Vollständigkeit.
Die Inhalte wurden teilweise mit Unterstützung von ChatGPT geglättet und ergänzt.
Auch wenn ich auf Richtigkeit achte, können Fehler enthalten sein.

---

## Einführung

* LPIC-1 besteht aus zwei Prüfungen: 101 und 102.
* Dieses Cheatbook behandelt die **Prüfung 101**.
* Themen: Systemarchitektur, Kernel, Systemstart, Init-Systeme, Dateisysteme und Partitionierung.
* Ziel: Übersicht und Zusammenhänge für praktische Anwendung und Prüfungsvorbereitung.

---

## 1. Systemarchitektur

### Systeminformationen anzeigen

* `uname` → Kernelinformationen anzeigen.

  * `uname -r` → Kernelversion.
  * `uname -m` → Maschinenarchitektur.
  * `uname -a` → Alle Infos.
* `lscpu` → CPU-Infos.
* Manpage zu jedem Befehl: `man uname`

---

## 2. Pseudo-Dateisysteme

### /proc

* Laufzeitinformationen über Kernel und Prozesse.
* Beispiel: `cat /proc/modules`

### /sys

* Enthält Kernelmodule und Hardwareinformationen zur Laufzeit.

### /dev

* Geräteverzeichnis, z. B. `sda` (Festplatte), `sda1` (Partition).

### Weitere Begriffe

* `udev` → verwaltet User-Geräte.
* **Hot Plug** → Gerät wird zur Laufzeit erkannt.
* **Cold Plug** → Gerät muss vor Start angeschlossen sein.
* **D-Bus-System** → Nachrichtenaustausch zwischen Anwendungen.

---

## 3. Kernelmodule

### Module anzeigen & verwalten

* `lsmod` → listet alle geladenen Kernelmodule.
* `modinfo <modul>` → zeigt Infos über Modul.

  * `-a` → Autor.
  * `-d` → Beschreibung.
  * `-l` → Lizenz.
* `modprobe <modul>` → lädt Modul.
* `modprobe -r <modul>` → entlädt Modul.

---

## 4. Hardware

### Hardware anzeigen

* `lspci` → listet PCI-Geräte.
* `lspci -v` → verbose Ausgabe.
* `lsusb` → listet USB-Geräte.
* `lsusb -v` → detailliert.

---

## 5. Systemstart

### Bootprozess (Übersicht)

* BIOS → MBR (Bootloader) → Kernel → initrd/initramfs → init/systemd.
* `systemd` ist der erste gestartete Prozess.
* Kernelmeldungen: `dmesg` zeigt Ring-Buffer an.

---

## 6. Bootloader

### GRUB2

* Bootloader, der Kernel lädt.
* Boot-Menü durch **Shift-Taste** öffnen.
* `e` → Edit-Modus.
* `c` → CLI-Modus.

---

## 7. SysVinit

* Klassische Init-Methode unter `/sbin/init`.
* Konfiguration in `/etc/inittab`.
* Runlevel-Skripte: `/etc/init.d/`.

### Runlevel (klassisch)

| Runlevel | Bedeutung                        |
| -------- | -------------------------------- |
| 0        | Shutdown                         |
| 1        | Single User / Wartung            |
| 2        | Multi-User ohne Netzwerk         |
| 3        | Multi-User mit Netzwerk (Server) |
| 4        | Benutzerdefiniert                |
| 5        | Multi-User mit GUI               |
| 6        | Reboot                           |

---

## 8. Upstart

* Nachfolger von SysVinit.
* Startet Prozesse parallel.
* Rückwärtskompatibel zu SysVinit-Skripten.
* Konfiguration unter `/etc/init/`.

---

## 9. Systemd

* Standard in modernen Distributionen.
* Verwaltet abhängige Dienste.
* Unit-Dateien:

  * `/etc/systemd/system` → lokale Units.
  * `/lib/systemd/system` → systemweite Units.

### Wichtige Befehle

* `systemctl list-units` → aktive Dienste.
* `systemctl status` → Status eines Dienstes.
* `systemctl stop <dienst>` → Dienst stoppen.
* `systemctl start <dienst>` → Dienst starten.
* `systemctl isolate multi-user.target` → Target wechseln.
* `systemctl set-default multi-user.target` → Standard setzen.

### Logs & Journal

* `journalctl` → zeigt alle Systemd-Meldungen.
* `journalctl -k` → zeigt Kernelmeldungen.

---

## 10. Dateisystem nach FHS

| Verzeichnis | Bedeutung                              |
| ----------- | -------------------------------------- |
| `/`         | Root (Wurzelverzeichnis)               |
| `/bin`      | Befehle für alle Benutzer              |
| `/sbin`     | Systembefehle (root)                   |
| `/boot`     | Bootloader-Dateien                     |
| `/dev`      | Gerätedateien                          |
| `/etc`      | Systemkonfigurationen                  |
| `/lib`      | Bibliotheken & Kernelmodule            |
| `/media`    | Mountpoints für Wechselmedien          |
| `/mnt`      | Temporäre Mountpoints                  |
| `/opt`      | Optionale Programme                    |
| `/run`      | Laufzeitdaten                          |
| `/srv`      | Daten für Dienste                      |
| `/tmp`      | Temporäre Dateien                      |
| `/usr`      | Sekundäre Hierarchie (Programme, Doku) |
| `/var`      | Variable Daten (Logs, Cache)           |
| `/home`     | Benutzerverzeichnisse                  |
| `/lib64`    | 64-Bit-spezifische Bibliotheken        |
| `/root`     | Home des Root-Users                    |

---

## 11. Swap

* Swap = Auslagerungsspeicher, wenn RAM voll ist.
* Empfehlung: ca. 50 % des RAM.
* Befehle:

  * `swapon` → Swap aktivieren.
  * `swapoff` → Swap deaktivieren.

---

## 12. Partitionen

### Grundlagen

* Festplatten: `/dev/sda`, `/dev/sdb`, `/dev/nvme0n1` usw.
* Partitionen: `/dev/sda1`, `/dev/sda2`, usw.
* Maximal 4 primäre Partitionen, Rest logisch (beginnend bei `/dev/sda5`).

### Weitere Befehle

* `lsblk` → zeigt Blockdevices.
* `df` → zeigt Speicherbelegung.
* `blkid` → zeigt UUIDs.
* EFI-Partition: FAT32, ESP markiert.

---

## 13. Mounten

* Mounten verbindet ein Dateisystem mit einem Verzeichnisbaum.
* Befehl: `mount`
* hardware wird automatisch von udev eingehängt.
* `mount` listet alle mounts eines systems
