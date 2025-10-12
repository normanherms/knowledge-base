# Iteration Plan – DevOp-Selbststudium

**Version:** 1.1
**Datum:** 2025-10-13
**Status:** Offen

---

## Ziel

Dieser Plan dokumentiert die Verbesserungen und Anpassungen des DevOps-Selbststudiums basierend auf Feedback-Runde vom 2025-10-13.

**Fokus:**
- Realistische Zeitplanung
- Gezieltes Debugging durch authentische Fehlerszenarien
- Flexiblere Dokumentation
- Authentisches Lernen ohne KI-Abhängigkeit

---

## 1. Zeitplanung anpassen

**Problem:** Die geschätzte Lernzeit ist zu ambitioniert.

**Lösung:**
- [ ] Puffer von +30–40 % auf alle Modulzeitschätzungen
- [ ] Path I: 60h → 80–90h (8–10 Wochen bei 10h/Woche)
- [ ] Path II: 70h → 90–100h (9–10 Wochen)
- [ ] Path III: 60h → 80h (8 Wochen)
- [ ] Gesamtzeit: **250–270 Stunden** (6–9 Monate bei 10h/Woche)

**Datei:** `lehrplan.md` → Sektion "Zeitplan" aktualisieren

---

## 2. Debugging & Chaos Quests einbauen

**Problem:** Fehlende Iterationsschleifen und reale Debugging-Szenarien.

**Lösung:** Alle 2–3 Module eine "Chaos Quest" ergänzen mit **echten** Fehlerquellen.

### 2.1 Chaos Quest nach Modul 3 (CI)

```markdown
## Chaos Quest: "Die kaputte Pipeline"

**Setup ohne direkte Fehlerangabe:**
- Erstelle eine CI-Pipeline mit pytest
- Nutze eine veraltete Python-Version im Container (3.8 statt 3.11)
- Führe Tests mit Dependencies aus, die Python 3.9+ erfordern

**Aufgabe:**
- Nach 2 Tagen: Pipeline läuft nicht mehr
- Debugging nur mit Logs, GitHub Actions Doku, pytest Doku
- Keine KI, keine fertigen Lösungen

**Lernziel:**
- Versionskonflikte erkennen
- CI-Logs richtig interpretieren
- Dependency-Management verstehen
```

**Datei:** Neue Datei `lehrpfad/chaos-quest-01-ci.md`

### 2.2 Chaos Quest nach Modul 5 (Kubernetes)

```markdown
## Chaos Quest: "Der mysteriöse Pod-Crash"

**Setup:**
- Deploye eine Anwendung mit Memory-Limit: 64MB (sollte 256MB sein)
- Setze Liveness-Probe auf `/healthz` (korrekter Pfad: `/health`)
- Health-Check-Timeout: 3s (realistisch: 10s)

**Aufgabe:**
- Warte 3 Tage, analysiere dann CrashLoopBackOff
- Nutze: `kubectl describe pod`, `kubectl logs`, `kubectl get events`
- Keine direkte Suche nach "CrashLoopBackOff fix"

**Lernziel:**
- OOMKilled vs. CrashLoopBackOff unterscheiden
- Resource Limits sinnvoll setzen
- Pod-Lifecycle verstehen
```

**Datei:** Neue Datei `lehrpfad/chaos-quest-02-k8s.md`

### 2.3 Chaos Quest nach Modul 7 (Ansible)

```markdown
## Chaos Quest: "Idempotenz-Illusion"

**Setup:**
- Erstelle ein Playbook, das eine Konfigurationsdatei deployed
- Nutze `copy` statt `template` für dynamische Werte
- Führe das Playbook 3x aus → Jedes Mal "changed"

**Aufgabe:**
- Analysiere, warum Idempotenz nicht funktioniert
- Fixe das Playbook ohne Copy-Paste von Ansible Galaxy

**Lernziel:**
- Idempotenz praktisch verstehen
- Ansible-Module richtig wählen
- Ansible-Output interpretieren
```

**Datei:** Neue Datei `lehrpfad/chaos-quest-03-ansible.md`

### 2.4 Chaos Quest nach Modul 10 (Security)

```markdown
## Chaos Quest: "Das abgelaufene Zertifikat"

**Setup:**
- Erstelle ein selbstsigniertes Zertifikat mit 7 Tagen Laufzeit
- Deploye einen Service, der TLS nutzt
- Konfiguriere KEIN automatisches Renewal

**Aufgabe:**
- Nach 7 Tagen: Service nicht erreichbar
- Debugging mit openssl, curl, kubectl/docker logs
- Implementiere ein Renewal-Skript oder Cert-Manager

**Lernziel:**
- Certificate Lifecycle verstehen
- TLS-Fehler debuggen
- Automatisierung von Security-Tasks
```

