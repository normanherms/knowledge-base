# DevOps Lehrplan (Basierend auf roadmap.sh/devops)

## Struktur

Der Lehrplan gliedert sich in 15 Module. Jedes Modul baut auf dem vorherigen auf und kombiniert Theorie mit praktischen Übungen.

| Nr. | Modul                            | Inhalt                                                |
| --- | -------------------------------- | ----------------------------------------------------- |
| 0   | Grundlagen & Einstieg            | Linux, CLI, Netzwerke, Scripting, DevOps-Mindset      |
| 1   | Python-Automation                | Python-Grundlagen, API-Nutzung, Automatisierung       |
| 2   | Versionsverwaltung               | Git, Branching, Pull Requests, Workflows              |
| 3   | Continuous Integration           | Buildtools, CI-Server, Testautomatisierung            |
| 4   | Container & Virtualisierung      | Docker, Containerfiles, Compose                       |
| 5   | Orchestrierung & Cluster         | Kubernetes, Helm, Service Mesh                        |
| 6   | Infrastruktur als Code           | Terraform, Pulumi, IaC-Konzepte                       |
| 7   | Konfigurationsmanagement         | Ansible, Puppet, Chef, Idempotenz                     |
| 8   | Continuous Delivery / Deployment | Deployment-Strategien, Blue/Green, Canary             |
| 9   | Monitoring & Observability       | Prometheus, Grafana, ELK, Tracing                     |
| 10  | Sicherheit & DevSecOps           | Secrets, Scanner, Supply Chain Security, Vault        |
| 11  | Systemdesign & Testing           | Architekturprinzipien, 12-Factor App, QA, Chaos Tests |
| 12  | Operations & Incident Management | On-Call, Alerts, Postmortems, Runbooks                |
| 13  | Cloud & Skalierung               | AWS, GCP, Azure, Load Balancing, Multi-Cloud          |
| 14  | Spezialisierungen & Trends       | GitOps, Platform Engineering, MLOps, Serverless       |

---

## Modul 0 – Grundlagen & Einstieg

**Ziel:** Verständnis, wie Systeme technisch und organisatorisch zusammenarbeiten. Fundament für alle folgenden Module.

| Bereich                       | Inhalte                                                      |
| ----------------------------- | ------------------------------------------------------------ |
| **Linux & CLI**               | Shell, Dateisysteme, Prozesse, Rechte, Systemd, Paketmanager |
| **Netzwerk-Basics**           | TCP/IP, DNS, HTTP/S, Routing, Firewalls, Ports               |
| **Scripting**                 | Bash, Python-Basics, Automatisierung kleiner Aufgaben        |
| **Betriebssystemverständnis** | Kernel, Logs, Ressourcen, Services                           |
| **DevOps-Mindset**            | Kultur, Kollaboration, Feedback, CALMS-Modell                |
| **Toolchain-Basis**           | VS Code, GitHub, SSH, curl, jq, nc, dig                      |

Ergebnis: lauffähige Linux-Umgebung mit funktionierender Toolchain und erstem Automationsskript (z. B. Backup- oder Log-Rotation-Skript).

---

## Modul 1 – Python-Automation

**Ziel:** Grundverständnis für Skript- und API-Automatisierung.

| Bereich                 | Inhalte                                 |
| ----------------------- | --------------------------------------- |
| **Syntax & Strukturen** | Datentypen, Schleifen, Bedingungen      |
| **Dateiverarbeitung**   | CSV, JSON, YAML einlesen und schreiben  |
| **Netzwerk & APIs**     | Requests, REST, JSON-Parsing            |
| **Systemautomation**    | subprocess, os, Logging, ArgumentParser |
| **Testing & Linting**   | pytest, black, flake8                   |

Ergebnis: eigenes Python-Skript zur Automatisierung eines DevOps-Prozesses (z. B. Logauswertung oder API-Monitoring).

---

## Zeitplan (6 Monate)

Ein realistischer Plan bei paralleler Berufstätigkeit mit wöchentlichen Lernphasen (5–10 Stunden).

| Monat | Module | Ziele                                                         |
| ----- | ------ | ------------------------------------------------------------- |
| 1     | 0–2    | Grundlagen Linux, Python & Git-Workflow praktisch anwenden    |
| 2     | 3–4    | CI/CD-Basis aufbauen, erste Pipelines und Docker-Container    |
| 3     | 5–6    | Kubernetes-Grundlagen, Terraform-Infrastruktur provisionieren |
| 4     | 7–8    | Automatisierte Konfiguration, Deployment-Strategien umsetzen  |
| 5     | 9–11   | Monitoring, Testing, Security und Design integrieren          |
| 6     | 12–14  | Operations, Cloud, Spezialisierungen & Abschlussprojekt       |

---

## Lernarchitektur & Methodik

**Lernmodus:** Kombination aus 30 % Theorie und 70 % Praxis.
**Iteratives Lernen:** Inhalte zyklisch wiederholen, nicht linear abarbeiten.
**Reflexion:** Nach jedem Modul kurze Retrospektive („Was lief gut, was unklar?“).
**Dokumentation:** Alle Projekte in Markdown dokumentieren (Screens, Logs, Erklärungen).
**Austausch:** Code-Review- oder Feedback-Simulation pro Modul.

---

## Systemdesign & Testing

| Bereich                | Inhalte                                                              |
| ---------------------- | -------------------------------------------------------------------- |
| **Architekturdenken**  | 12-Factor App, stateless Systeme, Microservices, Event-Driven Design |
| **Testing-Pyramide**   | Unit-, Integration-, Smoke-, Chaos-Tests                             |
| **Toolchain**          | pytest, curl, k6, Litmus                                             |
| **Qualitätssicherung** | Linting, CI-Teststufen, Metrik-Auswertung                            |

