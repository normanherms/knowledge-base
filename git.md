# Git Cheatbook

---

## Anmerkung

Dies ist ein persönliches Cheatbook.  
Es dient als Nachschlagewerk für meine eigenen Lerninhalte und erhebt keinen Anspruch auf Vollständigkeit.  
Die Inhalte wurden teilweise mit Unterstützung von ChatGPT geglättet und ergänzt.  
Auch wenn ich auf Richtigkeit achte, können Fehler enthalten sein.

---

## Einführung

- Git = Versionsverwaltung für Code (lokal + verteilt).
- Inhalte: Commits, Branches, Merge, Rebase, Pull Requests.
- Vorteil: automatische Versionierung, keine manuelle Sicherung der gesamten Codebasis nötig.

---

## Installation & Konfiguration

    # Installation (Debian/Ubuntu)
    sudo apt install git

    # Globale Konfiguration
    git config --global user.name "Dein Name"
    git config --global user.email "mail@example.com"
    git config --global core.editor nano        # oder vim
    git config --global init.defaultBranch main

---

## Basisbefehle

    git init           # neues Repo anlegen
    git status         # Status anzeigen

---

## Staging Area & Commits

    git add <file>              # Datei vormerken
    git add .                   # alle Dateien vormerken
    git commit -m "Nachricht"   # Commit erstellen

**Commit-Nachrichten**:

- Hauptsprache Englisch.
- Kurz und prägnant.
- Struktur: Was wurde gemacht? → ggf. genauere Beschreibung im Body.

---

## Logs

    git log            # Historie anzeigen
    git log -p         # mit detaillierten Änderungen
    git log --oneline  # kompakte Übersicht

---

## Commits ändern

    git commit --amend                      # letzten Commit anpassen (nur lokal verwenden!)
    git diff                                # Unterschiede Arbeitsverzeichnis ↔ Staging
    git diff --cached                       # Unterschiede Staging ↔ letztem Commit
    git diff <hash> <hash> -- <file>        # Diff zwischen Commits

---

## Reset (Achtung: Datenverlust möglich)

    git reset                   # staged Änderungen entfernen
    git reset <file>            # nur bestimmte Datei entfernen
    git reset <commit>          # setzt Branch-Zeiger zurück
    git reset --hard <commit>   # alles zurücksetzen, auch Arbeitsverzeichnis

---

## Checkout / Switch

    git checkout <commit>   # in Commit springen (detached HEAD)
    git checkout main       # zurück zum Branch

---

## HEAD

- **HEAD** = aktueller Commit-Zeiger.
- Beispiele:

        git diff HEAD~2 HEAD   # Unterschiede zwischen vorletztem und aktuellem Commit

---

## Stash

    git stash        # Änderungen zwischenspeichern
    git stash pop    # letzten Eintrag zurückholen
    git stash list   # Liste anzeigen
    git diff stash   # Unterschiede zum Stash anzeigen

---

## Revert

    git revert <commit>

- Erstellt einen neuen Commit, der die Änderungen eines älteren Commits rückgängig macht.
- Konflikte möglich, wenn spätere Commits denselben Bereich betreffen.
- Auflösen: Datei manuell bearbeiten → git add → git revert --continue.
- Abbrechen: git revert --abort

---

## Ignore

- `.gitignore` = Liste von Dateien/Ordnern, die Git ignorieren soll.
- Typische Beispiele: `*.log`, `node_modules/`, `.env`.
- Vorlagen für `.gitignore` gibt es bei GitHub.

---

## Dateien löschen/verschieben

    git rm <file>        # Datei löschen
    git mv <alt> <neu>   # Datei umbenennen/verschieben

---

## Blame

    git blame <file>                # Zeigt Zeile für Zeile wer was geändert hat
    git blame --color-lines <file>  # farbliche Darstellung

Alternative zu git log, um Änderungen nachzuvollziehen.

---

## GUI-Tools

- Windows/macOS: SourceTree.
- Linux: GitKraken, Fork, SmartGit, Git Cola oder VS Code mit GitLens.

---

## Branches

Branches sind Verzweigungen, die z. B. für Features genutzt werden können.  
Damit ist auch parallele Mitarbeit mehrerer Entwickler möglich.

    git branch                       # zeigt alle vorhandenen Branches an
    git branch <branchname>          # legt einen neuen Branch an
    git checkout <branchname>        # wechselt zu einem Branch
    git checkout -b <branchname>     # legt einen neuen Branch an und wechselt direkt dorthin

---

## Branches mergen (Fast-Forward-Merge)

    git checkout main
    git merge featurebranch
    git branch -d featurebranch

Ein Fast-Forward-Merge fügt den Feature-Branch linear an den Main-Branch an.  
Danach kann der Feature-Branch gelöscht werden.

---

## Three-Way-Merge

Wichtig, wenn sich `main` seit dem Abzweigen des Feature-Branch geändert hat.

    git checkout main
    git merge testbranch
    # Commit-Message ausfüllen
    git branch -d testbranch

---

## Konflikte beim Mergen

- Treten auf, wenn die **gleichen Zeilen** geändert wurden.  
- Konfliktmarker (`<<<<<<<`, `=======`, `>>>>>>>`) müssen **manuell entfernt** werden.  
- Danach:

        git add <file>
        git commit

Prüfen, ob nach dem Merge alle Funktionen noch korrekt sind.

Nützlicher Befehl zur Visualisierung:

    git log --oneline --branches --graph

---

## Git Rebase

