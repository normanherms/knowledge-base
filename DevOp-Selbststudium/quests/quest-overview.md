# DevOps Quest System – Gamified Learning Path

## Einführung

Das **DevOps Quest System** ist ein begleitendes Framework für das Selbststudium.
Es übersetzt die Lernmodule in kleine, klar definierte Aufgaben („Quests“), die praktische Anwendung und Reflexion fördern.
Das System ist vollständig textbasiert und erfordert keine zusätzliche Software.
Ziel ist es, Fortschritt sichtbar zu machen – nicht durch Punkte, sondern durch nachvollziehbare Ergebnisse.

---

## Aufbau des Systems

Jedes Lernmodul enthält:

1. **Main Quests** – verpflichtende Aufgaben, die die Kernziele des Moduls abdecken.
2. **Side Quests** – optionale Erweiterungen, um das Wissen zu vertiefen.
3. **Achievements** – kurze Bezeichnungen, die den Lernerfolg benennen (z. B. „Configuration Master“).

Alle Aufgaben sind in Markdown beschrieben und können Schritt für Schritt dokumentiert werden.

---

## Level-System

Das Level-System dient nur der Orientierung und Motivation.
Es spiegelt den individuellen Lernfortschritt wider und kann frei angepasst werden.

| Level | Bezeichnung | Beschreibung                                           | XP-Bereich |
| ----- | ----------- | ------------------------------------------------------ | ---------- |
| 1     | Novice      | Einstieg in die Grundlagen                             | 0–200      |
| 2     | Apprentice  | Erste Sicherheit in Kernkonzepten                      | 201–500    |
| 3     | Journeyman  | Selbstständige Arbeit mit Tools und Pipelines          | 501–1000   |
| 4     | Expert      | Umfassendes Verständnis und Routine                    | 1001–1800  |
| 5     | Master      | Sicherer Umgang mit allen zentralen DevOps-Komponenten | 1801–2500  |
| 6     | Legend      | Alle Module und Bonuschallenges abgeschlossen          | >2500      |

---

## Struktur der Lernpfade

Das Curriculum ist in drei Lernpfade aufgeteilt.
Jeder Pfad bündelt thematisch verwandte Module.

| Pfad                              | Module | Schwerpunkt                                         |
| --------------------------------- | ------ | --------------------------------------------------- |
| **Path I – Foundations**          | 00–04  | Grundlagen: Linux, Python, Git, CI, Container       |
| **Path II – Automation & Ops**    | 05–09  | Infrastruktur, Automatisierung, Cluster, Monitoring |
| **Path III – Security & Scaling** | 10–13  | Sicherheit, Testing, Betrieb, Cloud                 |

Jeder Pfad kann einzeln bearbeitet werden.
Der empfohlene Startpunkt ist **Path I – Foundations**.

---

## Punkte- und Zeitsystem

* Durchschnittlich **100 XP pro Modul** (ca. 10–15 Stunden Lernzeit).
* Main Quests decken etwa 70 XP ab, Side Quests 30 XP.
* Die Gesamtzeit für alle Module liegt bei ca. 180–200 Stunden.

Der XP-Wert ist **symbolisch** und hilft nur, Lernumfang einzuschätzen – es gibt keine Bewertung, nur Fortschritt.

---

## Arbeitsweise

1. **Wähle ein Modul** aus dem jeweiligen Pfad.
2. **Lies die Aufgaben** in der zugehörigen Quest-Datei (z. B. `path-01-foundations.md`).
3. **Bearbeite jede Quest** Schritt für Schritt und dokumentiere dein Vorgehen.
4. **Reflektiere** im Lernjournal, was du verstanden hast.
5. **Kennzeichne abgeschlossene Quests** einfach mit `[x]`.

Das System funktioniert offline und ist vollständig Git-kompatibel.
Jede Aufgabe ist so formuliert, dass sie praktisch lösbar ist – keine Simulation, sondern echtes Arbeiten mit Tools.

---

## Beispiel: Quest-Abschnitt in einem Modul

```markdown
## Modul 00 – Grundlagen & Einstieg
**Quest:** "Die Reise beginnt"
**Schwierigkeit:** Einsteiger
**Zeit:** 12 – 15 Stunden
**XP:** 100

### Main Quests
- [ ] Lerne grundlegende Linux-Kommandos und Strukturen.
- [ ] Schreibe dein erstes Bash-Skript mit Logging.
- [ ] Richte eine automatisierte Aufgabe per Cron ein.

### Side Quests
- [ ] Löse OverTheWire Bandit Level 0 – 10.
- [ ] Erstelle dein eigenes CLI-Cheatsheet.

**Achievement:** „Shell Practitioner“
```

---

## Wartung und Weiterentwicklung

Das Quest-System ist bewusst einfach gehalten:

* alle Inhalte liegen in Markdown-Dateien,
* keine externen Abhängigkeiten oder Programme,
* leicht erweiterbar durch neue Quests oder Pfade.

Ergänzungen sollen sich an der bestehenden Struktur orientieren:

* kurze, präzise Aufgaben,
* keine Fließtexte oder Theorienachweise,
* Fokus auf praktische Handlung.

---

## Zielbild

Das DevOps Quest System ist kein Spiel, sondern ein Lernrahmen.
Es motiviert durch Struktur, Selbstreflexion und sichtbaren Fortschritt.
Die Herausforderung besteht darin, das eigene Wissen anzuwenden, nicht Punkte zu sammeln.

---

📅 2025-10-13 00:08 | §quest-system §lernstruktur §curriculum