**Datei:** Neue Datei `lehrpfad/chaos-quest-04-security.md`

**Action Items:**
- [ ] 4 Chaos-Quest-Dateien erstellen
- [ ] In entsprechenden Modulen verlinken
- [ ] Quest-System aktualisieren (quest-path_I.md, quest-path_II.md, quest-path_III.md)

---

## 3. Lernjournal vereinfachen

**Problem:** Zu hoher Dokumentationsaufwand (10 Abschnitte pro Sitzung).

**Lösung:** Zwei Varianten anbieten:

### 3.1 Kurzversion (Standard)

```markdown
# Lernjournal – Modul XX (Kurz)

**Datum:** YYYY-MM-DD
**Modul:** XX
**Lernzeit:** Xh

## Was habe ich heute gelernt?

(2-3 Sätze)

## Welcher Fehler ist aufgetreten?

(Fehlermeldung + Kontext)

## Wie habe ich ihn gelöst?

(Lösungsweg in 3-5 Schritten)

## Nächster Schritt

- [ ] ...
```

### 3.2 Vollversion (für komplexe Module)

Aktuelles Template beibehalten, aber als optional markieren.

**Action Items:**
- [ ] `lernjournal/template-kurz.md` erstellen
- [ ] `lernjournal/template-voll.md` umbenennen (aktuelles template.md)
- [ ] In README.md beide Varianten erklären

---

## 4. Peer Learning & Self-Review

**Problem:** Kein echtes Teamfeedback oder Review-Mechanismus.

**Lösung:**

### 4.1 GitHub Discussions aktivieren

- [ ] GitHub Discussions im Repository aktivieren
- [ ] Kategorien anlegen:
  - 💬 Allgemein
  - 🆘 Hilfe & Debugging
  - 💡 Projektideen
  - 📢 Show & Tell

### 4.2 Self-Review-Checkliste

```markdown
## Self-Review Checkliste (nach jedem Modul)

- [ ] Kann ich das Projekt in 30 Min. aus dem Repo neu aufsetzen?
- [ ] Würde ein DevOps-Junior meine Dokumentation verstehen?
- [ ] Habe ich mindestens 3 eigene Fehler dokumentiert?
- [ ] Steht im README, WARUM ich Tool X statt Y gewählt habe?
- [ ] Funktioniert mein Setup nach 2 Wochen Pause noch?
```

**Datei:** Neue Datei `self-review-checkliste.md`

---

## 5. Show & Tell nach jedem Path

**Ziel:** Reflexion und Selbstsicherheit stärken.

**Umsetzung:**

### Template für Show & Tell

```markdown
# Show & Tell – Path I

## Was ich gebaut habe

(1-2 Absätze + Architekturdiagramm)

## Technologie-Stack

- Tool 1: Warum gewählt?
- Tool 2: Warum gewählt?
- ...

## Größter Lernmoment

(1 Absatz)

## Größter Fehler

Problem → Analyse → Lösung (3-5 Sätze)

## Was ich anders machen würde

(1-2 Verbesserungsideen)

## Nächste Schritte

(Ausblick auf Path II)
```

**Action Items:**
- [ ] Template erstellen: `show-and-tell-template.md`
- [ ] In jedem Quest-Path verlinken
- [ ] Optional: Video/Audio-Variante erwähnen

---

## 6. LERNREGELN.md erstellen

**Zweck:** Klare Prinzipien für authentisches Lernen ohne KI-Abhängigkeit.

```markdown
# Lernregeln

## 🚫 Nicht erlaubt während des Studiums

- KI-Tools (ChatGPT, Claude, Copilot) für Erklärungen oder Code-Generierung
- Copy-Paste von Lösungen ohne Verständnis
- Überspringen von Fehlermeldungen ("läuft ja irgendwie")
- Tutorial-Hopping ohne Projektabschluss

## ✅ Erlaubt und empfohlen

- Offizielle Dokumentationen (man pages, docs.docker.com, kubernetes.io)
- Stack Overflow (lesen, verstehen, **adaptieren** – nicht kopieren)
- YouTube-Tutorials (als Konzept-Einstieg, nicht als Lösung)
- Community-Foren (Reddit r/devops, Discord) für konzeptionelle Fragen
- Rubber Duck Debugging (laut erklären)

## 🎯 Die goldene Regel

**Wenn du es nicht erklären kannst, hast du es nicht verstanden.**

Jedes gelöste Problem = mindestens 3 Sätze Dokumentation:
1. Was war das Problem?
2. Wie habe ich es analysiert?
3. Warum funktioniert die Lösung?

## 📚 Lernprinzipien

### Verständnis vor Geschwindigkeit
- Kein Modul überspringen, weil "das kenne ich schon"
- Fehler sind Lernpunkte, keine Rückschläge
- Lieber 80% von allem als 100% von Modul 1

### Authentische Fehler
- Chaos Quests sind Pflicht, nicht optional
- Nach 2 Wochen Pause: Projekt neu starten → Was funktioniert nicht mehr?
- Debugging-Log führen: Fehler → Hypothese → Test → Ergebnis

### Dokumentation als Lernbeweis
- Jedes Modul endet mit einem Projektordner im Repo
- README mit: Setup-Anleitung, Architektur, 3 Learnings
- Screenshots/Logs von Fehlern und deren Lösung

## 🔄 Iteratives Lernen

- Nach jedem Path: 1 Woche Pause, dann Path-Review
- Alle 2 Monate: "Was würde ich jetzt anders machen?"
- Projekte aus früheren Modulen mit neuem Wissen verbessern
```