!!! Vorsicht: nur anwenden, wenn niemand anders gleichzeitig auf dem Branch arbeitet !!!

Rebase hängt Änderungen eines Feature-Branch an den letzten Commit von `main` an (wie ein nachträglicher Fast-Forward).  
Dabei werden Commits einzeln „wiederholt“ → Konflikte müssen direkt pro Commit aufgelöst werden.

    git checkout <featurebranch>
    git rebase main

---

## Merge-Optionen

    git merge --no-ff       # Verhindert einen Fast-Forward-Merge
    git merge --ff-only     # Erzwingt einen Fast-Forward-Merge

### Vorteile Fast-Forward-Merge

- Repo bleibt linear  
- leichter nachvollziehbar

### Vorteile Three-Way-Merge

- Jeder Feature-Branch bleibt sichtbar  
- Entwicklungsgeschichte der Features nachvollziehbar

---

## Tags

Tags markieren bestimmte Commits, oft für Releases.

    git tag -a v<x.y>            # Tag mit Nachricht auf aktuellen Commit
    git tag -a <commit-hash>     # Tag nachträglich auf älteren Commit setzen

Mit `-a` wird ein Kommentar (Annotation) erzwungen.

    git checkout <Tag>           # springt zu Commit mit diesem Tag

---

## Git Remote Repositories

Vorteile bei Remote-Repositories: Zusammenarbeit mehrerer Entwickler wird möglich.

---

### Git Repos klonen und anzeigen

    git clone <url>         # erstellt eine lokale Kopie des Repositories
    git remote -v           # zeigt alle konfigurierten Remotes

Standardmäßig legt Git beim Klonen den Remote-Namen `origin` an → z. B. `origin/main`.

---

### Remote Workflow: fetch & pull

    git fetch                   # lädt aktuelle Änderungen vom Remote Repo
    git branch -vv              # zeigt lokale Branches mit Tracking-Infos
    git log origin/<branch>     # zeigt Logs vom Remote Branch
    git merge origin/<branch>   # integriert Remote-Änderungen in den aktuellen Branch

    git pull                    # = fetch + merge für den aktuellen Branch

---

### GitHub Repo erstellen & verbinden

Auf GitHub → *New* → neues Repo erstellen.  
Dann lokales Repo verbinden:

    git remote add origin https://github.com/USERNAME/REPO.git
    git branch -M main
    git push -u origin main

#### Remote Repo entfernen

    git remote remove origin

#### Remote Repo hochladen

    git push

---

### Pull Requests

Ein Pull Request (PR) ist ein Vorschlag, Änderungen aus einem Branch in einen anderen (meist `main`) zu übernehmen.  
Er wird genutzt, wenn mehrere Entwickler am gleichen Repo arbeiten und dient auch als Review-Mechanismus.  

Ablauf:

- Lokalen Branch mit Remote verbinden:

        git push --set-upstream origin <branchname>

- Auf GitHub einen PR erstellen, Branch auswählen, Beschreibung hinzufügen.  
- Nach dem Merge PR schließen und den lokalen `main` mit `git pull` aktualisieren.

---

### Issues & Pull Requests

- Commit-Nachrichten können direkt auf Issues verweisen, z. B. `#42`.  
- Schlüsselwörter wie `resolves #42` oder `closes #42` im PR schließen ein Issue automatisch nach dem Merge.  
- So lassen sich Änderungen nachvollziehbar mit Aufgaben verknüpfen.

---

### Collaborators

- Direkte Commits auf `main/master` vermeiden, stattdessen PRs nutzen.  
- Collaborators können per Einladung Zugriff erhalten.  
- Branch-Protection-Regeln sichern den Workflow (z. B. Review-Pflicht vor Merge).

---

### Fork & Pull Request

- Ein Fork ist ein eigenes Abbild eines fremden Repos unter dem eigenen Account.  
- Änderungen erfolgen im Fork und können anschließend per PR an das ursprüngliche Repo vorgeschlagen werden.

---

### Fork aktuell halten (Rebase oder Merge)

Ein Fork basiert auf einem Snapshot des Original-Repos („upstream“).  
Damit er aktuell bleibt, muss man regelmäßig die Änderungen aus dem Original holen.

Upstream einmalig einrichten:

    git remote add upstream https://github.com/ORIGINAL/REPO.git

Änderungen aus Upstream holen:

    git fetch upstream

Option 1: Mit Merge aktualisieren

    git checkout main
    git merge upstream/main

Option 2: Mit Rebase aktualisieren (lineare History)

    git checkout main
    git rebase upstream/main

Danach Push aktualisieren (bei Rebase oft Force nötig):

    git push --force origin main

---

### Code Review im Pull Request

- Ein PR ist nicht nur ein technischer Merge, sondern auch ein Ort für Diskussion und Review.  
- Teammitglieder können Kommentare zu einzelnen Zeilen hinterlassen, Änderungen anfragen oder den PR freigeben.  
- Erst nach Review (je nach Branch-Protection-Regeln) darf gemergt werden.

---

### Merge-Strategien (GitHub)

Beim Schließen eines PR können verschiedene Strategien gewählt werden:

- **Merge Commit (Standard)**  
  Bewahrt die gesamte Branch-Historie → nachvollziehbare Entwicklung.  

- **Squash & Merge**  
  Fasst alle Commits aus dem PR zu einem einzigen Commit zusammen → saubere History.  

- **Rebase & Merge**  
  Hängt die PR-Commits linear hinter den Ziel-Branch → wirkt wie direkte Commits ohne Merge-Commit.  
