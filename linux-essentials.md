# Linux Essentials Cheatbook

---

## Anmerkung

Dies ist ein persönliches Cheatbook.
Es dient als Nachschlagewerk für meine eigenen Lerninhalte und erhebt keinen Anspruch auf Vollständigkeit.
Die Inhalte wurden teilweise mit Unterstützung von ChatGPT geglättet und ergänzt.
Auch wenn ich auf Richtigkeit achte, können Fehler enthalten sein.

---

## Einführung

* Linux = Betriebssystemkern (Kernel) + Programme.
* Linux ist Open Source und von Unix inspiriert.
* Inhalte: Kernel, Distributionen, Dateisystem, Shell, Netzwerk, Rechteverwaltung.
* Vorteil: Flexibel, stabil, weit verbreitet (Server, Embedded, Cloud).

---

## LPIC 010-160 Linux Essentials (Grundlagen)

### What is Linux

* Linux ist ein Kernel
* Kernel ist das Hirn eines OS
* Der Kernel ist ein Teil des OS
* Um den Kernel herum sind Programme

### Distribution

* Es gibt eine Distro-Familie
* Beispiel: Ubuntu ist Debian-basiert
* Eine Distro basiert oft auf einer anderen
* Größter Unterschied ist die Paketverwaltung

### Historie

* Linus Torvalds hat Linux 1991 programmiert
* Linux war inspiriert von Unix
* Linux ist zusammengesetzt aus Linux und Unix
* Linux enthält keine Unix-Befehle bzw. Unix-Code

### Distro-Kurzübersicht

* Red Hat (Server & Enterprise)
* SUSE (Enterprise, aber auch downloadbar)

### Installationstypen

* Embedded (Built-in)
* Android (Android Inc. bzw. Google)
* Raspberry Pi (Pi OS, basiert auf Debian)
* Cloud Computing (AWS, Google Cloud, Azure)

---

## Abschnitt 1: First Hand-on

* Linux Kernel laden von kernel.org

**Quiz:** 5 von 5

---

### Interessante Software für Linux

* Firefox, Google Chrome, LibreOffice
* Gimp (ähnlich Photoshop)
* Blender (3D-Bearbeitung)
* Audacity (Audio)
* ImageMagick (Image Processing)

### Server Packages

* Apache (Webserver)
* NFS, Samba (Fileserver)
* Domain Controller
* Nextcloud, Owncloud

### Netzwerk

* DHCP (IP-Vergabe)
* DNS

### Programmierung

* C (Speed)
* Python (leicht zu erlernen)
* JavaScript (Webentwicklung)
* Perl
* Java (Portability, Cross-Plattform)
* Shell (Scripting in Shell)
* PHP (Webentwicklung)

#### Begriffe

* Compiled = Source Code zu Standalone machen
* Interpreted = Programm → Ausführung, oft als Scripting Language bezeichnet

---

## Abschnitt 2: Software & Desktop

### Software-Management

* Software wird aus Repositories installiert
* Nutzung von Paketmanagern (z. B. Gnome Software)
* Installationen können per Desktop oder Terminal erfolgen

### Desktop-Komponenten

* Display Manager: GDM, LightDM, SDDM (Login Manager)
* Window Manager: openbox, KWin, Mutter, Xfwm
* Komplettes Environment: KDE Plasma, Gnome, MATE, Cinnamon
* Gnome ist meist Default
* Toolkits: GTK, Qt
* Bibliotheken: erleichtern Programmierung, z. B. Sound abspielen ohne es selbst zu programmieren
* Gnome nutzt GTK, Plasma nutzt Qt

---

## Abschnitt 3: Hands-on

* Linux vom Stick booten (z. B. fedora-project.org)
* Download einer Distro → Media Writer

**Quiz:** 5 von 5

---

## Abschnitt 4: Kommandozeile

### Shell-Beispiele

* zsh
* csh
* ksh
* Standard Bourne Again Shell (bash)

> Alles was man mit einer GUI machen kann, kann man in der Shell auch machen.

### Aufbau Kommandozeile

Prompt-Beispiel:

