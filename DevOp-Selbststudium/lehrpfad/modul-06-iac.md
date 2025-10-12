# Modul 06 – Infrastruktur als Code

## Ziel

Verständnis und Anwendung von Infrastructure-as-Code-Konzepten.
Dieses Modul zeigt, wie Infrastruktur reproduzierbar, versionierbar und automatisiert bereitgestellt werden kann.

---

## Kerninhalte

| Bereich              | Themen                                            |
| -------------------- | ------------------------------------------------- |
| Grundlagen           | Deklarative vs. imperative Definitionen           |
| Tools                | Terraform, Pulumi, CloudFormation                 |
| Ressourcenmanagement | Provider, Module, State Files, Outputs            |
| Infrastrukturdesign  | Modularisierung, Wiederverwendbarkeit, Variablen  |
| Automatisierung      | CI/CD-Integration, Remote State, Secrets-Handling |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion     | Abgedeckt durch             | Status |
| ---------------------- | --------------------------- | ------ |
| infrastructure-as-code | Grundlagen, Terraform       | ✅      |
| terraform              | Terraform-Implementierung   | ✅      |
| pulumi                 | Alternative Toolchain       | ✅      |
| remote-state           | Terraform Cloud, S3 Backend | ✅      |
| automation             | CI/CD-Anbindung             | ✅      |

---

## Theoriephase

Ziel: Verständnis der IaC-Philosophie und Struktur.

* Prinzipien von Infrastructure as Code
* Aufbau einer Terraform-Konfiguration
* State-Management und Versionskontrolle
* Sicherheitsaspekte (z. B. Secrets, Variablen, Locking)
* Vergleich von Terraform und Pulumi

---

## Praxisphase

Ziel: Aufbau einer automatisierten Infrastruktur mit Terraform.

1. Installation und Grundkonfiguration von Terraform
2. Anlegen einer Infrastruktur (z. B. VM auf Netcup oder Hetzner Cloud)
3. Nutzung von Variablen, Outputs und Modulen
4. Versionierung der IaC-Konfiguration im Git-Repository
5. Einrichtung eines Remote States (z. B. S3 oder Terraform Cloud)
6. Automatisierung der Provisionierung über CI/CD

---

## Projektphase

Beispielprojekt:
Bereitstellung einer virtuellen Maschine oder eines K3s-Clusters per Terraform.
Optional: Anbindung an GitHub Actions zur automatischen Ausführung bei Merge.

Ziel: Reproduzierbare Infrastruktur, dokumentiert und automatisiert.

---

## Reviewphase

Reflexion:

* Ist meine Infrastruktur reproduzierbar und versionierbar?
* Nutze ich sinnvolle Modularisierung und Variablenstrukturen?
* Habe ich Sicherheitsaspekte (z. B. Secrets, State) berücksichtigt?

Empfohlene Tools zur Vertiefung:
Terraform, Pulumi, Terragrunt, tfsec, Infracost, Checkov

---

## Ressourcen

| Thema                | Quelle                                                                                                                                             |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Terraform Grundlagen | [https://developer.hashicorp.com/terraform](https://developer.hashicorp.com/terraform)                                                             |
| Pulumi               | [https://www.pulumi.com/docs/](https://www.pulumi.com/docs/)                                                                                       |
| Best Practices       | [https://www.terraform-best-practices.com/](https://www.terraform-best-practices.com/)                                                             |
| IaC Security         | [https://www.aquasec.com/wiki/display/KB/Infrastructure+as+Code+Security](https://www.aquasec.com/wiki/display/KB/Infrastructure+as+Code+Security) |
| State Management     | [https://developer.hashicorp.com/terraform/language/state](https://developer.hashicorp.com/terraform/language/state)                               |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Eine vollständige Terraform- oder Pulumi-Konfiguration im Repository
* Verständnis für State, Module und Remote Backends
* Automatisierte Infrastrukturbereitstellung über CI/CD
* Grundlage für Konfigurationsmanagement (Modul 07)

---

Nächster Schritt: Modul 07 – Konfigurationsmanagement

---

🕓 2025-10-12 21:38 | §devops §modul6 §terraform
