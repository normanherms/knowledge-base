# Modul 13 – Cloud & Skalierung

## Ziel

Verständnis von Cloud-Architekturen, Skalierung und Multi-Cloud-Strategien.
Dieses Modul zeigt, wie Infrastruktur elastisch und global betrieben werden kann.

---

## Kerninhalte

| Bereich              | Themen                                                 |
| -------------------- | ------------------------------------------------------ |
| Cloud-Grundlagen     | IaaS, PaaS, SaaS, Shared Responsibility Model          |
| Anbieter             | AWS, Azure, GCP, OpenStack                             |
| Skalierung           | Horizontal vs. Vertikal, Auto Scaling, Load Balancing  |
| Multi-Cloud          | Provider-übergreifende Strategien, Portabilität        |
| Kosten & Optimierung | Cloud-Kostenmanagement, Reservierungen, Spot-Instanzen |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion | Abgedeckt durch              | Status |
| ------------------ | ---------------------------- | ------ |
| cloud-providers    | AWS, Azure, GCP              | ✅      |
| scalability        | Auto Scaling, Load Balancing | ✅      |
| multi-cloud        | Strategien & Architektur     | ✅      |
| cost-optimization  | Monitoring & Reporting       | ✅      |
| automation         | Integration in IaC & CD      | 🔄     |

---

## Theoriephase

Ziel: Verständnis von Cloud-Konzepten und Skalierungsmechanismen.

* Unterschiede zwischen IaaS, PaaS und SaaS
* Überblick über große Anbieter und ihre Kernservices
* Skalierungsstrategien und Load Balancing
* Prinzipien von Multi-Cloud-Architekturen
* Kostenkontrolle und Cloud Governance

---

## Praxisphase

Ziel: Aufbau einer skalierbaren Cloud-Umgebung.

1. Erstellen eines Testprojekts auf AWS, Azure oder GCP
2. Deployment einer Anwendung mit Auto Scaling Group oder Managed Kubernetes
3. Einrichtung eines Load Balancers und Health Checks
4. Nutzung von Cloud Monitoring für Performance und Kosten
5. Vergleich verschiedener Provider-Ansätze
6. Dokumentation von Architektur und Skalierungsmechanismen im Repository

---

## Projektphase

Beispielprojekt:
Bereitstellung einer Web-App mit Load Balancer, Auto Scaling und Cloud Monitoring.
Optional: Kombination aus zwei Providern zur Demonstration einer Multi-Cloud-Strategie.

Ziel: Skalierbare, resiliente und kostenbewusste Cloud-Infrastruktur.

---

## Reviewphase

Reflexion:

* Ist meine Cloud-Architektur elastisch und wiederherstellbar?
* Habe ich Skalierung automatisiert und getestet?
* Sind Kosten und Ressourcen effizient verwaltet?

Empfohlene Tools zur Vertiefung:
AWS CLI, Azure CLI, gcloud, Terraform, Grafana Cloud, Lens

---

## Ressourcen

| Thema           | Quelle                                                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| AWS Grundlagen  | [https://aws.amazon.com/getting-started/](https://aws.amazon.com/getting-started/)                                             |
| Azure           | [https://learn.microsoft.com/en-us/azure/](https://learn.microsoft.com/en-us/azure/)                                           |
| Google Cloud    | [https://cloud.google.com/docs](https://cloud.google.com/docs)                                                                 |
| OpenStack       | [https://docs.openstack.org/](https://docs.openstack.org/)                                                                     |
| Cloud Economics | [https://cloud.google.com/architecture/cloud-cost-optimization](https://cloud.google.com/architecture/cloud-cost-optimization) |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Eine funktionierende Cloud-Umgebung mit Auto Scaling und Monitoring
* Verständnis von Cloud-Strukturen und Verantwortlichkeiten
* Grundlagen für Multi-Cloud-Architekturen und Governance
* Grundlage für Spezialisierungen und Trends (Modul 14)

---

Nächster Schritt: Modul 14 – Spezialisierungen & Trends

---

🕓 2025-10-12 22:42 | §devops §modul13 §cloud
