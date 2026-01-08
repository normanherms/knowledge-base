# 🧩 IT-Begriffsliste nach Themen (aktualisiert)

## Betriebssysteme & Tools

- Alpine (Linux)
- Azure
- Bootstrap
- CIM
- Dumpen
- ESX
- Gnome Evolution
- Greenshot
- LDAP
- Lease
- Lolcat
- On Premise
- RoyalTS
- Salt
- Snap
- WSL
- msmtp

## Cloud & Plattformen

- Azure
- Sovereign Cloud Stack

## Cluster & HPC

- Grid Engine
- Torque

## Hardware & Systeme

- Blade Node

## Netzwerk & Protokolle

- Backplane
- Coturn
- DMARC
- DMZ
- DMZ hinter FritzBox
- DSCP
- FDR Infiniband
- IOStat
- Jump Host
- MPLS
- NFS
- NetScaler
- Network Stack
- OSI
- Perimeter
- RDMA
- RDP
- S3 Storage
- SAS
- SATA
- SD-WAN
- STUN
- TURN
- Through-Kommando
- Vesus Reporting
- Witnesser
- iLOs

## Planung & Konzepte

- Domain Controller
- Exposed Host
- Fabric
- Greenfield

## Security & Angriffstechniken

- Admin Tiering
- CVEs
- DMARC
- Deadlock
- HashiCorp Vault
- Idempotent
- Lateral Movement
- Log4Shell (Log4j)
- NIST 2
- NTLM Replay
- Oquotes (verworfen)
- PrintNightmare
- Provisionierung
- Quotes
- S/MIME
- SLA
- SQUIT (IRC)
- Stack Buffer Overflow
- Stepping Stone
- Supply Chain
- Tiebreaker
- Webshell
- XenServer

## Sonstiges

- Blade Node
- CIM
- Grid Engine
- NIST 2
- NVMe
- SLA
- Through-Kommando
- Torque
- ejabberd

## Storage & Filesysteme

- 3 Par
- 3PA (HP)
- BeeGFS
- Ceph
- Data Core
- Data Domain
- Data Shuffling
- DataCore
- Dedup
- Fabric
- MSA
- MergerFS
- NVMe
- Pooling
- Quorum Witness
- Readintensiv SSD

## Virtualisierung & Container

- Citrix
- CloudPBX
- Hypervisor
- ISA Server
- Jabber Server
- MinIO
- PVE (Proxmox VE)
- Redis
- SD-WAN
- SINA Workstation
- Simple Mail Transfer Protocol
- Slurm Controller
- Slurmctld
- SnapRAID
- ejabberd

---

## 🖥️ Betriebssysteme & Tools

---

### 🔹 Alpine (Linux)

**Kurze Erklärung:**
**Alpine Linux** ist ein ultraleichtes, sicherheitsorientiertes Linux, das vor allem in Containern (z. B. Docker) beliebt ist. Es nutzt **musl libc** und **BusyBox**, um auf ein Minimum reduziert zu sein – ohne Ballast.

**Einfach gesagt:**
Alpine ist das Diät-Linux: klein, schnell, sicher – perfekt für minimalistische Nerds und Docker-Fans.

**Beispiel:**
Viele Docker-Images wie `nginx:alpine` sparen Speicherplatz und Startzeit, weil Alpine nur 5 MB wiegt.

**🧠 Merksatz:**
> „Alpine – Linux mit Sixpack für deinen Container.“

