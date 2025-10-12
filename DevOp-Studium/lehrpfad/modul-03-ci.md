# Modul 03 – Continuous Integration

## Ziel

Grundlagen der kontinuierlichen Integration verstehen und anwenden.
Dieses Modul führt in Build-, Test- und Integrationsprozesse ein und bildet die Basis für CI/CD.

---

## Kerninhalte

| Bereich          | Themen                                                   |
| ---------------- | -------------------------------------------------------- |
| Konzepte         | Continuous Integration, Build Automation, Test Pipelines |
| Tools            | GitHub Actions, GitLab CI, Jenkins, CircleCI             |
| Tests            | Unit-, Integration- und Lint-Tests automatisieren        |
| Artefakte        | Build-Artefakte, Caching, Dependency Management          |
| Benachrichtigung | E-Mail, Slack, Webhooks                                  |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion     | Abgedeckt durch           | Status |
| ---------------------- | ------------------------- | ------ |
| continuous-integration | Konzepte & Tools          | ✅      |
| ci-tools               | GitHub Actions, GitLab CI | ✅      |
| testing                | Tests & Linting           | ✅      |
| artifact-management    | Artefakte                 | ✅      |
| notification           | Benachrichtigung          | ✅      |

---

## Theoriephase

Ziel: Verständnis, warum CI zentral für DevOps ist.

* Bedeutung von Continuous Integration
* Build-Prozess und Testautomatisierung
* Pipeline-Struktur und Ausführungsumgebungen
* Integration von Linter, Unit-Tests und Code Coverage
* Artefakte und Caching-Strategien

---

## Praxisphase

Ziel: Eine funktionsfähige CI-Pipeline aufbauen.

1. Erstellung einer einfachen CI-Pipeline mit GitHub Actions oder GitLab CI
2. Automatische Tests bei jedem Push auf main oder dev
3. Nutzung von Linting und Code-Formatierung
4. Generierung und Upload von Build-Artefakten
5. Einbindung von Statusbadges und Benachrichtigungen
6. Dokumentation der Pipeline im Repository

---

## Projektphase

Beispielprojekt:
Eine CI-Pipeline, die ein Python- oder Bash-Projekt automatisch testet, formatiert und bei Erfolg ein Artefakt erzeugt.
Optional: Integration einer einfachen Slack- oder Mail-Benachrichtigung.

Ziel: Automatisierte Qualitätsprüfung und kontinuierliche Integration im Code-Workflow.

---

## Reviewphase

Reflexion:

* Wird der Code bei jeder Änderung überprüft?
* Funktioniert die Pipeline reproduzierbar?
* Werden Fehler rechtzeitig erkannt und gemeldet?

Empfohlene Tools zur Vertiefung:
GitHub Actions, GitLab CI, Jenkins, CircleCI, Drone CI

---

## Ressourcen

| Thema          | Quelle                                                                                                                       |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| CI Grundlagen  | [https://martinfowler.com/articles/continuousIntegration.html](https://martinfowler.com/articles/continuousIntegration.html) |
| GitHub Actions | [https://docs.github.com/actions](https://docs.github.com/actions)                                                           |
| Jenkins        | [https://www.jenkins.io/doc/](https://www.jenkins.io/doc/)                                                                   |
| GitLab CI      | [https://docs.gitlab.com/ee/ci/](https://docs.gitlab.com/ee/ci/)                                                             |
| CircleCI       | [https://circleci.com/docs](https://circleci.com/docs)                                                                       |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Eine lauffähige CI-Pipeline, die Code automatisch testet und prüft
* Verständnis für Build- und Testprozesse
* Eine stabile Grundlage für Continuous Delivery (Modul 08)
* Ein dokumentiertes Beispielprojekt im Git-Repository

---

Nächster Schritt: Modul 04 – Container & Virtualisierung

---

🕓 2025-10-12 21:10 | §devops §modul3 §ci
