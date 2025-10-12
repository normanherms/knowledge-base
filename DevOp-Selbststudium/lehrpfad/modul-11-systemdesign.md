# Modul 11 – Systemdesign & Testing

## Ziel

Verständnis von Architekturprinzipien und Qualitätssicherung im DevOps-Kontext.
Dieses Modul verbindet Systemdesign, Skalierbarkeit und Testing zu einem ganzheitlichen Ansatz.

---

## Kerninhalte

| Bereich               | Themen                                            |
| --------------------- | ------------------------------------------------- |
| Architekturprinzipien | 12-Factor App, Microservices, Event-Driven Design |
| Systemdesign          | Skalierung, Hochverfügbarkeit, Redundanz          |
| Teststrategien        | Unit-, Integration-, Smoke-, Chaos-Tests          |
| Tools                 | pytest, k6, Postman, Litmus, curl                 |
| Qualitätsmetriken     | Code Coverage, Performance, Reliability           |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion        | Abgedeckt durch            | Status |
| ------------------------- | -------------------------- | ------ |
| system-design             | Architektur & Skalierung   | ✅      |
| testing                   | Testpyramide & Tools       | ✅      |
| chaos-engineering         | Litmus & Stresstests       | ✅      |
| quality-metrics           | Code Coverage, Performance | ✅      |
| observability-integration | Verbindung zu Modul 09     | 🔄     |

---

## Theoriephase

Ziel: Verständnis der strukturellen und qualitativen Anforderungen moderner Systeme.

* Aufbau skalierbarer und fehlertoleranter Systeme
* Bedeutung stateless Services und Entkopplung
* Testing-Pyramide und deren Anwendung im DevOps-Kontext
* Einführung in Chaos Engineering und Resilienztests
* Interpretation und Nutzung von Qualitätsmetriken

---

## Praxisphase

Ziel: Architektur analysieren, Tests automatisieren und Qualität sichtbar machen.

1. Analyse einer bestehenden Anwendung auf 12-Factor-Konformität
2. Aufbau automatischer Unit- und Integrationstests mit pytest
3. Durchführung von Smoke- und Performance-Tests mit k6
4. Einführung von Chaos-Tests mit Litmus oder Gremlin
5. Erfassung und Auswertung von Code Coverage und Performance-Daten
6. Dokumentation der Teststrategie im Repository

---

## Projektphase

Beispielprojekt:
Testgetriebene Überprüfung einer Microservice-Architektur mit automatischen Unit-, Integration- und Chaos-Tests.
Optional: Kombination mit CI/CD zur kontinuierlichen Qualitätsprüfung.

Ziel: Belastbares, getestetes Systemdesign mit messbarer Stabilität.

---

## Reviewphase

Reflexion:

* Ist mein Systemdesign modular, skalierbar und testbar?
* Sind Tests sinnvoll priorisiert und automatisiert?
* Kann ich die Systemqualität anhand von Metriken bewerten?

Empfohlene Tools zur Vertiefung:
pytest, Postman, k6, Litmus, Gremlin, Chaos Toolkit

---

## Ressourcen

| Thema                   | Quelle                                                                                                                         |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Systemdesign Grundlagen | [https://12factor.net](https://12factor.net)                                                                                   |
| Microservices           | [https://microservices.io](https://microservices.io)                                                                           |
| Testing-Pyramide        | [https://martinfowler.com/articles/practical-test-pyramid.html](https://martinfowler.com/articles/practical-test-pyramid.html) |
| Chaos Engineering       | [https://principlesofchaos.org](https://principlesofchaos.org)                                                                 |
| Performance Testing     | [https://k6.io/docs/](https://k6.io/docs/)                                                                                     |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Ein solides Verständnis für Systemdesign und Teststrategien
* Automatisierte Tests für Stabilität und Leistung
* Eine getestete Architektur mit dokumentierten Qualitätsmetriken
* Grundlage für Operations und Incident Management (Modul 12)

---

Nächster Schritt: Modul 12 – Operations & Incident Management

---

🕓 2025-10-12 22:24 | §devops §modul11 §testing