```bash
zimtadmin@zimtbox:~$
```

* User
* Hostname
* Arbeitsverzeichnis

### Einfache Kommandos

* ls (zeigt das Arbeitsverzeichnis an)
* pwd (zeigt das aktuelle Verzeichnis)
* mkdir (erstellt neue Ordner)
* cd (wechselt Verzeichnisse)
* rm (löschen von Dateien/Ordnern, `-r` für Verzeichnis)
* echo (zeigt das nachfolgende in der Shell)

### Aufbau eines Kommandos (Syntax)

```bash
ls -l Dokumente
```

* Kommando
* Option
* Argument

### Quoting

Beispiel:

```bash
mkdir Meine Notizen
```

* erstellt 1 Ordner „Meine“ und 1 Ordner „Notizen“

```bash
mkdir "Meine Notizen"
```

* erstellt 1 Ordner „Meine Notizen“ (Leerschutz durch Anführungszeichen)

* Backslash (`\`) = Escape-Zeichen, verhindert Interpretation von Leerzeichen

### Variablen

* Beispiel: `echo $HOME` → zeigt das Homeverzeichnis
* Das `$`-Zeichen beschreibt eine Variable
* `" "` doppelte Anführungszeichen werden anders interpretiert als `' '` einfache Anführungszeichen

#### Variablen erstellen

* Beispiel: `NAME="Norman Herms"`
* Anzeigen mit `echo $NAME`
* Eine Variable besteht bis zum Schließen der Shell-Session
* Environment-Variablen anzeigen mit `env`

### Pfade

* Absolute Pfade: beginnen vom Root-Verzeichnis, z. B. `/home/zimtadmin/Bilder`
* Relative Pfade: beziehen sich auf aktuellen Ordner
* Linux-Dateisystem ist baumartig, ähnlich Windows
* Linux ist **case-sensitive** (Groß- und Kleinschreibung beachten)

### Text in Dateien

* `echo "Hello World" > file.txt` (Text überschreiben)
* `echo "Hello World" >> file.txt` (Text anhängen)

#### Kommando-Sheet

* touch (erstellt Dateien)
* env (zeigt Environment-Variablen)
* mv (Datei verschieben)
* cp (Datei kopieren)
* rm (Datei löschen)
* cat (Inhalt einer Datei anzeigen)
* locate (Dateien finden)

---

## Abschnitt 5: Dokumentation

### Man Pages

* `man` = Manual Page eines Kommandos

* Navigation:

  * ↑ oder `33` = nach oben
  * ↓ oder `54` + `7` = nach unten
  * `/` = Suche
  * `q` = Exit
  * `n` = nächstes Suchergebnis

* Kategorien anzeigen: `whatis passwd`

* Weitere Hilfe: `--help`

* Dokumentation online: [https://wiki.archlinux.org](https://wiki.archlinux.org)

* Lokale Docs: `/usr/share/doc` oder README-Dateien

**Quiz:** 5 von 5

---

## Abschnitt 6: Datenmanipulation

### Kompression

* Daten komprimieren spart Speicher
* Durch Entfernen redundanter Daten

#### Archivierung

* `tar` = Archivierung, keine Kompression außer in Kombination mit gzip
* Beispiel: `tar -cf mybackup.tar Documents.bak` (packen)
* `tar -xf mybackup.tar` (entpacken)
* `tar -tvf mybackup.tar` (Inhalt anzeigen)

#### Arten der Komprimierung

* Lossy: Datenverlust möglich
* Lossless: kein Datenverlust
* Beispiel ZIP:

  * `zip -r mybackup.zip Documents.bak`
  * `unzip mybackup.zip`

---

## Abschnitt 7: Datenströme

* 0: stdin (Eingaben vom User)
* 1: stdout (normale Ausgaben)
* 2: stderr (Fehlermeldungen)

Beispiel für Umleitung:

```bash
find . -type f -name issue.net 2>errors.txt
```

* `/dev/null` = Blackhole
* Umleitungen kombinieren mit `2>&1`

---

## Abschnitt 8: grep

* `grep Wort` → Ausgabe mit Wort
* `grep -v Wort` → Ausgabe ohne Wort
* Ausgabe kann gepiped werden (`| grep`)

### Hints

* Kommandos verbinden mit `&&`
* Variablen für Exit Code: `$?`

---

## Abschnitt 9: Bash Scripting

### Basics

* Editor z. B. `nano script.sh`
* Erste Zeile: `#!/bin/bash` (Shebang)
* Beispiel:

```bash
echo "Hello World"
```

* Skripte müssen ausführbar gemacht werden:

```bash
sudo chmod +x script.sh
```

* `sudo` im Script sparsam einsetzen (Sicherheit)

### Hands-on

* Download mit `wget`
* `.tar.gz` entpacken: `tar -xzf file.tar.gz`
* `.gz` entpacken: `gunzip file.tar.gz`
* `.tar` komprimieren: `gzip file.tar`

**Quiz:** 5 von 5

---

## Abschnitt 10: Linux als Betriebssystem

### Enterprise vs. Consumer Linux

* Enterprise Linux: stabil und zuverlässig
* Consumer Linux: aktueller, aber weniger stabil

Beispiele Enterprise Distros:

* Debian
* CentOS
* Ubuntu LTS
* Red Hat
* SUSE

Beispiele Consumer Distros:

* Fedora
* Ubuntu non-LTS
* OpenSUSE
* Rolling Release: Arch Linux, Gentoo, Kali, Parrot OS

---

## Abschnitt 11: Hardware

* Keine Aufzeichnungen vorhanden, Modul wurde aber behandelt

---

## Abschnitt 12: Linux Dateisystem

* Das Dateisystem ist wie ein Baum aufgebaut, startet bei `/`
* Jeder Ordner in Linux hat eine Funktion:

  * `/home` = Benutzerverzeichnis
  * `/etc` = Konfigurationsdateien (systemweit)
  * `/boot` = Bootloader
  * `/opt` = optionale Programme
  * `/dev` = Devices
  * `/root` = Home für den Root-User
  * `/var` = Logs
  * `/usr/bin` = Binaries
  * `/bin` = essentielle Binaries

---

## Abschnitt 13: Netzwerk

* Link Layer: TCP/IP basiert, Kabel oder Funk überträgt Bits
* Network Layer: Routing, IP sorgt für richtige Adresse
* App Layer: Anwendungsschicht (Protokolle, IPv4)
* IPv4 = 32-bit Adresse (4 Nummern, durch Punkte getrennt)
* Subnetting: Netzwerke in kleinere Segmente unterteilen

**Quiz:** 5 von 5

---

## Abschnitt 14: Ressourcen Management

### User und Gruppen

* User-Datenbank: `/etc/passwd`
* Passwortdatei: `/etc/shadow`
* Gruppendatei: `/etc/group`

#### User Management

* User erstellen: `sudo useradd user`
* Passwort ändern: `passwd user` (mit sudo)
* User löschen: `sudo userdel user`

---

## Abschnitt 15: Zugriffsrechte

* Typen: d = Ordner, - = Datei
* Rechte des Users, der Gruppe und andere

```text
drwxr-xr-x
```

* r = lesen
* w = schreiben
* x = ausführen

Sonderzeichen:

* b = block device
* d = directory
* l = link
* s = socket
* c = character device

### Rechte ändern

* Besitzer ändern: `chown`
* Rechte ändern: `chmod`
* Beispiel: `chmod u+rwx Datei`
* Zahlenmethode: rwx = 111 = 7

  * rw- = 110 = 6
  * r-- = 100 = 4

---

## Abschnitt 16: Prozesse & Ressourcen

### Monitoring

* `du -h` = Speicher der Ordner
* `top` = Prozessübersicht
* `uptime` = Uptime & Load Average
* `ps -u` = Prozesse User
* `ps -a` = alle User
* `ps -aux` = alle inkl. Hintergrundprozesse

**Quiz:** 3 von 5

### Speicher

* RAM & Swap prüfen: `free -m`
* Festplatte prüfen: `df -h`

---

## Kursende ✅
