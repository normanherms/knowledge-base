# Modul 01 – Python-Automation

## Ziel

Grundverständnis für Skript- und API-Automatisierung.
Dieses Modul erweitert die Grundlagenarbeit aus Modul 00 und führt in die praktische Automatisierung mit Python ein.

---

## Kerninhalte

| Bereich             | Themen                                                  |
| ------------------- | ------------------------------------------------------- |
| Syntax & Strukturen | Datentypen, Variablen, Schleifen, Bedingungen           |
| Dateiverarbeitung   | Einlesen und Schreiben von CSV-, JSON- und YAML-Dateien |
| Netzwerk & APIs     | HTTP-Requests, REST, JSON-Parsing                       |
| Systemautomation    | subprocess, os, Logging, ArgumentParser                 |
| Testing & Linting   | pytest, black, flake8                                   |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion | Abgedeckt durch             | Status |
| ------------------ | --------------------------- | ------ |
| python-scripting   | Syntax & Strukturen         | ✅      |
| working-with-apis  | Netzwerk & APIs             | ✅      |
| automation         | Systemautomation            | ✅      |
| testing            | Testing & Linting           | ✅      |
| version-control    | Git-Integration vorbereitet | 🔜     |

---

## Theoriephase

Ziel: Verständnis grundlegender Python-Konzepte und deren Einsatz im DevOps-Kontext.

* Aufbau und Syntax der Sprache Python
* Unterschied zwischen Skripten und Modulen
* Umgang mit Bibliotheken und virtuellen Umgebungen
* Grundlagen der API-Kommunikation (GET, POST, JSON)
* Logging und Fehlerbehandlung für stabile Skriptausführung

---

## Praxisphase

Ziel: Eigene Automatisierungsskripte erstellen und testen.

1. Installation von Python 3 und Pip
2. Einrichtung einer virtuellen Umgebung mit venv
3. Schreiben eines Skripts zur API-Abfrage (z. B. Wetterdaten, GitHub API)
4. Nutzung von os und subprocess zur Systemsteuerung
5. Formatierung und Test des Codes mit black und pytest
6. Dokumentation der Skripte und Ausgaben in Markdown

---

## Projektphase

Beispielprojekt:
Ein Python-Skript, das Systemlogs oder Statusdaten regelmäßig ausliest, über eine API versendet oder in eine Datei schreibt.
Optional: Benachrichtigung per E-Mail oder Webhook.

Ziel: Vollautomatisierter Prozess mit Fehlerbehandlung und Logging.

---

## Reviewphase

Reflexion:

* Kann ich API-Daten verarbeiten und auswerten?
* Nutze ich Funktionen und Module effizient?
* Erfüllt mein Skript die Prinzipien sauberer Automatisierung?

Empfohlene Tools zur Vertiefung:
requests, json, logging, black, pytest, typer

---

## Ressourcen

| Thema             | Quelle                                                                                                 |
| ----------------- | ------------------------------------------------------------------------------------------------------ |
| Python Grundlagen | [https://www.python.org/about/gettingstarted/](https://www.python.org/about/gettingstarted/)           |
| API Nutzung       | [https://realpython.com/api-integration-in-python/](https://realpython.com/api-integration-in-python/) |
| Automatisierung   | [https://automatetheboringstuff.com](https://automatetheboringstuff.com)                               |
| Testing           | [https://docs.pytest.org](https://docs.pytest.org)                                                     |
| Linting           | [https://black.readthedocs.io](https://black.readthedocs.io)                                           |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Ein funktionierendes Python-Skript zur Prozess- oder API-Automatisierung
* Verständnis für Logging, Testing und Fehlerbehandlung
* Eine saubere, dokumentierte Python-Umgebung im Git-Repository
* Grundlage für die Integration in CI/CD-Pipelines (Modul 03)

---

Nächster Schritt: Modul 02 – Versionsverwaltung

---

🕓 2025-10-12 20:49 | §devops §modul1 §python