**Action Items:**
- [ ] `LERNREGELN.md` im Repository-Root erstellen
- [ ] In README.md unter "Nutzungsempfehlung" verlinken

---

## 7. Externe Ressourcen für echte Fehler

**Ziel:** Debugging üben ohne künstliche Breaks.

### Empfohlene Plattformen

```markdown
## Debugging-Ressourcen (in LERNREGELN.md ergänzen)

### Für Linux & Scripting (Modul 0-2)
- OverTheWire Bandit (overthewire.org/bandit)
- SadServers (sadservers.com) – kaputte Linux-Systeme reparieren

### Für Container & K8s (Modul 4-5)
- KillerCoda Kubernetes Scenarios
- K8s Debugging Labs (kubernetes.io/docs/tasks/debug/)

### Für Security (Modul 10)
- OWASP WebGoat
- HackTheBox (Anfänger-Challenges)

### Für Cloud (Modul 13)
- AWS Well-Architected Labs
- Terraform Troubleshooting (developer.hashicorp.com)
```

**Action Items:**
- [ ] Ressourcen-Sektion in LERNREGELN.md aufnehmen
- [ ] Bei Chaos Quests alternative externe Labs verlinken

---

## 8. Iterationsrhythmus & Versionierung

**Ziel:** Kontinuierliche Verbesserung des Curriculums.

### Versionierung

- Jede größere Anpassung → Git-Tag `v1.1`, `v1.2` etc.
- Changelog im Iteration Plan führen

### Review-Zyklen

- Nach Path I (ca. Monat 2): Struktur-Review
- Nach Path II (ca. Monat 4): Methodik-Review
- Nach Path III (ca. Monat 6): Gesamt-Review

### Feedback-Mechanismus

```markdown
## Feedback-Log (am Ende von iteration-plan.md)

### 2025-10-13
- Zeitschätzungen zu optimistisch → +30% Puffer
- Fehlen authentischer Debugging-Szenarien → Chaos Quests
- Lernjournal zu umfangreich → Kurzversion
```

**Action Items:**
- [ ] Changelog-Sektion in `iteration-plan.md` anlegen
- [ ] Git-Tag `v1.1` nach Abschluss dieser Iteration setzen

---

## 9. Priorisierung der Tasks

### Must Have (vor Start von Modul 0)
- [x] LERNREGELN.md erstellen
- [ ] Zeitplanung in lehrplan.md anpassen
- [ ] Lernjournal Kurzversion erstellen
- [ ] Self-Review-Checkliste anlegen

### Should Have (vor Path I Abschluss)
- [ ] Chaos Quest 01 (CI) erstellen
- [ ] GitHub Discussions aktivieren
- [ ] Show & Tell Template

### Nice to Have (iterativ)
- [ ] Chaos Quests 02-04
- [ ] Externe Debugging-Ressourcen sammeln
- [ ] Feedback-Log nach jedem Path

---

## 10. Changelog

### v1.1 (geplant 2025-10-14)
- ➕ Zeitplanung um 30-40% erhöht
- ➕ LERNREGELN.md hinzugefügt
- ➕ Lernjournal Kurzversion (template-kurz.md)
- ➕ Self-Review-Checkliste
- ➕ Chaos Quest Konzept (4 Quests geplant)
- ➕ Show & Tell Template
- ➕ GitHub Discussions als Kommunikationskanal

### v1.0 (2025-10-12)
- ✅ Initiales Curriculum (15 Module, 3 Paths)
- ✅ Quest-System mit XP-Tracking
- ✅ Lernjournal-Template (Vollversion)
- ✅ Ressourcen-Links kuratiert

---

📅 2025-10-13 01:15 | §iteration §planung §curriculum
