# Modul 02 – Versionsverwaltung

## Ziel

Verständnis und sichere Anwendung von Versionskontrolle mit Git und GitHub.
Dieses Modul vermittelt das Fundament für kollaboratives Arbeiten, Nachvollziehbarkeit und CI/CD-Integration.

---

## Kerninhalte

| Bereich            | Themen                                            |
| ------------------ | ------------------------------------------------- |
| Grundlagen         | Repositories, Commits, Branches, Merges           |
| Workflows          | Feature Branches, Pull Requests, Merge-Strategien |
| Remote-Systeme     | GitHub, GitLab, SSH-Keys, Token, Forks            |
| Konfliktmanagement | Merge-Konflikte, Rebase, History Cleanup          |
| Best Practices     | Commit Messages, Tags, Release Management         |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion      | Abgedeckt durch           | Status |
| ----------------------- | ------------------------- | ------ |
| version-control-systems | Git-Grundlagen            | ✅      |
| git-branching           | Workflows                 | ✅      |
| collaboration           | Pull Requests, Reviews    | ✅      |
| hosting-services        | GitHub, GitLab            | ✅      |
| ci-cd-basics            | Vorbereitung auf Modul 03 | 🔜     |

---

## Theoriephase

Ziel: Verständnis der Versionskontrolle und ihrer Bedeutung für DevOps-Prozesse.

* Zweck und Philosophie von Versionskontrolle
* Aufbau eines Repositorys
* Funktionsweise von Commit, Stage, Merge, Rebase
* Remote-Repositories und Authentifizierung
* Einführung in GitHub Actions als Brücke zu CI/CD

---

## Praxisphase

Ziel: Git im Alltag sicher anwenden.

1. Installation und Konfiguration von Git
2. Erstellung eines lokalen Repositorys und Verbindung zu GitHub
3. Branching-Strategie einführen (main/dev/feature)
4. Erstellung eines Pull Requests mit Review-Simulation
5. Umgang mit Merge-Konflikten und Rebases
6. Nutzung von Tags und Releases
7. Dokumentation der Git-Kommandos und Workflows in Markdown

---

## Projektphase

Beispielprojekt:
Ein Mini-Projekt (z. B. Bash- oder Python-Skript) wird versioniert, in GitHub veröffentlicht und über Pull Requests gepflegt.
Optional: Einbindung erster GitHub-Actions für Syntaxprüfung oder Tests.

Ziel: Sauberer Git-Workflow mit dokumentiertem Change-Management.

---

## Reviewphase

Reflexion:

* Kann ich Code-Änderungen strukturiert nachverfolgen?
* Habe ich eine sinnvolle Branch-Strategie gewählt?
* Sind meine Commit-Messages klar und nachvollziehbar?

Empfohlene Tools zur Vertiefung:
GitKraken, LazyGit, GitHub CLI, gh, tig

---

## Ressourcen

| Thema             | Quelle                                                                                                                     |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Git Grundlagen    | [https://git-scm.com/book](https://git-scm.com/book)                                                                       |
| Git Workflows     | [https://www.atlassian.com/git/tutorials/comparing-workflows](https://www.atlassian.com/git/tutorials/comparing-workflows) |
| GitHub Actions    | [https://docs.github.com/actions](https://docs.github.com/actions)                                                         |
| Open Source Flow  | [https://guides.github.com/introduction/flow/](https://guides.github.com/introduction/flow/)                               |
| Branching Modelle | [https://nvie.com/posts/a-successful-git-branching-model/](https://nvie.com/posts/a-successful-git-branching-model/)       |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Einen funktionierenden Git-Workflow für lokale und Remote-Repos
* Verständnis für Branching, Merging und Konfliktlösung
* Eine konsistente Commit-Struktur und Dokumentation
* Erste CI-Verknüpfung durch GitHub Actions vorbereitet

---

Nächster Schritt: Modul 03 – Continuous Integration

---

🕓 2025-10-12 21:00 | §devops §modul2 §git