**🔗 Quelle:**
[https://alpinelinux.org/](https://alpinelinux.org/)

---

### 🔹 Bootstrap

**Kurze Erklärung:**
**Bootstrap** ist ein beliebtes Frontend-Framework zum schnellen Bauen von responsiven Webseiten. Entwickelt von Twitter, basiert auf HTML, CSS und JavaScript.

**Einfach gesagt:**
Bootstrap ist wie ein Baukasten für Webseiten – mit hübschen Knöpfen, Spaltenraster und Mobil-Design out of the box.

**Beispiel:**
Statt mühsam ein Grid-System zu basteln, sagst du einfach `class="col-md-6"` – und Bootstrap kümmert sich um den Rest.

**🧠 Merksatz:**
> „Mit Bootstrap sieht sogar deine erste Webseite aus wie aus dem 21. Jahrhundert.“

**🔗 Quelle:**
[https://getbootstrap.com/](https://getbootstrap.com/)

---

### 🔹 CIM (Common Information Model)

**Kurze Erklärung:**
**CIM** ist ein Standard zur Verwaltung von IT-Komponenten in Netzwerken. Es beschreibt Geräte, Services und Zustände einheitlich – wie ein Lexikon für Admins.

**Einfach gesagt:**
CIM sagt: „Nenn mir deinen Drucker, deine CPU und deinen Plattenplatz – und zwar überall gleich!“

**Beispiel:**
Systeme wie Microsoft WMI basieren auf CIM, um Hardware-Infos in einer Sprache abzurufen.

**🧠 Merksatz:**
> „CIM – Wenn sich Server, Switch und Drucker endlich verstehen.“

**🔗 Quelle:**
[https://de.wikipedia.org/wiki/Common_Information_Model](https://de.wikipedia.org/wiki/Common_Information_Model)

---

### 🔹 Dumpen

**Kurze Erklärung:**
**Dumpen** heißt in der IT „etwas auslesen und abspeichern“. Das können Speicherinhalte, Festplatten, Prozesse oder Datenbanken sein – oft zwecks Forensik oder Backup.

**Einfach gesagt:**
Dumpen ist wie „Speicher rausziehen und abheften“ – nur digital und manchmal etwas illegal, je nach Kontext.

**Beispiel:**
Ein RAM-Dump nach einem Hack zeigt, welche Passwörter oder Keys im Speicher lagen.

**🧠 Merksatz:**
> „Was du dumpst, das hast du – ob legal oder nicht.“

**🔗 Quelle:**
[https://de.wikipedia.org/wiki/Dump_(Datenverarbeitung)](https://de.wikipedia.org/wiki/Dump_(Datenverarbeitung))

---

### 🔹 ESX (VMware ESXi)

**Kurze Erklärung:**
**VMware ESX/ESXi** ist ein Hypervisor – also ein minimales Betriebssystem, das virtuelle Maschinen direkt auf der Hardware betreibt (Bare-Metal).

**Einfach gesagt:**
ESXi ist wie ein Hotelmanager, der viele Betriebssysteme auf einer Maschine unterbringt – effizient, aber mit Lizenzkosten.

**Beispiel:**
In einem Serverraum läuft ein ESXi-Host mit 10 VMs: Linux, Windows, Firewall, Mailserver – alles auf einer Blechkiste.

**🧠 Merksatz:**
> „Mit ESX laufen zehn Server auf einem – wie in einer WG, aber ohne Pizza-Streit.“

**🔗 Quelle:**
[https://www.vmware.com/de/topics/glossary/content/hypervisor.html](https://www.vmware.com/de/topics/glossary/content/hypervisor.html)

---

### 🔹 Gnome Evolution

**Kurze Erklärung:**
**Evolution** ist der Groupware-Client des Gnome-Desktops – ein All-in-One für E-Mail, Kalender, Kontakte und Aufgaben.

**Einfach gesagt:**
Outlook für Linux – mit weniger Glitzer, aber Open Source und ohne nervige Clippy-Vibes.

**Beispiel:**
Viele Linux-Nutzer setzen Evolution für ihre Firmen-Exchange-Postfächer ein – läuft solide, wenn’s einmal konfiguriert ist.

**🧠 Merksatz:**
> „Evolution – die Gnome-Antwort auf Outlook, nur mit Bart.“

**🔗 Quelle:**
[https://wiki.gnome.org/Apps/Evolution](https://wiki.gnome.org/Apps/Evolution)

---

### 🔹 Greenshot

**Kurze Erklärung:**
**Greenshot** ist ein leichtes Screenshot-Tool für Windows mit vielen nützlichen Extras: Anmerkungen, Markierungen, Uploads.

**Einfach gesagt:**
Greenshot ist wie Snipping Tool – nur auf Koffein.

**Beispiel:**
Du machst einen Screenshot vom Fehlerfenster, markierst den Fehler mit einem Pfeil – und schickst ihn direkt per E-Mail.

**🧠 Merksatz:**
> „Greenshot – dein Screenshot, nur mit Superkräften.“

**🔗 Quelle:**
[https://getgreenshot.org/](https://getgreenshot.org/)

---

### 🔹 LDAP (Lightweight Directory Access Protocol)

**Kurze Erklärung:**
**LDAP** ist ein Protokoll zur Abfrage und Pflege von Verzeichnisdiensten, etwa Benutzerkonten in großen Netzwerken (Active Directory & Co.).

**Einfach gesagt:**
LDAP ist das Adressbuch für alles – mit Passwortabfrage.

**Beispiel:**
Wenn du dich im Intranet einloggst, fragt der Server per LDAP: „Gibt’s den User überhaupt – und kennt er das Passwort?“

**🧠 Merksatz:**
> „LDAP – der stille Türsteher deiner Firmen-IT.“

**🔗 Quelle:**
[https://ldap.com/](https://ldap.com/)

---

### 🔹 Lease

**Kurze Erklärung:**
In Netzwerken beschreibt ein **Lease** die Zeitspanne, wie lange ein Gerät eine zugewiesene IP-Adresse vom DHCP-Server behalten darf.

**Einfach gesagt:**
Ein Lease ist wie ein Mietvertrag für deine IP-Adresse – zeitlich befristet.

**Beispiel:**
Dein Laptop bekommt vom DHCP eine IP für 24 h. Danach wird neu verhandelt.

**🧠 Merksatz:**
> „IP auf Zeit – mit Lease hast du WLAN-Mietrecht.“

**🔗 Quelle:**
[https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol)

---

### 🔹 Lolcat

**Kurze Erklärung:**
**Lolcat** ist ein Unix-Tool, das Textausgaben mit Regenbogenfarben versieht. Total sinnlos – und deswegen so großartig.

**Einfach gesagt:**
Terminal-Ausgabe in Pride-Modus. Für alle, die Logs lieber bunt mögen.

**Beispiel:**
`echo "Hallo Welt" | lolcat` zaubert dir bunte Buchstaben auf den Bildschirm.

**🧠 Merksatz:**
> „Lolcat – weil Logs in Grau einfach zu traurig sind.“

**🔗 Quelle:**
[https://github.com/busyloop/lolcat](https://github.com/busyloop/lolcat)

---

### 🔹 On Premise

**Kurze Erklärung:**
**On Premise** bedeutet: Die IT läuft **nicht** in der Cloud, sondern im eigenen Rechenzentrum, Keller oder 19-Zoll-Rack.

**Einfach gesagt:**
On Prem ist wie „selbst kochen statt Lieferdienst“ – mehr Kontrolle, aber auch mehr Abwasch.

**Beispiel:**
Eine Firma betreibt ihre Server für E-Mail, Datenbanken und VPNs komplett im eigenen Haus – ohne AWS oder Azure.

**🧠 Merksatz:**
> „On Prem – IT zum Anfassen, mit Kabelsalat inklusive.“

**🔗 Quelle:**
[https://www.itwissen.info/on-premise-On-Prem.html](https://www.itwissen.info/on-premise-On-Prem.html)

---

### 🔹 RoyalTS

**Kurze Erklärung:**
**RoyalTS** ist ein Remote-Management-Tool, mit dem Admins verschiedene Verbindungen (RDP, SSH, VNC usw.) in einer Oberfläche verwalten.

**Einfach gesagt:**
RoyalTS ist wie ein Werkzeugkoffer für Admins – alles drin, alles aufklappbar.

**Beispiel:**
Du klickst auf einen Server, öffnest per RDP die Konsole und per SSH die Logs – alles in Tabs in einer App.

**🧠 Merksatz:**
> „RoyalTS – weil Admins nicht 10 Fenster brauchen, sondern eins mit Stil.“

**🔗 Quelle:**
[https://www.royalapps.com/ts/welcome](https://www.royalapps.com/ts/welcome)

---

### 🔹 Salt (SaltStack)

**Kurze Erklärung:**
**Salt** ist ein Open-Source-Automatisierungstool zur Konfigurationsverwaltung und Orchestrierung – ähnlich wie Ansible oder Puppet.

**Einfach gesagt:**
Mit Salt kannst du hunderte Server gleichzeitig steuern – wie ein Admin mit Zauberstab.

**Beispiel:**
Ein Befehl, und alle Server bekommen das gleiche Update – synchron und sauber dokumentiert.

**🧠 Merksatz:**
> „Salt – der IT-Zauber, bei dem ein Befehl alles regelt.“

**🔗 Quelle:**
[https://saltproject.io/](https://saltproject.io/)

---

### 🔹 Snap

**Kurze Erklärung:**
**Snap** ist ein Paketformat von Canonical (Ubuntu), das Apps containerisiert mit allen Abhängigkeiten ausliefert – für alle Linux-Distributionen.

**Einfach gesagt:**
Snap ist wie eine Bento-Box: Programm und Beilagen in einem Paket.

**Beispiel:**
`sudo snap install spotify` bringt dir Spotify inklusive aller benötigten Bibliotheken – isoliert vom Rest.

**🧠 Merksatz:**
> „Snap – wenn dein Linux-Paket mehr kann als nur passen.“

**🔗 Quelle:**
[https://snapcraft.io/](https://snapcraft.io/)

---

### 🔹 WSL (Windows Subsystem for Linux)

**Kurze Erklärung:**
**WSL** erlaubt dir, unter Windows eine Linux-Umgebung zu starten – direkt im Terminal, ohne VM oder Dual-Boot.

**Einfach gesagt:**
WSL ist Linux für Windows-Klicker – Terminalspaß ohne Reboot.

**Beispiel:**
Du entwickelst ein Bash-Skript unter Ubuntu – und das ganz ohne dein Windows zu verlassen.

**🧠 Merksatz:**
> „WSL – der Tunnel zwischen PowerShell und Bash.“

**🔗 Quelle:**
[https://learn.microsoft.com/de-de/windows/wsl/](https://learn.microsoft.com/de-de/windows/wsl/)

---

### 🔹 msmtp

**Kurze Erklärung:**
**msmtp** ist ein minimalistisches SMTP-Client-Tool, das E-Mails über externe Mailserver (z. B. Gmail) versenden kann – ideal für Skripte und Server.

**Einfach gesagt:**
msmtp ist der stille Postbote für deine Cronjobs.

**Beispiel:**
Dein Server crasht? Ein Bash-Skript mit `msmtp` informiert dich per Mail.

**🧠 Merksatz:**
> „msmtp – der stille Held im Hintergrund deiner Logs.“

**🔗 Quelle:**
[https://marlam.de/msmtp/](https://marlam.de/msmtp/)

## ☁️ Cloud & Plattformen

---

### 🔹 Azure1

**Kurze Erklärung:**
**Microsoft Azure** ist eine riesige Cloud-Plattform mit allem von VMs über Datenbanken bis hin zu KI. Denk an Amazon AWS – nur in Blau und mit Office-Attitüde.

**Einfach gesagt:**
Azure ist wie ein Rechenzentrum im Himmel, gemietet bei Microsoft. Nur mit mehr Menüpunkten als eine deutsche Verwaltung.

**Beispiel:**
Du kannst eine Ubuntu-VM, SQL-Datenbank und eine KI-API mit drei Klicks in Azure starten – und mit zehn Klicks wieder löschen.

**🧠 Merksatz:**
> „Azure: Die Cloud, in der sogar Excel ein Zuhause hat.“

**🔗 Quelle:**
[https://azure.microsoft.com/de-de/resources/cloud-computing-dictionary/what-is-azure](https://azure.microsoft.com/de-de/resources/cloud-computing-dictionary/what-is-azure)

---

### 🔹 Sovereign Cloud Stack (SCS)

**Kurze Erklärung:**
Der **Sovereign Cloud Stack (SCS)** ist ein Open-Source-Projekt, das eine vollständig **souveräne europäische Cloud-Infrastruktur** ermöglichen will – unabhängig von US-Anbietern. Basis: OpenStack, Kubernetes und Co.

**Einfach gesagt:**
SCS ist die europäische Antwort auf AWS & Azure – nur mit Datenschutz und Open-Source-DNA.

**Beispiel:**
Ein deutscher Hoster betreibt mit SCS eine eigene Cloud-Infrastruktur – DSGVO-konform, modular und unabhängig.

**🧠 Merksatz:**
> „SCS – die Cloud mit EU-Pass und Datenschutzschleife.“

**🔗 Quelle:**
[https://scs.community](https://scs.community)

---

## 🖧 Cluster & HPC

---

### 🔹 Grid Engine

**Kurze Erklärung:**
**Grid Engine** ist ein Job-Management-System für Rechencluster. Es verteilt rechenintensive Aufgaben automatisch auf verfügbare Knoten – häufig im wissenschaftlichen Umfeld genutzt.

**Einfach gesagt:**
Grid Engine ist der Butler deines Rechenclusters – er weiß, welcher Knoten gerade frei ist, und reicht den Job dorthin weiter.

**Beispiel:**
Ein Bioinformatik-Projekt nutzt Grid Engine, um Genomdaten auf 100 Knoten gleichzeitig zu analysieren.

**🧠 Merksatz:**
> „Grid Engine – damit Jobs nicht Schlange stehen müssen.“

**🔗 Quelle:**
[https://en.wikipedia.org/wiki/Oracle_Grid_Engine](https://en.wikipedia.org/wiki/Oracle_Grid_Engine)

---

### 🔹 Torque

**Kurze Erklärung:**
**Torque** ist ein weiteres Batch-System für Hochleistungsrechner (HPC). Es basiert auf OpenPBS und hilft beim Verwalten und Planen von Rechenjobs in Clustern.

**Einfach gesagt:**
Torque ist wie ein Ticketsystem für Supercomputer – du reichst einen Job ein, und Torque macht den Rest.

**Beispiel:**
Ein Physik-Labor nutzt Torque, um Simulationsjobs strukturiert über einen Cluster zu verteilen.

**🧠 Merksatz:**
> „Torque – der Dispatcher für deine Rechenmonster.“

**🔗 Quelle:**
[https://adaptivecomputing.com/cherry-services/torque-resource-manager/](https://adaptivecomputing.com/cherry-services/torque-resource-manager/)

---

## 🧱 Hardware & Systeme

---

### 🔹 Blade Node

**Kurze Erklärung:**
Ein **Blade Node** ist ein einzelnes, modulares Server-Modul (Blade), das in einem Blade-Gehäuse („Chassis“) steckt. Viele Nodes teilen sich dabei Stromversorgung, Lüftung und Netzwerk – spart Platz und Energie.

**Einfach gesagt:**
Blade Nodes sind wie Server in der Schublade – viele schlanke Rechner in einem kompakten Rack.

**Beispiel:**
Ein Rechenzentrum betreibt ein Blade-Chassis mit 16 Blade Nodes – jeder mit eigenem Prozessor und RAM, aber gemeinsamer Infrastruktur.

**🧠 Merksatz:**
> „Blade Node – der Server im Slimfit-Anzug.“

**🔗 Quelle:**
[https://de.wikipedia.org/wiki/Blade-Server](https://de.wikipedia.org/wiki/Blade-Server)

## 🌐 Netzwerk & Protokolle

---

### 🔹 Backplane

**Kurze Erklärung:**
Die **Backplane** ist die zentrale Verbindungseinheit in einem Server oder Switch, über die Module, Slots oder Ports kommunizieren – quasi das Rückgrat der Hardware.

**Einfach gesagt:**
Die Backplane ist wie der Bus im Schulhof: Sie verbindet alle Kinder (Karten, Ports) miteinander.

**Beispiel:**
Ein Switch mit 48 Ports hat eine interne 1 Tbps-Backplane – damit nicht alles beim Kopieren in die Knie geht.

**🧠 Merksatz:**
> „Backplane – der Drahtzieher hinter den Steckkarten.“

**🔗 Quelle:**
[https://de.wikipedia.org/wiki/Backplane](https://de.wikipedia.org/wiki/Backplane)

---

### 🔹 Coturn

**Kurze Erklärung:**
**Coturn** ist ein Open-Source-STUN/TURN-Server, der bei WebRTC-Anwendungen hilft, Clients trotz NAT/Firewall zu verbinden.

**Einfach gesagt:**
Coturn ist der Vermittler, wenn zwei Geräte hinter Routern miteinander sprechen wollen – z. B. für Videochats.

**Beispiel:**
Deine Peer-to-Peer-App will direkt kommunizieren, aber beide Nutzer sind hinter einer FritzBox – Coturn hilft, die Verbindung trotzdem aufzubauen.

**🧠 Merksatz:**
> „Coturn – macht P2P möglich, wo Firewalls sonst Nein sagen.“

**🔗 Quelle:**
[https://github.com/coturn/coturn](https://github.com/coturn/coturn)

---

### 🔹 DMARC (Domain-based Message Authentication, Reporting and Conformance)

**Kurze Erklärung:**
**DMARC** ist ein E-Mail-Sicherheitsstandard, der Spoofing erkennt und verhindert. Er baut auf SPF und DKIM auf.

**Einfach gesagt:**
DMARC fragt: „Ist diese Mail wirklich von @beispiel.de – oder tut nur so?“

**Beispiel:**
Mit DMARC verhinderst du, dass Spammer über deine Domain Mails verschicken – auch wenn sie nicht autorisiert sind.

**🧠 Merksatz:**
> „DMARC – der Türsteher deiner E-Mail-Domain.“

**🔗 Quelle:**
[https://dmarc.org/](https://dmarc.org/)

---

### 🔹 DMZ (Demilitarisierte Zone)

**Kurze Erklärung:**
Die **DMZ** ist ein Netzwerkbereich zwischen Internet und internem LAN, in dem öffentlich erreichbare Dienste (z. B. Webserver) betrieben werden – abgesichert, aber getrennt.

**Einfach gesagt:**
DMZ ist wie der Hausflur: Besucher dürfen rein, aber nicht ins Wohnzimmer.

**Beispiel:**
Ein Mailserver in der DMZ empfängt Mails aus dem Internet, leitet sie aber nur kontrolliert ins LAN weiter.

**🧠 Merksatz:**
> „DMZ – die digitale Pufferzone für deine Server.“

**🔗 Quelle:**
[https://de.wikipedia.org/wiki/Demilitarisierte_Zone_(Informatik)](https://de.wikipedia.org/wiki/Demilitarisierte_Zone_(Informatik))

---

### 🔹 DMZ hinter FritzBox

**Kurze Erklärung:**
Viele Heimrouter wie die **FritzBox** bieten keine echte DMZ, sondern nur eine „Exposed Host“-Funktion – nicht dasselbe! Das Gerät wird ungeschützt dem Internet ausgesetzt.

**Einfach gesagt:**
„DMZ“ bei der FritzBox heißt: Alles an einen Host weiterleiten – wie ein offenes Fenster ohne Gitter.

**Beispiel:**
Ein Raspberry Pi als „Exposed Host“ bekommt alle Ports der FritzBox – das ist keine echte DMZ, sondern ein Sicherheitsrisiko.

**🧠 Merksatz:**
> „FritzBox-DMZ ist keine Zone – das ist ein Fall für die Feuerwehr.“

**🔗 Quelle:**
[https://avm.de/service/fritzbox/fritzbox-7590/wissensdatenbank/publication/show/22_FRITZ-Box-als-DSL-Router-einrichten-und-Internetzugang-einrichten/](https://avm.de/service/fritzbox/fritzbox-7590/wissensdatenbank/publication/show/22_FRITZ-Box-als-DSL-Router-einrichten-und-Internetzugang-einrichten/)

---

### 🔹 DSCP (Differentiated Services Code Point)

**Kurze Erklärung:**
**DSCP** ist ein Bitfeld im IP-Header, das zur **Qualitätssteuerung** (QoS) im Netzwerk dient. Es hilft, Datenverkehr zu priorisieren – z. B. VoIP vor Datei-Downloads.

**Einfach gesagt:**
DSCP ist wie ein VIP-Stempel für deine Datenpakete.

**Beispiel:**
Ein Netzwerkadmin markiert VoIP-Pakete mit hohem DSCP-Wert – damit sie bevorzugt behandelt werden und nicht ruckeln.

**🧠 Merksatz:**
> „DSCP – damit Voice nicht verhungert, wenn Download-Berge rollen.“

**🔗 Quelle:**
[https://en.wikipedia.org/wiki/Differentiated_services](https://en.wikipedia.org/wiki/Differentiated_services)

---

### 🔹 FDR Infiniband

**Kurze Erklärung:**
**FDR (Fourteen Data Rate)** ist eine Infiniband-Generation mit 56 Gbit/s, genutzt in Hochleistungs-Clustern (HPC). Extrem niedrige Latenzen, sehr hohe Bandbreite.

**Einfach gesagt:**
FDR ist das Ferrari-Netzwerk für Supercomputer.

**Beispiel:**
Ein HPC-Cluster überträgt riesige Simulationsdaten in Mikrosekunden – dank FDR Infiniband.

**🧠 Merksatz:**
> „FDR – Full Data Rage für Rechenmonster.“

**🔗 Quelle:**
[https://en.wikipedia.org/wiki/InfiniBand](https://en.wikipedia.org/wiki/InfiniBand)

---

### 🔹 IOStat

**Kurze Erklärung:**
**iostat** ist ein Kommandozeilentool zur Anzeige von **CPU- und I/O-Auslastung** auf Linux- und Unix-Systemen. Ideal für Performance-Analysen.

**Einfach gesagt:**
Mit iostat siehst du, ob dein Server wegen CPU, Platte oder I/O langsam ist – schwarz auf weiß.

**Beispiel:**
Langsame App? `iostat -x 1` zeigt dir live, ob eine Platte am Limit ist.

**🧠 Merksatz:**
> „IOStat – dein Lügendetektor fürs Storage-Drama.“

**🔗 Quelle:**
[https://linux.die.net/man/1/iostat](https://linux.die.net/man/1/iostat)

---

### 🔹 Jump Host

**Kurze Erklärung:**
Ein **Jump Host** (auch Bastion Host genannt) ist ein vorgeschalteter Server, über den sich Admins in ein internes Netzwerk einloggen – wie ein kontrollierter Zugangspunkt.

**Einfach gesagt:**
Ein Jump Host ist das Schleusenhäuschen – du musst durch ihn, bevor du zu den „richtigen“ Servern darfst.

**Beispiel:**
Admins verbinden sich per SSH auf den Jump Host – und von dort weiter in die abgesicherten Systeme.

**🧠 Merksatz:**
> „Jump Host – der Bodyguard vorm Serverraum.“

**🔗 Quelle:**
[https://de.wikipedia.org/wiki/Bastion_Host](https://de.wikipedia.org/wiki/Bastion_Host)

---

### 🔹 MPLS (Multiprotocol Label Switching)

**Kurze Erklärung:**
**MPLS** ist eine Technik zur schnellen Weiterleitung von Datenpaketen durch das Netz – nicht anhand von IPs, sondern über Labels. Häufig in Unternehmensnetzen.

**Einfach gesagt:**
MPLS ist wie eine Express-Straße mit festen Fahrspuren – kein Stau, keine Umwege.

**Beispiel:**
Ein Unternehmen verbindet seine Standorte mit MPLS-Leitungen – für stabile Verbindungen und garantierte Qualität.

**🧠 Merksatz:**
> „MPLS – der VIP-Bus für deine Datenpakete.“

**🔗 Quelle:**
[https://en.wikipedia.org/wiki/Multiprotocol_Label_Switching](https://en.wikipedia.org/wiki/Multiprotocol_Label_Switching)

---

### 🔹 NFS (Network File System)

**Kurze Erklärung:**
**NFS** ist ein Protokoll, mit dem ein Rechner über das Netzwerk auf Dateisysteme eines anderen zugreift – als wären sie lokal.

**Einfach gesagt:**
NFS ist wie ein Netzlaufwerk – nur von Linux, für Linux.

**Beispiel:**
Ein Raspberry Pi mountet `/media/nas` via NFS von einem zentralen Server.

**🧠 Merksatz:**
> „NFS – das WLAN-Kabel zur Festplatte im Nebenraum.“

**🔗 Quelle:**
[https://wiki.ubuntuusers.de/NFS/](https://wiki.ubuntuusers.de/NFS/)

---

### 🔹 NetScaler

**Kurze Erklärung:**
**NetScaler** (Citrix ADC) ist ein Load Balancer, der zusätzlich auch Sicherheitsfunktionen wie SSL-Offloading, App-Firewall und Traffic-Optimierung bietet.

**Einfach gesagt:**
NetScaler ist der smarte Türsteher vorm Webserver – regelt den Andrang und prüft auf böse Absichten.

**Beispiel:**
Ein Unternehmen nutzt NetScaler, um Webanfragen auf mehrere Backend-Server zu verteilen – mit HTTPS-Entschlüsselung.

**🧠 Merksatz:**
> „NetScaler – der IT-Verkehrspolizist mit IQ 130.“

**🔗 Quelle:**
[https://www.citrix.com/de-de/products/citrix-adc/](https://www.citrix.com/de-de/products/citrix-adc/)

---

### 🔹 Network Stack

**Kurze Erklärung:**
Der **Network Stack** ist die Sammlung aller Protokolle, die zusammen das Funktionieren der Netzwerkkommunikation ermöglichen – von Hardware bis Anwendungsebene.

**Einfach gesagt:**
Der Stack ist wie ein Lasagne-Turm – unten Ethernet, oben HTTP, dazwischen TCP/IP und Co.

**Beispiel:**
Bei einem Verbindungsfehler prüfst du: „Ist es DNS, ist es Routing, ist es Layer 8?“

**🧠 Merksatz:**
> „Ohne Stack kein Netz – und ohne Netz kein Kaffee.“

**🔗 Quelle:**
[https://en.wikipedia.org/wiki/Protocol_stack](https://en.wikipedia.org/wiki/Protocol_stack)

---

### 🔹 OSI-Modell

**Kurze Erklärung:**
Das **OSI-Modell** beschreibt in 7 Schichten, wie Daten durch ein Netzwerk wandern – von der App bis zur Leitung.

**Einfach gesagt:**
OSI ist wie eine Postkette: Einer schreibt, einer kuvertiert, einer stempelt – bis die Nachricht auf Reise geht.

**Beispiel:**
Beim Troubleshooting prüfst du Schicht für Schicht: „Liegt's an TCP, an der IP oder am Kabel?“

**🧠 Merksatz:**
> „OSI – Ordnung schafft Infos.“

**🔗 Quelle:**
[https://de.wikipedia.org/wiki/OSI-Modell](https://de.wikipedia.org/wiki/OSI-Modell)

---

### 🔹 Perimeter (Security)

**Kurze Erklärung:**
**Perimeter** meint in der IT-Sicherheit die äußere Schutzgrenze eines Netzwerks – meist durch Firewalls, Gateways und Regeln definiert.

**Einfach gesagt:**
Der Perimeter ist wie der Gartenzaun – nur digital und mit IDS statt Gartenzwerg.

**Beispiel:**
Die Firewall trennt das Internet (unsicher) vom internen Netz (vertraulich) – klassischer Perimeterschutz.

**🧠 Merksatz:**
> „Perimeter – wo das Netzwerk aufhört und die Angreifer warten.“

**🔗 Quelle:**
[https://www.kaspersky.de/resource-center/definitions/what-is-network-perimeter](https://www.kaspersky.de/resource-center/definitions/what-is-network-perimeter)

---

### 🔹 RDMA (Remote Direct Memory Access)

**Kurze Erklärung:**
**RDMA** ermöglicht extrem schnellen Datenaustausch zwischen Servern – direkt zwischen Arbeitsspeichern, ohne CPU-Last.

**Einfach gesagt:**
RDMA ist wie eine Express-Lieferung direkt ins RAM – kein Zwischenstopp bei der CPU.

**Beispiel:**
Hochleistungsdatenbanken nutzen RDMA über Infiniband oder RoCE, um Zugriffszeiten zu minimieren.

**🧠 Merksatz:**
> „RDMA – Teleportation für Datenpakete.“

**🔗 Quelle:**
[https://en.wikipedia.org/wiki/Remote_direct_memory_access](https://en.wikipedia.org/wiki/Remote_direct_memory_access)

---

### 🔹 RDP (Remote Desktop Protocol)

**Kurze Erklärung:**
**RDP** ist Microsofts Protokoll für grafischen Fernzugriff – damit kannst du einen Windows-Desktop remote steuern, als säßest du davor.

**Einfach gesagt:**
RDP ist wie TeamViewer – nur direkt von Windows, für Windows.

**Beispiel:**
Admins loggen sich per RDP auf Windows-Server ein, um Wartungen durchzuführen.

**🧠 Merksatz:**
> „RDP – der digitale Sessellift ins Rechenzentrum.“

**🔗 Quelle:**
[https://learn.microsoft.com/de-de/windows-server/remote/remote-desktop-services/welcome-to-rds](https://learn.microsoft.com/de-de/windows-server/remote/remote-desktop-services/welcome-to-rds)

---

### 🔹 S3 Storage

**Kurze Erklärung:**
**S3** (Simple Storage Service) ist objektbasierter Cloud-Speicher von AWS – hochverfügbar, skalierbar und über HTTP erreichbar.

**Einfach gesagt:**
S3 ist wie Dropbox für Server – aber ohne GUI und mit APIs.

**Beispiel:**
Ein Webshop speichert Produktbilder in S3 – weltweit abrufbar, mit wenig Aufwand.

**🧠 Merksatz:**
> „S3 – wenn deine Daten lieber im Himmel wohnen.“

**🔗 Quelle:**
[https://aws.amazon.com/s3/](https://aws.amazon.com/s3/)

---

---

### 🔹 SAS (Serial Attached SCSI)

**Kurze Erklärung:**
**SAS** ist eine Hochleistungs-Schnittstelle für Festplatten und SSDs, meist im Serverumfeld. Schnell, zuverlässig und hot-swappable – also perfekt fürs Rechenzentrum.

**Einfach gesagt:**
SAS ist SATA in Business-Klamotten – robuster, schneller, teurer.

**Beispiel:**
Ein Storage-Server mit SAS-HDDs kann selbst bei hoher Last stabil Daten liefern – oft mit Dual-Port-Anbindung für Redundanz.

**🧠 Merksatz:**
> „SAS – für Server, die keine Kompromisse mögen.“

**🔗 Quelle:**
[https://de.wikipedia.org/wiki/Serial_Attached_SCSI](https://de.wikipedia.org/wiki/Serial_Attached_SCSI)

---

### 🔹 SATA (Serial ATA)

**Kurze Erklärung:**
**SATA** ist die klassische Schnittstelle für Festplatten und SSDs in PCs, NAS und Consumer-Hardware. Kostengünstig und ausreichend schnell für viele Einsatzzwecke.

**Einfach gesagt:**
SATA ist der Golf unter den Festplattenanschlüssen – solide, bekannt, überall.

**Beispiel:**
Die meisten Heim-NAS setzen auf 3,5"-SATA-HDDs – günstig, aber mit Limit bei IOPS und Bandbreite.

**🧠 Merksatz:**
> „SATA – wenn du viel speichern willst, aber nicht gleich zum Rechenzentrum willst.“

**🔗 Quelle:**
[https://de.wikipedia.org/wiki/Serial_ATA](https://de.wikipedia.org/wiki/Serial_ATA)

---

### 🔹 STUN (Session Traversal Utilities for NAT)

**Kurze Erklärung:**
**STUN** ist ein Protokoll, das hilft, die eigene öffentliche IP und NAT-Konfiguration zu ermitteln – wichtig für Peer-to-Peer-Verbindungen.

**Einfach gesagt:**
STUN ist wie ein Netz-Periskop: „Wo bin ich eigentlich im Internet?“

**Beispiel:**
Ein Videotool nutzt STUN, um zu prüfen, ob zwei Clients direkt kommunizieren können – oder ob TURN helfen muss.

**🧠 Merksatz:**
> „STUN – der Selbstfindungstrip für deine IP.“

**🔗 Quelle:**
[https://tools.ietf.org/html/rfc5389](https://tools.ietf.org/html/rfc5389)

---

### 🔹 TURN (Traversal Using Relays around NAT)

**Kurze Erklärung:**
**TURN** ist ein Protokoll, das Peer-to-Peer-Verkehr über einen Relay-Server leitet, wenn direkte Kommunikation nicht möglich ist – z. B. bei strengen NATs.

**Einfach gesagt:**
TURN ist der Postbote, wenn zwei Leute sich nicht direkt treffen können.

**Beispiel:**
Zwei Teilnehmer in unterschiedlichen Firmen-VPNs nutzen TURN, um über WebRTC Video zu chatten.

**🧠 Merksatz:**
> „TURN – der Mittelsmann, wenn’s mit der Direktverbindung nichts wird.“

**🔗 Quelle:**
[https://datatracker.ietf.org/doc/html/rfc5766](https://datatracker.ietf.org/doc/html/rfc5766)

---

### 🔹 Through-Kommando

**Kurze Erklärung:**
Der Begriff „Through-Kommando“ ist **nicht standardisiert**. Vermutlich handelt es sich um ein internes Skript, einen Alias oder eine umgangssprachliche Bezeichnung.

**Einfach gesagt:**
Unklar. Klingt nach: „Schieb das mal durch den Tunnel!“ Bitte Kontext prüfen.

**🧠 Merksatz:**
> „Through-Kommando – klingt cool, macht aber was genau?“

**🔗 Quelle:**
(nicht auffindbar – kein offizieller Begriff)

---

### 🔹 Vesus Reporting

**Kurze Erklärung:**
Kein offiziell dokumentierter Begriff in IT- oder Netzwerkkontext. Möglicherweise handelt es sich um eine firmeninterne Software oder um einen Tippfehler.

**Einfach gesagt:**
Unklar – bitte prüfen, ob „Versus“, „Veeam“ oder „Visual Reporting“ gemeint ist.

**🧠 Merksatz:**
> „Vesus? Vielleicht ein Reporting – vielleicht ein Pokémon.“

**🔗 Quelle:**
(nicht belegt – kein verbreiteter Begriff)

---

### 🔹 Witnesser

**Kurze Erklärung:**
Ein **Witness** (bzw. Witness Node) ist ein neutraler Knotenpunkt in einem Cluster, der bei **Split-Brain-Situationen** entscheidet, welcher Teil "überlebt". Wird oft bei Storage-Replikation verwendet.

**Einfach gesagt:**
Der Witness ist der Schiedsrichter im Cluster-Streit.

**Beispiel:**
Zwei Storage-Server verlieren die Verbindung. Der Witness entscheidet, welcher weiter aktiv sein darf – damit es keine Datenkorruption gibt.

**🧠 Merksatz:**
> „Witness – der digitale Friedensrichter im Cluster-Krieg.“

**🔗 Quelle:**
[https://docs.vmware.com/en/VMware-vSAN/7.0/com.vmware.vsan.gettingstarted.doc/GUID-5A5B34D6-41F3-466C-8E5E-2E7934E1628F.html](https://docs.vmware.com/en/VMware-vSAN/7.0/com.vmware.vsan.gettingstarted.doc/GUID-5A5B34D6-41F3-466C-8E5E-2E7934E1628F.html)

---

### 🔹 iLOs (Integrated Lights-Out)

**Kurze Erklärung:**
**iLO** ist HPs Remote-Management-Interface für Server. Es erlaubt Zugriff auf den Server (inkl. BIOS und KVM), selbst wenn das Betriebssystem abgeschmiert ist.

**Einfach gesagt:**
iLO ist der USB-Stick mit Webcam und Reset-Knopf – nur übers Netzwerk.

**Beispiel:**
Ein Admin kann aus der Ferne ins BIOS, das System neu starten oder Logs prüfen – ohne physischen Zugang zum Server.

**🧠 Merksatz:**
> „iLO – Adminrechte mit Sofa-Komfort.“

**🔗 Quelle:**
[https://www.hpe.com/de/de/servers/integrated-lights-out-ilo.html](https://www.hpe.com/de/de/servers/integrated-lights-out-ilo.html)

## 🧠 Planung & Konzepte

---

### 🔹 Domain Controller

**Kurze Erklärung:**
Ein **Domain Controller (DC)** ist der zentrale Server in einem Windows-Netzwerk, der Benutzer authentifiziert und Zugriffsrechte verteilt – das Herzstück jeder Active Directory-Umgebung.

**Einfach gesagt:**
Der DC ist der Türsteher mit Gästeliste: „Du darfst rein, du nicht – und du nur bis zum Drucker!“

**Beispiel:**
Beim Einloggen prüft der Domain Controller, ob du ein legitimer User bist – samt Gruppenrichtlinien, Login-Skript und Roaming-Profil.

**🧠 Merksatz:**
> „Ohne Domain Controller kein Ordnungsamt in der Windows-Welt.“

**🔗 Quelle:**
[https://learn.microsoft.com/de-de/windows-server/identity/ad-ds/get-started/virtual-dc/what-is-active-directory-domain-services](https://learn.microsoft.com/de-de/windows-server/identity/ad-ds/get-started/virtual-dc/what-is-active-directory-domain-services)

---

### 🔹 Exposed Host

**Kurze Erklärung:**
Ein **Exposed Host** ist ein Gerät im Netzwerk, das ohne Firewall-Schutz direkt alle eingehenden Anfragen vom Router erhält – quasi nackt im Internet.

**Einfach gesagt:**
Das ist der Server ohne Regenschirm bei Gewitter – alles trifft ihn.

**Beispiel:**
Eine FritzBox leitet alle Ports an einen Raspberry Pi weiter, der damit völlig ungeschützt ist. Nicht zu empfehlen!

**🧠 Merksatz:**
> „Exposed Host – maximal erreichbar, minimal geschützt.“

**🔗 Quelle:**
[https://avm.de/service/fritzbox/fritzbox-7590/wissensdatenbank/publication/show/321_FRITZ-Box-als-DSL-Router-verwenden/](https://avm.de/service/fritzbox/fritzbox-7590/wissensdatenbank/publication/show/321_FRITZ-Box-als-DSL-Router-verwenden/)

---

### 🔹 Fabric (Netzwerk)

**Kurze Erklärung:**
**Fabric** bezeichnet ein engmaschiges Netzwerk-Design, das auf hohe Bandbreite, Redundanz und Skalierbarkeit ausgelegt ist – oft über Spine-Leaf-Architektur realisiert.

**Einfach gesagt:**
Fabric ist das Spinnennetz der IT – schnell, flexibel und überall verbunden.

**Beispiel:**
In modernen Rechenzentren nutzt man ein Fabric, um alle Server mit allen Switches mehrfach zu verknüpfen – für Low Latency und Redundanz.

**🧠 Merksatz:**
> „Fabric – das Netz, das sich nicht verheddert.“

**🔗 Quelle:**
[https://en.wikipedia.org/wiki/Network_fabric](https://en.wikipedia.org/wiki/Network_fabric)

---

### 🔹 Greenfield

**Kurze Erklärung:**
Ein **Greenfield-Projekt** ist eine IT-Umgebung, die **völlig neu** aufgebaut wird – ohne Altlasten, Zwänge oder bestehende Systeme. Das Gegenteil: Brownfield.

**Einfach gesagt:**
Greenfield ist wie ein leerer Acker: Du kannst alles von Grund auf frisch pflanzen – oder verbocken.

**Beispiel:**
Ein Startup setzt auf Greenfield, um seine Cloud-Infrastruktur komplett modern und containerbasiert zu planen – kein „Alt-Geraffel“.

**🧠 Merksatz:**
> „Greenfield – der Traum jedes Architekten: endlich ohne Altlasten!“

**🔗 Quelle:**
[https://en.wikipedia.org/wiki/Greenfield_project](https://en.wikipedia.org/wiki/Greenfield_project)
