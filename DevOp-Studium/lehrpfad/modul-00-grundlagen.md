# Modul 00 – Grundlagen & Einstieg

## Ziel

Verständnis, wie Systeme technisch und organisatorisch zusammenarbeiten.
Dieses Modul bildet das Fundament für alle weiteren Themen im DevOps-Bereich.

---

## Kerninhalte

| Bereich                   | Themen                                                                          |
| ------------------------- | ------------------------------------------------------------------------------- |
| Linux & CLI               | Shell, Dateisysteme, Prozesse, Benutzer, Rechte, Systemd, Paketmanager          |
| Netzwerk-Basics           | TCP/IP, DNS, HTTP/S, Routing, Firewalls, Ports                                  |
| Scripting-Grundlagen      | Bash-Syntax, einfache Automatisierungen, Einstieg in Python                     |
| Betriebssystemverständnis | Kernel, Logs, Ressourcenverwaltung, Services                                    |
| DevOps-Mindset            | CALMS-Modell (Culture, Automation, Lean, Measurement, Sharing), Feedback-Kultur |
| Toolchain-Basis           | VS Code, Git, GitHub, SSH, curl, jq, dig, nc                                    |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion | Abgedeckt durch           | Status |
| ------------------ | ------------------------- | ------ |
| linux-basics       | Linux & CLI               | ✅      |
| networking-basics  | Netzwerk-Basics           | ✅      |
| bash-scripting     | Scripting-Grundlagen      | ✅      |
| operating-system   | Betriebssystemverständnis | ✅      |
| devops-culture     | DevOps-Mindset            | ✅      |
| essential-tools    | Toolchain-Basis           | ✅      |
| version-control    | Vorbereitung auf Modul 2  | 🕸️    |

---

## Theoriephase

Ziel: Grundverständnis für Linux-Systeme und Kommandozeilen-Arbeit.

* Aufbau eines Betriebssystems: Kernel – Userland – Shell
* Prozesse und Rechte: ps, top, chmod, sudo
* Dateisystem und Pfade: ls, cd, cp, mv, find
* Dienste und Systemd: systemctl status, start, enable
* Netzwerkdiagnose: ping, curl, dig, ss, netstat
* Textverarbeitung: grep, awk, sed, cat, less

---

## Praxisphase

Ziel: Eigene Linux-Umgebung aufbauen und erste Automatisierung umsetzen.

1. Installation von Debian 13 oder Fedora
2. Einrichtung eines nicht-Root-Users mit SSH-Key
3. Nutzung grundlegender Shell-Kommandos und Verkettungen per Pipe
4. Schreiben eines ersten Bash-Skripts, das z. B. Logdateien komprimiert und archiviert
5. Analyse von System-Logs (z. B. /var/log/syslog, journalctl -xe)
6. Netzwerktests mit nc, ping, curl und dig

---

## Projektphase

Beispielprojekt:
Ein Skript zur täglichen Sicherung von Systemlogs oder Konfigurationsdateien.
Die Ausführung wird automatisiert (Cronjob) und der Ablauf in Markdown dokumentiert.

Ziel: Ein funktionierendes, sicheres Automationsskript als Grundlage für spätere CI-Pipelines.

---

## Reviewphase

Reflexion:

* Verstehe ich, was im System beim Start passiert?
* Kann ich Netzwerkprobleme mit CLI-Tools analysieren?
* Beherrsche ich grundlegende Shell-Automatisierungen?

Empfohlene Tools zur Vertiefung:
htop, btop, ncdu, jq, curl, dig, tmux, ssh-agent

---

## Ressourcen

| Thema            | Quelle                                                                             |
| ---------------- | ---------------------------------------------------------------------------------- |
| Linux Grundlagen | [https://linuxjourney.com](https://linuxjourney.com)                               |
| Shell & Bash     | [https://www.bash.academy](https://www.bash.academy)                               |
| Netzwerk         | [https://overthewire.org/wargames/bandit](https://overthewire.org/wargames/bandit) |
| DevOps Kultur    | [https://educationops.org/calms-model](https://educationops.org/calms-model)       |
| Toolchain        | [https://roadmap.sh/devops](https://roadmap.sh/devops)                             |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Eine lauffähige Linux-Umgebung mit SSH-Zugang
* Grundverständnis von Netzwerk, CLI und Systemstrukturen
* Ein erstes Automationsskript im Git-Repo dokumentiert
* Eine funktionierende DevOps-Basisumgebung (VS Code + GitHub + SSH)

---

Nächster Schritt: Modul 01 – Python-Automation

---

🕛 2025-10-12 20:39 | §devops §modul0 §roadmapsh
