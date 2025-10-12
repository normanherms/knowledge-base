# Modul 05 – Orchestrierung & Cluster

## Ziel

Verständnis und Aufbau von Container-Orchestrierungssystemen.
Dieses Modul führt in Kubernetes und verwandte Tools ein und legt den Grundstein für skalierbare Deployments.

---

## Kerninhalte

| Bereich               | Themen                                      |
| --------------------- | ------------------------------------------- |
| Kubernetes-Grundlagen | Pods, Deployments, Services, Namespaces     |
| Architektur           | Control Plane, Nodes, Scheduler, API Server |
| Ressourcenverwaltung  | YAML-Definitionen, ConfigMaps, Secrets      |
| Tools                 | kubectl, k9s, Helm, K3s                     |
| Erweiterungen         | Service Mesh, Ingress, Autoscaling          |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion      | Abgedeckt durch   | Status |
| ----------------------- | ----------------- | ------ |
| container-orchestration | Kubernetes        | ✅      |
| kubernetes-basics       | Pods, Deployments | ✅      |
| helm                    | Helm Charts       | ✅      |
| service-mesh            | Grundlagen        | ✅      |
| scaling                 | Autoscaling       | ✅      |

---

## Theoriephase

Ziel: Verständnis der Architektur und Funktionsweise von Kubernetes.

* Komponenten der Control Plane und Worker Nodes
* Aufbau von YAML-Ressourcen
* Kommunikation im Cluster (Pod-Netzwerke, Services, DNS)
* Helm als Paketmanager für Kubernetes
* Grundlagen von Service Mesh und Observability

---

## Praxisphase

Ziel: Aufbau und Verwaltung eines funktionierenden Clusters.

1. Installation eines K3s- oder Minikube-Clusters
2. Deployment einer Beispielanwendung (z. B. Nginx oder Flask)
3. Verwaltung mit kubectl (get, apply, describe, logs)
4. Nutzung von Namespaces und Ressourcenlimits
5. Erstellung und Nutzung eines Helm-Charts
6. Test eines einfachen Autoscalers (HPA)
7. Dokumentation der YAML-Definitionen im Repository

---

## Projektphase

Beispielprojekt:
Bereitstellung einer mehrschichtigen Anwendung (Frontend, Backend, Datenbank) im Kubernetes-Cluster.
Optional: Einsatz von Helm für Installation und Updates.

Ziel: Verständnis für skalierbare, selbstheilende Containerumgebungen.

---

## Reviewphase

Reflexion:

* Kann ich die Hauptkomponenten eines Clusters erklären?
* Verstehe ich den Unterschied zwischen Deployment, Pod und Service?
* Habe ich meine Ressourcen logisch strukturiert und versioniert?

Empfohlene Tools zur Vertiefung:
kubectl, k9s, Helm, Lens, Okteto, Kind, K3s

---

## Ressourcen

| Thema                 | Quelle                                                                                                 |
| --------------------- | ------------------------------------------------------------------------------------------------------ |
| Kubernetes Grundlagen | [https://kubernetes.io/docs/home/](https://kubernetes.io/docs/home/)                                   |
| K3s                   | [https://docs.k3s.io/](https://docs.k3s.io/)                                                           |
| Helm                  | [https://helm.sh/docs/](https://helm.sh/docs/)                                                         |
| Service Mesh          | [https://istio.io/latest/about/service-mesh/](https://istio.io/latest/about/service-mesh/)             |
| Monitoring            | [https://prometheus.io/docs/introduction/overview/](https://prometheus.io/docs/introduction/overview/) |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Einen lauffähigen Kubernetes-Cluster (lokal oder remote)
* Verständnis für Deployments, Services und Scaling
* Ein Helm-basiertes Deployment-Projekt im Git-Repository
* Grundlage für Infrastructure as Code (Modul 06)

---

Nächster Schritt: Modul 06 – Infrastruktur als Code

---

🕓 2025-10-12 21:28 | §devops §modul5 §kubernetes
