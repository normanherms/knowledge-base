# Modul 01 – Python-Automation

## Ziel

Grundverständnis für Skript- und API-Automatisierung entwickeln.
Dieses Modul baut auf den Shell- und Systemkenntnissen aus **Modul 00** auf und erweitert sie um Automatisierung mit **Python**.
Der Fokus liegt auf pragmatischer Skriptentwicklung, sauberem Code und API-Kommunikation im DevOps-Kontext.

---

## Lernorientierung

Ziel für Selbstlernende:
Python verstehen, Skripte schreiben, externe Datenquellen verarbeiten und Abläufe automatisieren.

Am Ende dieses Moduls solltest du:

1. Python-Code lesen, verstehen und erweitern können
2. Daten aus Dateien und APIs einlesen und verarbeiten
3. Skripte strukturiert und reproduzierbar ausführen
4. Code prüfen, testen und sauber dokumentieren

---

## Themenüberblick

| Bereich             | Lerninhalte & Schwerpunkte                                                        |
| ------------------- | --------------------------------------------------------------------------------- |
| Syntax & Strukturen | Datentypen, Variablen, Schleifen, Bedingungen, Funktionen, Module                 |
| Dateiverarbeitung   | CSV, JSON, YAML lesen und schreiben                                               |
| Netzwerk & APIs     | HTTP-Requests, REST-Prinzip, JSON-Parsing, Fehlerbehandlung                       |
| Systemautomation    | subprocess, os, Logging, ArgumentParser, CLI-Tools mit Typer                      |
| Testing & Linting   | pytest, black, flake8, saubere Formatierung und Stilprüfung                       |

> Orientierung: Inhalte decken die Python-Abschnitte der [DevOps-Roadmap auf roadmap.sh](https://roadmap.sh/devops) ab.

---

## Lernziele nach Themenfeld

### 1. Syntax & Strukturen

**Was lernen:**

- Aufbau eines Python-Skripts
- Datentypen (int, str, list, dict)
- Kontrollstrukturen (if, for, while)
- Funktionen, Module, Import-Struktur

**Wie lernen:**

- Mit der interaktiven REPL (`python3`) experimentieren
- Eigene Mini-Skripte schreiben und kommentieren

**Beispiele:**

- Schleife über eine Liste von Dateien
- Funktion zur Ausgabe von Systeminformationen

---

### 2. Dateiverarbeitung

**Was lernen:**

- Struktur von CSV-, JSON- und YAML-Dateien
- Lesen, Schreiben und Validieren von Inhalten

**Wie lernen:**

- Eigene Datenquelle (z. B. Logdateien oder Speedtest-Ergebnisse) verarbeiten
- Daten in ein neues Format umwandeln

**Beispiele:**

- JSON-Datei einlesen und Werte ausgeben
- YAML-Datei in CSV konvertieren

---

### 3. Netzwerk & APIs

**Was lernen:**

- Aufbau einer API (REST, Endpunkte, HTTP-Statuscodes)
- Datenabruf mit `requests`
- Parsing von JSON und Fehlerbehandlung

**Wie lernen:**

- Öffentliche APIs nutzen (z. B. OpenWeatherMap, GitHub, httpbin.org)
- Skript, das Daten abfragt und speichert

**Beispiele:**

- Wetterdaten abrufen und lokal speichern
- GitHub-Repo-Infos per Script abfragen

---

### 4. Systemautomation

**Was lernen:**

- Prozesse starten und steuern mit `subprocess`
- Dateisystemzugriff mit `os`
- Logging und ArgumentParser nutzen

**Wie lernen:**

- Skripte mit Parametern ausführen
- Logs für jede Ausführung speichern

**Beispiele:**

- Script, das `ping` ausführt und Ergebnisse loggt
- Backup-Prozess mit Logging und Exit-Codes

---

### 5. Testing & Linting

**Was lernen:**

- Grundlagen automatischer Tests mit `pytest`
- Codequalität mit `black` und `flake8` prüfen

**Wie lernen:**

- Einfache Unit-Tests schreiben
- Testausgabe und Formatierung im Terminal verstehen

**Beispiele:**

- Test für JSON-Verarbeitung
- Skriptformatierung mit `black .`

---

## Praxisprojekt

**Aufgabe:**
Ein Python-Skript liest Systeminformationen oder Logdaten aus und sendet sie per API oder Webhook an ein Zielsystem.
Das Skript läuft automatisch (Cron oder systemd), protokolliert Fehler und ist formatiert sowie getestet.

**Lernziel:**
Ein wartbares, robustes Automationsskript mit sauberem Code, Logging und Testabdeckung.

---

## Selbstreflexion

Am Ende solltest du beantworten können:

- Kann ich Python-Skripte modular aufbauen und wiederverwenden?
- Verstehe ich den Ablauf einer API-Kommunikation?
- Habe ich ein automatisiertes Skript mit Logging und Tests realisiert?

---

## Ressourcen (frei & geprüft)

| Kategorie | Format | Quelle / Beschreibung |
| ---------- | ------- | --------------------- |
| Python Grundlagen | Interaktiv | [PythonTutor](https://pythontutor.com) – visualisiert Code und Logikschritte |
| Syntax & Praxis | Text | [W3Schools Python Tutorial](https://www.w3schools.com/python/) – übersichtlich und praxisnah |
| Automation | Buch | [Automate the Boring Stuff](https://automatetheboringstuff.com) – freies Buch mit Praxisbeispielen |
| APIs & Requests | Artikel | [Real Python: API Integration](https://realpython.com/api-integration-in-python/) |
| Tests | Doku | [pytest Documentation](https://docs.pytest.org) |
| Linting & Format | Doku | [Black – Code Formatter](https://black.readthedocs.io) |
| DevOps-Integration | Video | [Python for DevOps – freeCodeCamp](https://www.youtube.com/watch?v=9s0ANx6Dwjc) (~2 h Grundlagen + Praxis) |
| Datenformate | Video | [JSON, CSV, YAML Explained – Tech With Tim](https://www.youtube.com/watch?v=9N6a-VLBa2I) (~20 min) |
| Podcast | Audio | [Talk Python To Me – Automate with Python](https://talkpython.fm/episodes/show/380) |

---

## Ergebnis

Am Ende von Modul 01 hast du:

- ein lauffähiges Python-Automationsskript,
- Verständnis für APIs, Datenformate und Prozesssteuerung,
- Logging, Testing und Linting implementiert,
- ein dokumentiertes Python-Repo mit klarer Struktur,
- die Grundlage für CI/CD-Integration (Modul 03).

---

**Weiterführend:** Modul 02 – Versionsverwaltung
**geändert am 2025-10-14**
