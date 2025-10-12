# Modul 10 – Sicherheit & DevSecOps

## Ziel

Verständnis und Umsetzung sicherer Entwicklungs- und Betriebsprozesse.
Dieses Modul zeigt, wie Sicherheit integraler Bestandteil jeder Phase der Pipeline wird.

---

## Kerninhalte

| Bereich               | Themen                                               |
| --------------------- | ---------------------------------------------------- |
| Sicherheitsprinzipien | Least Privilege, Defense in Depth, RBAC              |
| Secrets Management    | HashiCorp Vault, Key Rotation, Zugriffskontrolle     |
| Code Security         | Static & Dynamic Analysis, SBOM, Dependency Scanning |
| Supply Chain Security | Signaturen, Container-Scanning, Provenance           |
| Compliance & Auditing | Logging, Policies, IAM                               |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion | Abgedeckt durch       | Status |
| ------------------ | --------------------- | ------ |
| security-basics    | Prinzipien & RBAC     | ✅      |
| secrets-management | Vault, Rotation       | ✅      |
| code-analysis      | SAST, DAST            | ✅      |
| container-security | Scanning & Signaturen | ✅      |
| compliance         | Audit & IAM           | ✅      |

---

## Theoriephase

Ziel: Verständnis der Sicherheitskonzepte und deren Umsetzung in DevOps.

* Bedeutung von DevSecOps im Lebenszyklus
* Prinzipien sicherer Softwareentwicklung
* Umgang mit Identitäten, Rollen und Berechtigungen
* Schutz sensibler Daten (z. B. Secrets, Tokens, Zertifikate)
* Überblick über SBOM (Software Bill of Materials)

---

## Praxisphase

Ziel: Integration von Sicherheit in bestehende Workflows.

1. Einrichtung von Secrets Management (Vault, GitHub Secrets)
2. Implementierung von Code Scans (z. B. Trivy, Bandit, Snyk)
3. Container-Images auf Schwachstellen prüfen
4. Nutzung von SBOMs zur Nachvollziehbarkeit von Abhängigkeiten
5. Aufbau eines Audit-Logs für Änderungen und Deployments
6. Test von RBAC-Regeln in Kubernetes oder GitOps-Systemen

---

## Projektphase

Beispielprojekt:
Integration eines Security-Scans in die CI/CD-Pipeline inklusive Container-Analyse und Vault-basierter Secret-Verwaltung.
Optional: Erstellung einer automatisierten Sicherheitsdokumentation.

Ziel: Nachweislich sichere Pipeline mit überprüfbaren Policies.

---

## Reviewphase

Reflexion:

* Sind alle Secrets sicher gespeichert und versioniert?
* Werden Schwachstellen regelmäßig erkannt und gemeldet?
* Ist mein Zugriffskonzept nachvollziehbar und minimal gehalten?

Empfohlene Tools zur Vertiefung:
HashiCorp Vault, Trivy, Snyk, Anchore, Open Policy Agent, Falco

---

## Ressourcen

| Thema                 | Quelle                                                                                   |
| --------------------- | ---------------------------------------------------------------------------------------- |
| DevSecOps Grundlagen  | [https://owasp.org/www-community/DevSecOps](https://owasp.org/www-community/DevSecOps)   |
| Vault                 | [https://developer.hashicorp.com/vault/docs](https://developer.hashicorp.com/vault/docs) |
| Container Security    | [https://aquasecurity.github.io/trivy](https://aquasecurity.github.io/trivy)             |
| Supply Chain Security | [https://slsa.dev](https://slsa.dev)                                                     |
| Policy Enforcement    | [https://www.openpolicyagent.org](https://www.openpolicyagent.org)                       |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Ein integriertes Security-Konzept innerhalb deiner CI/CD-Pipeline
* Sicheren Umgang mit Secrets und Berechtigungen
* Tools zur kontinuierlichen Schwachstellenanalyse
* Grundlage für Auditing und Incident Response (Modul 12)

---

Nächster Schritt: Modul 11 – Systemdesign & Testing

---

🕓 2025-10-12 22:15 | §devops §modul10 §security
