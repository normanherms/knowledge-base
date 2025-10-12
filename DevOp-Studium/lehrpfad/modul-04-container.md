# Modul 04 – Container & Virtualisierung

## Ziel

Verständnis und praxisnahe Anwendung von Containertechnologien.
Dieses Modul vermittelt den Einsatz von Docker und verwandten Tools als Grundlage für Orchestrierung und Deployment.

---

## Kerninhalte

| Bereich              | Themen                                           |
| -------------------- | ------------------------------------------------ |
| Container-Konzepte   | Images, Container, Volumes, Netzwerke            |
| Docker-Grundlagen    | Docker CLI, Dockerfiles, Container Lifecycle     |
| Docker Compose       | Multi-Container-Umgebungen, YAML-Konfiguration   |
| Container-Sicherheit | User-Rechte, Image-Scanning, Minimal-Images      |
| Virtualisierung      | Hypervisor, KVM, LXC, Unterschiede zu Containern |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion   | Abgedeckt durch              | Status |
| -------------------- | ---------------------------- | ------ |
| containers           | Docker & Compose             | ✅      |
| virtualization       | KVM & LXC Grundlagen         | ✅      |
| container-security   | Image-Scanning & User-Rechte | ✅      |
| container-networking | Compose-Netzwerke            | ✅      |
| container-registry   | Vorbereitung auf Modul 05    | 🔜     |

---

## Theoriephase

Ziel: Verständnis von Containerprinzipien und Isolation.

* Unterschied zwischen virtuellen Maschinen und Containern
* Architektur von Docker und OCI (Open Container Initiative)
* Aufbau eines Dockerfiles und Schichtenmodell (Layer)
* Funktionsweise von Volumes und Netzwerken
* Sicherheitsaspekte und Best Practices

---

## Praxisphase

Ziel: Eigene Container-Umgebung aufbauen und verwalten.

1. Installation von Docker Engine oder Podman
2. Erstellung eines eigenen Dockerfiles für eine kleine Web-App
3. Aufbau einer Multi-Container-Umgebung mit Docker Compose
4. Nutzung von Volumes für persistente Daten
5. Konfiguration eines eigenen Netzwerks zwischen Containern
6. Testen und Stoppen von Containern mit CLI-Kommandos
7. Dokumentation der Konfiguration und Logs in Markdown

---

## Projektphase

Beispielprojekt:
Bereitstellung einer einfachen Webanwendung (z. B. Nginx oder Flask) über Docker Compose mit separaten Services für App und Datenbank.
Optional: Integration eines Reverse Proxy.

Ziel: Funktionsfähige, reproduzierbare Containerumgebung als Basis für spätere Cluster (Modul 05).

---

## Reviewphase

Reflexion:

* Verstehe ich den Unterschied zwischen VM und Container?
* Kann ich Container starten, stoppen und vernetzen?
* Ist mein Dockerfile effizient und sicher aufgebaut?

Empfohlene Tools zur Vertiefung:
Docker Desktop, Portainer, Dive, Hadolint, Podman, Nerdctl

---

## Ressourcen

| Thema             | Quelle                                                                                         |
| ----------------- | ---------------------------------------------------------------------------------------------- |
| Docker Grundlagen | [https://docs.docker.com/get-started/](https://docs.docker.com/get-started/)                   |
| Docker Compose    | [https://docs.docker.com/compose/](https://docs.docker.com/compose/)                           |
| Podman            | [https://podman.io/](https://podman.io/)                                                       |
| Sicherheit        | [https://snyk.io/learn/docker-security-basics/](https://snyk.io/learn/docker-security-basics/) |
| OCI Spezifikation | [https://opencontainers.org/](https://opencontainers.org/)                                     |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Eine lauffähige Containerumgebung mit Docker oder Podman
* Verständnis für Images, Volumes und Netzwerke
* Ein eigenes Compose-Projekt im Repository
* Grundlage für Kubernetes und Orchestrierung (Modul 05)

---

Nächster Schritt: Modul 05 – Orchestrierung & Cluster

---

🕓 2025-10-12 21:19 | §devops §modul4 §docker