Ergebnis: getestete, resiliente Systeme mit nachvollziehbaren Qualitätsmetriken.

---

## DevSecOps & Operations

| Bereich                 | Inhalte                                      |
| ----------------------- | -------------------------------------------- |
| **Security-Prinzipien** | Least Privilege, RBAC, IAM, SBOM             |
| **Secrets-Management**  | HashiCorp Vault, Rotation, Zugriffskontrolle |
| **Incident Response**   | Alerts, On-Call, Runbooks, Postmortems       |
| **Observability**       | Logs, Metriken, Tracing, Alert-Routing       |

Ergebnis: Betriebssichere Systeme mit dokumentierten Notfallprozessen und Security-Checks.

---

## Lernpfad-Erweiterung & Zertifikate

**Ziel:** Orientierung für Spezialisierungen oder Zertifizierungen.

| Richtung             | Empfohlene Zertifikate                                         |
| -------------------- | -------------------------------------------------------------- |
| **Cloud**            | AWS Certified Cloud Practitioner, GCP Associate Cloud Engineer |
| **Kubernetes**       | CKA, CKAD                                                      |
| **Automation**       | Red Hat Ansible Automation Expert                              |
| **Security**         | CompTIA Security+, HashiCorp Vault Associate                   |
| **DevOps allgemein** | Linux Foundation DevOps Bootcamp, GitLab Certified Associate   |

---

## Projekt-Portfolio

| Abschnitt      | Projektidee                                                 |
| -------------- | ----------------------------------------------------------- |
| Grundlagen     | Bash- oder Python-Skript (Logrotation, Backup)              |
| Git/CI         | Automatischer Build & Test über GitHub Actions              |
| Container      | Web-App mit Docker Compose                                  |
| IaC            | Terraform-Infrastruktur für Testsystem                      |
| Orchestrierung | Mini-K3s-Cluster lokal aufsetzen                            |
| Monitoring     | Prometheus + Grafana Dashboard                              |
| Security       | Vault-Integration für Secrets                               |
| Abschluss      | End-to-End CI/CD Workflow (Code → Build → Deploy → Monitor) |

---

## Fortschritts-Tracking

* **Self-Assessments:** Fragen am Modulende („Kann ich ...?“)
* **Kompetenzmatrix:** 0 = keine Ahnung, 1 = verstanden, 2 = geübt, 3 = sicher
* **Automatisierte Reports:** Fortschritt z. B. via GitHub Action dokumentieren
* **Review-Checklisten:** Einheitliche Qualitätskriterien pro Modul

---

## Lernstruktur pro Modul

**1. Theoriephase** – zentrale Begriffe, kurze Zusammenfassung
**2. Praxisphase** – Mini-Projekte und Übungen
**3. Projektphase** – eigenes Modulprojekt
**4. Reviewphase** – Feedback, Analyse, Vertiefung

---

## Ressourcen (Auswahl)

* **Grundlagen:** Linux Journey, OverTheWire Bandit, Bash Academy
* **Python:** Automate the Boring Stuff, Real Python, API Tutorials
* **Git & GitHub:** Pro Git (Buch), Atlassian Git Tutorials
* **CI/CD:** GitHub Actions, GitLab CI, Jenkins Doku
* **Container:** Docker Docs, Play with Docker, Katacoda Labs
* **IaC:** Terraform Doku, HashiCorp Learn
* **Kubernetes:** Kubernetes.io Tutorials, K3s Docs
* **Monitoring:** Prometheus.io, Grafana Labs, Elastic Stack Guide
* **DevSecOps:** OWASP, Trivy, Snyk Academy, Vault Docs
* **Testing:** pytest, k6, Litmus Chaos Engineering
* **Cloud:** AWS Free Tier Labs, Google Qwiklabs

---

## Kontrollmechanismen

* Nach jedem Modul:

  * Wissenscheck (Quiz oder Aufgabenblatt)
  * Review des Modulprojekts
  * Feedback-Notiz für Verbesserungen

* Nach jedem zweiten Modul:

  * **Zwischenprojekt:** Kleine End-to-End-Pipeline (Code → Build → Deploy → Monitor)

* Abschlussprojekt nach Monat 6:

  * Vollständiger DevOps-Workflow mit CI/CD, IaC, Security-Checks und Monitoring-Dashboard.

---

## Fortschrittsbewertung

| Bewertungskriterium   | Beschreibung                             |
| --------------------- | ---------------------------------------- |
| Konzeptverständnis    | Theoretische Klarheit der Prinzipien     |
| Anwendung             | Praktische Umsetzung der Tools           |
| Automatisierung       | Grad der Automatisierung & Dokumentation |
| Sicherheit            | Secure-by-Design-Prinzipien umgesetzt    |
| Monitoring & Feedback | Sichtbarkeit & Wartbarkeit               |

---

## Lernumgebung & Tooling

* Einheitliche Umgebung: Debian 13 / Fedora / Ubuntu LTS
* Tools: VS Code, Docker, Git, Terraform, Ansible, kubectl, Helm, Vault
* Einheitliche Repo-Struktur: `mod01_python`, `mod02_git`, `mod03_ci`
* Automatisierte Setup-Skripte (z. B. Ansible)
* Dokumentation versioniert im Git-Repo

---

TZ=Europe/Berlin | Datum 2025-10-12 19:45 | §DevOps §Lehrplan §Curriculum
