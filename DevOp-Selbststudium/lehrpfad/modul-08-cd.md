# Modul 08 – Continuous Delivery / Deployment

## Ziel

Verständnis und Umsetzung von Continuous Delivery und Deployment.
Dieses Modul baut auf CI und Konfigurationsmanagement auf und zeigt, wie Anwendungen automatisiert ausgeliefert werden.

---

## Kerninhalte

| Bereich     | Themen                                                |
| ----------- | ----------------------------------------------------- |
| Konzepte    | CI/CD-Zusammenhang, Pipeline-Stufen, Deployment-Arten |
| Strategien  | Blue/Green, Canary, Rolling, Feature Flags            |
| Tools       | ArgoCD, Flux, GitHub Actions, GitLab CD               |
| Sicherheit  | Secret Management, Rollback, Change Control           |
| Integration | Verbindung zu IaC und Monitoring                      |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion     | Abgedeckt durch             | Status |
| ---------------------- | --------------------------- | ------ |
| continuous-delivery    | Deployment-Konzepte         | ✅      |
| deployment-strategies  | Blue/Green, Canary          | ✅      |
| gitops                 | ArgoCD, Flux                | ✅      |
| rollback               | Versionierung & Safety Nets | ✅      |
| monitoring-integration | Übergang zu Modul 09        | 🔜     |

---

## Theoriephase

Ziel: Verständnis, wie Software sicher und automatisiert in Produktion gebracht wird.

* Abgrenzung von Continuous Integration, Delivery und Deployment
* Pipeline-Architektur: Build, Test, Deploy
* Deployment-Strategien im Detail
* GitOps-Prinzipien: deklarative Steuerung per Repository
* Rollbacks und Sicherheit im Release-Prozess

---

## Praxisphase

Ziel: Aufbau einer vollständigen CI/CD-Pipeline mit Deployment.

1. Erweiterung der bestehenden CI-Pipeline um Delivery-Stufen
2. Nutzung von GitHub Actions oder GitLab CI/CD für Deployment
3. Automatisches Deployment in Test- oder Staging-Umgebungen
4. Implementierung von Canary- oder Blue/Green-Strategie
5. Optional: Einführung eines GitOps-Tools (z. B. ArgoCD)
6. Dokumentation der Pipeline, Trigger und Rollback-Mechanismen

---

## Projektphase

Beispielprojekt:
Automatisierte Bereitstellung einer Container-basierten Anwendung über CI/CD mit Canary-Rollout und automatischer Validierung.
Optional: Verbindung mit Monitoring und Alerting.

Ziel: Vollständig automatisierte, sichere Delivery-Pipeline mit Rückfallmechanismus.

---

## Reviewphase

Reflexion:

* Funktioniert mein Deployment reproduzierbar und sicher?
* Habe ich eine sinnvolle Trennung von Umgebungen umgesetzt?
* Kann ich ein Rollback manuell oder automatisch ausführen?

Empfohlene Tools zur Vertiefung:
ArgoCD, Flux, Spinnaker, GitHub Actions, GitLab CD, Jenkins X

---

## Ressourcen

| Thema                 | Quelle                                                                                                             |
| --------------------- | ------------------------------------------------------------------------------------------------------------------ |
| CI/CD Grundlagen      | [https://www.thoughtworks.com/continuous-integration](https://www.thoughtworks.com/continuous-integration)         |
| GitOps                | [https://www.weave.works/technologies/gitops/](https://www.weave.works/technologies/gitops/)                       |
| Deployment-Strategien | [https://martinfowler.com/bliki/BlueGreenDeployment.html](https://martinfowler.com/bliki/BlueGreenDeployment.html) |
| ArgoCD                | [https://argo-cd.readthedocs.io/en/stable/](https://argo-cd.readthedocs.io/en/stable/)                             |
| Flux                  | [https://fluxcd.io/docs/](https://fluxcd.io/docs/)                                                                 |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Eine funktionierende Continuous Delivery Pipeline
* Verständnis verschiedener Deployment-Strategien
* Eine GitOps-basierte Steuerung deines Deployments
* Verbindung zu Monitoring und Alerting (Modul 09)

---

Nächster Schritt: Modul 09 – Monitoring & Observability

---

🕓 2025-10-12 21:56 | §devops §modul8 §cicd
