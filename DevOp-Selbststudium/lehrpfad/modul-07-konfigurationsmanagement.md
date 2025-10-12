# Modul 07 – Konfigurationsmanagement

## Ziel

Einrichtung und Verwaltung von Systemkonfigurationen mit deklarativen Tools.
Dieses Modul zeigt, wie Systeme konsistent und automatisiert konfiguriert werden.

---

## Kerninhalte

| Bereich               | Themen                                              |
| --------------------- | --------------------------------------------------- |
| Grundlagen            | Idempotenz, Deklarativ vs. Imperativ, Desired State |
| Tools                 | Ansible, Puppet, Chef                               |
| Inventare & Variablen | Gruppen, Hosts, Templates                           |
| Playbooks & Rollen    | Wiederverwendbare Automatisierung                   |
| Sicherheit            | Vault, Secrets, SSH, Rollenbasierte Zugriffe        |

---

## Abgleich mit roadmap.sh/devops

| roadmap.sh-Sektion       | Abgedeckt durch           | Status |
| ------------------------ | ------------------------- | ------ |
| configuration-management | Ansible, Puppet, Chef     | ✅      |
| ansible                  | Playbooks, Inventare      | ✅      |
| automation               | Rollen, Templates         | ✅      |
| security                 | Vault & SSH               | ✅      |
| orchestration            | Verbindung zu IaC & CI/CD | 🔄     |

---

## Theoriephase

Ziel: Verständnis, wie Konfigurationsmanagement-Tools Systeme steuern.

* Unterschiede zwischen IaC und Konfigurationsmanagement
* Prinzipien der Idempotenz
* Aufbau eines Ansible-Playbooks
* Struktur von Inventaren und Variablen
* Sicherheit und Geheimnishandling (Ansible Vault, SSH-Agenten)

---

## Praxisphase

Ziel: Systeme automatisiert konfigurieren.

1. Installation von Ansible auf der Management-Node
2. Definition eines Inventars mit mehreren Hosts
3. Erstellung eines Playbooks zur Paketinstallation und Service-Konfiguration
4. Nutzung von Templates und Variablen
5. Testen der Idempotenz (mehrfache Ausführung ohne Änderung)
6. Einsatz von Ansible Vault für Secrets
7. Dokumentation der Playbooks im Repository

---

## Projektphase

Beispielprojekt:
Erstelle eine automatisierte Systemkonfiguration für einen Webserver-Stack (z. B. Nginx + Firewall + User Setup).
Optional: Nutzung von Rollen für Wiederverwendbarkeit.

Ziel: Vollautomatisierte, wiederholbare Systemkonfiguration.

---

## Reviewphase

Reflexion:

* Habe ich verstanden, wie Idempotenz funktioniert?
* Kann ich Playbooks logisch strukturieren und debuggen?
* Ist meine Konfiguration sicher und wiederholbar?

Empfohlene Tools zur Vertiefung:
Ansible, Molecule, Ansible Lint, Puppet Bolt, Chef Workstation

---

## Ressourcen

| Thema              | Quelle                                                                                                                         |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| Ansible Grundlagen | [https://docs.ansible.com/ansible/latest/user_guide/index.html](https://docs.ansible.com/ansible/latest/user_guide/index.html) |
| Puppet             | [https://puppet.com/docs/puppet/latest/puppet_index.html](https://puppet.com/docs/puppet/latest/puppet_index.html)             |
| Chef               | [https://docs.chef.io/](https://docs.chef.io/)                                                                                 |
| Sicherheit         | [https://docs.ansible.com/ansible/latest/user_guide/vault.html](https://docs.ansible.com/ansible/latest/user_guide/vault.html) |
| Best Practices     | [https://galaxy.ansible.com](https://galaxy.ansible.com)                                                                       |

---

## Ergebnis

Am Ende dieses Moduls hast du:

* Ein funktionierendes Ansible-Setup mit Inventar und Playbooks
* Verständnis für Idempotenz und Zustandsverwaltung
* Eine sichere, dokumentierte Automatisierungsbasis
* Grundlage für Continuous Delivery (Modul 08)

---

Nächster Schritt: Modul 08 – Continuous Delivery / Deployment

---

🕓 2025-10-12 21:47 | §devops §modul7 §ansible
