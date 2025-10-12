# Modul 09 – Monitoring & Observability

## Ziel

Verständnis und Aufbau von Überwachungs- und Analysesystemen.
Dieses Modul vermittelt, wie Systeme messbar, nachvollziehbar und proaktiv beobachtet werden können.

---

## Kerninhalte

| Bereich           | Themen                               |
| ----------------- | ------------------------------------ |
| Monitoring        | Metriken, Logs, Events               |
| Observability     | Tracing, Correlation, Dashboards     |
| Tools             | Prometheus, Grafana, Loki, ELK Stack |
| Logging & Tracing | OpenTelemetry, Jaeger, Loki          |
| Alarmierung       | Alerts, Webhooks, Incident Response  |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion | Abgedeckt durch        | Status |
| ------------------ | ---------------------- | ------ |
| monitoring         | Prometheus, Grafana    | ✅      |
| logging            | Loki, ELK              | ✅      |
| tracing            | Jaeger, OpenTelemetry  | ✅      |
| alerting           | Alertmanager, Webhooks | ✅      |
| observability      | Gesamtkonzept          | ✅      |

---

## Theoriephase

Ziel: Verständnis der Prinzipien von Monitoring und Observability.

* Unterschied zwischen Monitoring und Observability
* Sammeln und Auswerten von Metriken und Logs
* Architektur moderner Monitoring-Stacks
* Aufbau von Dashboards und Alarmregeln
* Integration in CI/CD- und Deployment-Prozesse

---

## Praxisphase

Ziel: Aufbau einer Monitoring-Infrastruktur.

1. Installation und Konfiguration von Prometheus und Grafana
2. Erfassung von Systemmetriken (Node Exporter, cAdvisor)
3. Aufbau eines Dashboards für Cluster- und App-Überwachung
4. Integration von Logging mit Loki oder ELK
5. Einrichtung von Alarmen mit Alertmanager
6. Tracing-Setup mit OpenTelemetry oder Jaeger
7. Dokumentation der Metriken, Dashboards und Alerts im Repository

---

## Projektphase

Beispielprojekt:
Erstelle ein vollständiges Monitoring-Setup für eine Webanwendung inklusive Dashboards, Logs und Alarmierung.
Optional: Integration mit CI/CD zur automatischen Prüfung nach Deployment.

Ziel: Vollständige Transparenz über Systemzustand und Performance.

---

## Reviewphase

Reflexion:

* Sehe ich Probleme im System, bevor sie kritisch werden?
* Habe ich sinnvolle Metriken und Schwellenwerte definiert?
* Ist mein Monitoring wartbar und erweiterbar aufgebaut?

Empfohlene Tools zur Vertiefung:
Prometheus, Grafana, Loki, Jaeger, Alertmanager, OpenTelemetry Collector

---

## Ressourcen

| Thema                 | Quelle                                                                                                 |
| --------------------- | ------------------------------------------------------------------------------------------------------ |
| Prometheus Grundlagen | [https://prometheus.io/docs/introduction/overview/](https://prometheus.io/docs/introduction/overview/) |
| Grafana               | [https://grafana.com/docs/](https://grafana.com/docs/)                                                 |
| Loki                  | [https://grafana.com/oss/loki/](https://grafana.com/oss/loki/)                                         |
| OpenTelemetry         | [https://opentelemetry.io/docs/](https://opentelemetry.io/docs/)                                       |
| ELK Stack             | [https://www.elastic.co/what-is/elk-stack](https://www.elastic.co/what-is/elk-stack)                   |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Eine funktionierende Monitoring- und Logging-Umgebung
* Verständnis für Metriken, Logs und Traces
* Dashboards und Alarme zur proaktiven Systemüberwachung
* Grundlage für DevSecOps und Incident Management (Modul 10/12)

---

Nächster Schritt: Modul 10 – Sicherheit & DevSecOps

---

🕓 2025-10-12 22:06 | §devops §modul9 §monitoring
