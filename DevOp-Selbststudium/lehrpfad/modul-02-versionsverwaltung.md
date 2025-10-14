# Modul 02 – Versionsverwaltung

## Ziel

Versionskontrolle verstehen und sicher anwenden – lokal und remote.
Dieses Modul vermittelt die Grundlagen von **Git** und **GitHub** als Basis für Zusammenarbeit, Nachvollziehbarkeit und spätere CI/CD-Prozesse.

---

## Lernorientierung

Ziel für Selbstlernende:
Die Logik hinter Versionskontrolle begreifen und ein eigenes, sauberes Git-Workflow-System aufbauen.

Am Ende dieses Moduls solltest du:

1. Git lokal einrichten und effektiv nutzen können
2. Branches, Commits und Merges sicher beherrschen
3. mit Remote-Repositories (GitHub, GitLab) arbeiten
4. Pull Requests, Reviews und Releases verstehen
5. die Bedeutung von Git für Automatisierung (CI/CD) kennen

---

## Themenüberblick

| Bereich            | Lerninhalte & Schwerpunkte                                                |
| ------------------ | -------------------------------------------------------------------------- |
| Grundlagen         | Repositories, Commits, Branches, Merges                                   |
| Workflows          | Feature Branches, Pull Requests, Merge-Strategien                         |
| Remote-Systeme     | GitHub, GitLab, SSH-Keys, Token, Forks                                    |
| Konfliktmanagement | Merge-Konflikte, Rebase, History Cleanup                                  |
| Best Practices     | Commit Messages, Tags, Release Management                                 |

> Orientierung: Inhalte entsprechen dem Abschnitt „Version Control Systems“ der [DevOps-Roadmap](https://roadmap.sh/devops).

---

## Lernziele nach Themenfeld

### 1. Git-Grundlagen

**Was lernen:**

- Funktionsweise von Versionskontrolle
- Arbeitsbereiche: Working Directory, Staging, Repository
- Befehle: `git init`, `add`, `commit`, `log`, `status`, `diff`

**Wie lernen:**

- Lokales Test-Repository anlegen
- Dateiänderungen committen und Versionen vergleichen

**Beispiele:**

- Initiales Repository mit README.md
- Drei Commits mit Änderungen und Rücksprung (`git checkout`)

---

### 2. Branching & Workflows

**Was lernen:**

- Branch-Konzepte und Workflows (main, dev, feature)
- Merge-Strategien (fast-forward, squash, rebase)
- Pull Requests als Review-Werkzeug

**Wie lernen:**

- Eigenes Branch-System im Projekt einführen
- Branches zusammenführen und Konflikte gezielt erzeugen

**Beispiele:**

- Feature-Branch erstellen, Merge-Konflikt lösen
- Branch-Historie mit `git log --graph` visualisieren

---

### 3. Remote-Systeme

**Was lernen:**

- Verbindung lokaler Repos mit GitHub
- Authentifizierung per SSH-Key oder Token
- Cloning, Forking, Upstream-Verwaltung

**Wie lernen:**

- SSH-Key erzeugen (`ssh-keygen`) und in GitHub einbinden
- Repository clonen und per Pull Request beitragen

**Beispiele:**

- Lokales Repo pushen
- Änderungen per Pull Request auf GitHub einreichen

---

### 4. Konfliktmanagement & History

**Was lernen:**

- Konflikte verstehen und manuell lösen
- History säubern (rebase, squash, amend)
- Tags und Releases nutzen

**Wie lernen:**

- Konflikt simulieren und gezielt auflösen
- Commit-Historie bereinigen, saubere Release-Tags setzen

**Beispiele:**

- Merge-Konflikt mit `<<<<<<<` analysieren
- `git rebase -i HEAD~3` für Clean History

---

### 5. Best Practices

**Was lernen:**

- Aussagekräftige Commit-Messages schreiben
- Sinnvolle Branch-Benennung
- Release-Zyklen planen

**Wie lernen:**

- Eigene Commit-Konvention (z. B. Conventional Commits) festlegen
- README und CHANGELOG pflegen

---

## Praxisprojekt

**Aufgabe:**
Ein Mini-Projekt (z. B. Bash- oder Python-Skript) wird versioniert, in GitHub veröffentlicht und über Pull Requests gepflegt.
Optional: Einfache GitHub Action für Syntaxprüfung oder Tests.

**Lernziel:**
Ein strukturierter Git-Workflow mit dokumentiertem Change-Management und sauberer Commit-Historie.

---

## Selbstreflexion

Am Ende solltest du beantworten können:

- Kann ich den Zustand eines Projekts jederzeit rekonstruieren?
- Nutze ich Branches und Commits sinnvoll?
- Kann ich Konflikte selbstständig lösen?
- Dokumentiere ich Änderungen nachvollziehbar?

---

## Ressourcen (frei & geprüft)

| Kategorie | Format | Quelle / Beschreibung |
| ---------- | ------- | --------------------- |
| Git Grundlagen | Text | [Pro Git (Online Book)](https://git-scm.com/book/en/v2) – offizielles Standardwerk |
| Git-Workflows | Artikel | [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials) – Praxisorientierte Vergleiche |
| Branching Modelle | Artikel | [A Successful Git Branching Model](https://nvie.com/posts/a-successful-git-branching-model/) |
| GitHub Flow | Artikel | [GitHub Flow Guide](https://guides.github.com/introduction/flow/) |
| Konfliktlösung | Video | [Git Merge Conflicts Explained (freeCodeCamp)](https://www.youtube.com/watch?v=JtIX3HJKwfo) (~20 min) |
| Pull Requests | Video | [GitHub Pull Request Tutorial (The Net Ninja)](https://www.youtube.com/watch?v=rgbCcBNZcdQ) (~25 min) |
| GitKraken Basics | Video | [GitKraken 101 – Visual Git](https://www.youtube.com/watch?v=UBAX-13g8OM) |
| Git CLI Training | Interaktiv | [learngitbranching.js.org](https://learngitbranching.js.org) – spielerisches Lernen |
| DevOps Integration | Video | [Git & GitHub for DevOps Engineers (freeCodeCamp)](https://www.youtube.com/watch?v=RGOj5yH7evk) (~2 h) |
| Podcast | Audio | [The Git Minute Podcast](https://changelog.com/gotime) – Themen rund um Git-Workflows |

---

## Ergebnis

Am Ende von Modul 02 hast du:

- ein funktionierendes lokales und Remote-Git-Setup,
- Verständnis für Branching, Merging und Konfliktlösung,
- saubere Commit-Historien mit dokumentierten Änderungen,
- erste CI/CD-Anknüpfung über GitHub Actions vorbereitet.

---

**Weiterführend:** Modul 03 – Continuous Integration
**geändert am 2025-10-14**
