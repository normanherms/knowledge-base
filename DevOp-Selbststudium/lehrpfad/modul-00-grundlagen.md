# Modul 00 – Grundlagen & Einstieg

## Ziel

Verstehen, wie ein System technisch und organisatorisch funktioniert.
Dieses Modul bildet die Basis für alle späteren DevOps-Themen – Betriebssystem, Netzwerk, Automatisierung und Kultur.

---

## Lernorientierung

Selbstlerner benötigen klare Ziele und Strukturen.
Am Ende dieses Moduls solltest du:

1. ein Linux-System sicher bedienen können,
2. die wichtigsten Netzwerkmechanismen verstehen,
3. einfache Skripte schreiben und automatisieren,
4. grundlegende DevOps-Prinzipien kennen,
5. mit zentralen Tools (Git, SSH, VS Code) souverän umgehen.

---

## Themenüberblick

| Bereich                   | Lerninhalte & Schwerpunkte                                                                                  |
| -------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Linux & CLI               | Shell-Grundlagen, Dateisystem, Rechte, Prozesse, Dienste, systemd, Paketmanager                             |
| Netzwerk-Basics           | TCP/IP, DNS, Routing, Ports, Firewalls, HTTP/S, Tools zur Analyse                                           |
| Scripting-Grundlagen      | Bash-Syntax, Kontrollstrukturen, Variablen, Pipes, Einstieg in Python                                       |
| Betriebssystemverständnis | Kernel, Userland, Bootprozess, Logs, Ressourcenverwaltung, Fehlerdiagnose                                   |
| DevOps-Mindset            | CALMS-Modell (Culture, Automation, Lean, Measurement, Sharing), Feedback-Kultur, kontinuierliches Lernen     |
| Toolchain-Basis           | VS Code, Git & GitHub, SSH, curl, jq, dig, nc, tmux, CLI-Produktivität                                      |

> Orientierung: Themen decken den Abschnitt „Foundations“ der [DevOps-Roadmap auf roadmap.sh](https://roadmap.sh/devops) ab.

---

## Lernziele nach Themenfeld

### 1. Linux & CLI

**Was lernen:**

- Struktur eines Linux-Systems
- Arbeiten mit Shell, Dateien, Prozessen, Rechten
- Dienste starten, stoppen und kontrollieren

**Wie lernen:**

- Interaktiv üben auf einer Debian- oder Fedora-VM
- Man-Pages lesen, Aufgaben selbst lösen, Fehler dokumentieren

**Beispiele:**

- Nutzer anlegen und Rechte prüfen
- `systemctl`-Dienste verwalten
- `find` + `grep` für Logsuche kombinieren

---

### 2. Netzwerk-Basics

**Was lernen:**

- Wie Pakete über TCP/IP fließen
- Aufbau und Auflösung von DNS
- Erkennen von offenen Ports und Routing-Problemen

**Wie lernen:**

- Mit Tools experimentieren (`ping`, `traceroute`, `curl`, `dig`, `nc`)
- Netzwerkdiagramm zeichnen (eigene Verbindung vom PC bis Website)

**Beispiele:**

- Ping zu 8.8.8.8 und DNS-Test mit `dig google.com`
- Verbindung zu Remote-Host über `nc` prüfen

---

### 3. Scripting-Grundlagen

**Was lernen:**

- Shell-Syntax verstehen (Variablen, if, loops)
- Automatisierungen schreiben und testen
- Saubere Ausgabe, Logging, Exit-Codes

**Wie lernen:**

- Eigene Skripte im Home-Verzeichnis schreiben und in Git sichern
- Aufgaben: Dateiüberwachung, Backup, Kompression, Logrotation

**Beispiele:**

- Skript, das Logdateien in /var/log komprimiert
- Cronjob zur täglichen Ausführung

---

### 4. DevOps-Mindset

**Was lernen:**

- Bedeutung von Zusammenarbeit, Feedback, Automatisierung
- Das CALMS-Modell als Rahmen für Kultur und Technik
- Warum DevOps kein Jobtitel, sondern eine Arbeitsweise ist

**Wie lernen:**

- Lesen, hören und reflektieren: technische + menschliche Seite
- Eigene Beobachtungen im Alltag notieren (Wo fehlt Feedback? Wo hilft Automatisierung?)

---

## Praxisprojekt

**Aufgabe:**
Ein Bash-Skript erstellt täglich ein Backup bestimmter Konfigurationsdateien und komprimiert sie in einem Archiv.
Das Skript wird über Cron ausgeführt und das Ergebnis im Git-Repository dokumentiert.

**Lernziel:**
Ein funktionierendes, nachvollziehbares Automationsskript als Grundlage für CI/CD.

---

## Selbstreflexion

Am Ende solltest du beantworten können:

- Wie startet und läuft ein Linux-System technisch ab?
- Wie erkenne ich Netzwerkprobleme mit CLI-Tools?
- Kann ich einfache Automatisierungen schreiben, dokumentieren und sicher ausführen?

---

## Ressourcen (frei & geprüft)

| Kategorie | Format | Quelle / Beschreibung |
| ---------- | ------- | --------------------- |
| Linux & CLI | Interaktiv | [Linux Journey](https://linuxjourney.com) – freier interaktiver Einstieg |
| Bash | Text | [Bash Academy](https://www.bash.academy) – kompakter Überblick zur Syntax |
| Netzwerkpraxis | Übung | [OverTheWire: Bandit](https://overthewire.org/wargames/bandit) – spielerisches Linux-Netzwerktraining |
| DevOps-Kultur | Artikel | [CALMS-Modell – EducationOps](https://educationops.org/calms-model) |
| DevOps-Einstieg | Video | [DevOps Explained – freeCodeCamp](https://www.youtube.com/watch?v=_I94-tJlovg) – visuelle Einführung (~1h) |
| Toolchain | Artikel | [roadmap.sh/devops](https://roadmap.sh/devops) – Orientierung zu Tools und Lernpfad |
| Motivation & Kultur | Podcast | [Ship It! (Changelog Network)](https://changelog.com/shipit) – reale DevOps-Erfahrungen und Kultur |
| Linux für Einsteiger | Video | [Learn Linux (NetworkChuck)](https://www.youtube.com/watch?v=ivlT3nFqKJ8) – praxisorientierter Einstieg (~45 min) |
| CLI-Kommandos | Cheatsheet | [cheat.sh](https://cheat.sh) – direkte CLI-Hilfe für Befehle |

---

## Ergebnis

Am Ende von Modul 00 hast du:

- eine funktionierende Linux-Umgebung mit SSH-Zugang,
- ein Verständnis für Netzwerke, Prozesse und Systemdienste,
- dein erstes Bash-Skript im eigenen Git-Repository,
- grundlegendes Verständnis der DevOps-Kultur,
- eine persönliche Lernroutine etabliert.

---

**Weiterführend:** Modul 01 – Python-Automation
**geändert am 2025-10-14**
