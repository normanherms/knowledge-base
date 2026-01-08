# Ansible Cheatbook

---

## Anmerkung

Dies ist ein persönliches Cheatbook.
Es dient als Nachschlagewerk für meine eigenen Lerninhalte und erhebt keinen Anspruch auf Vollständigkeit.
Die Inhalte wurden teilweise mit Unterstützung von ChatGPT geglättet und ergänzt.
Auch wenn ich auf Richtigkeit achte, können Fehler enthalten sein.

---

## Einführung

- Ansible ist ein Open-Source Automatisierungstool
- wir können damit Systeme verwalten (Server, Clients usw.)
- [Dokumentation](https://docs.ansible.com)

---

## Architektur

- Control Node baut Verbindung zu den **Managed Nodes** auf (z. B. per SSH)
- dafür wichtig: zwei Files

  - Inventory (INI oder YAML) → Infos zu den Managed Nodes (IP, Hostname)
  - Playbook (YAML) → enthält Tasks, die auf den Nodes ausgeführt werden sollen

---

## YAML Kurzfassung

- Einrückung statt Klammern
- Leerzeichen, keine Tabs (Fehlerquelle Nr. 1)
- key: value
- Listen mit `-`
- Kommentare mit `#`
- Dateiendung: `.yml`

```yaml
---
- name: Paket installieren
  hosts: all
  tasks:
    - name: nginx installieren
      ansible.builtin.package:
        name: nginx
        state: present
```

---

## Use Cases

- mehrere Systeme gleichzeitig konfigurieren
- wiederholbare Automatisierung (Idempotenz)
- weniger manuelle Arbeit & direkte Logins
- Dokumentation und Versionskontrolle via Git
- agentless, basiert auf Python, skalierbar

## Inventory (INI-Variante)

- Einfachere Schreibweise, gut für kleine Tests
- Beispiel `inventory.ini`:

```ini
[dev]  
serv-dev ansible_host=10.10.10.10 ansible_user=testadmin  
```

- `[dev]` ist eine Hostgruppe (frei wählbar)
- `serv-dev` ist ein Alias für die Maschine
- `ansible_host` ist die IP oder der DNS-Name
- `ansible_user` der SSH-Benutzer

## Inventory (YAML-Variante)

```yaml
dev_env:                 # Gruppe (frei wählbarer Name)
  hosts:
    serv-dev:            # Host-Alias (frei wählbar)
      ansible_host: 10.10.10.10     # IP oder DNS-Name
      ansible_user: testadmin       # SSH-Benutzer
      ansible_password: passwort    # (nur für Tests, unsicher)
      ansible_port: 22              # optional, Standard ist 22
      ansible_ssh_private_key_file: ~/.ssh/id_rsa   # Pfad zum SSH-Key
      ansible_become: true          # root-Rechte via sudo
      ansible_become_method: sudo   # Methode (meist sudo)
      ansible_become_user: root     # Zieluser (meist root)
```

### Wichtigste Variablen im Inventory

- ansible_host → Ziel-IP oder Hostname
- ansible_user → SSH-Benutzername
- ansible_password → Passwort für SSH (nicht empfohlen, nur Test)
- ansible_port → Port für SSH (Standard: 22)
- ansible_ssh_private_key_file → Pfad zum privaten Key
- ansible_become → true, wenn sudo benötigt wird
- ansible_become_user → Ziel-User für sudo (Standard: root)
- ansible_become_method → Art von sudo (meist sudo, selten su)

Alltagsvergleich: Stelle dir das Inventory wie ein Adressbuch vor – es sagt Ansible, unter welcher Adresse und mit welchem Schlüssel es zu einer Maschine kommt.

---

## Ansible wichtige Argumente (für Einsteiger)

- -i   → gibt das Inventory an (Standard: /etc/ansible/hosts)
- -m  → welches Modul soll ausgeführt werden?

  - ping → prüft nur Erreichbarkeit + Python vorhanden
  - command → führt Befehle aus (z. B. -m command -a "uptime")
- -a  → Argumente für das Modul (z. B. Befehl für command)
- -k → Passwortabfrage für SSH erzwingen (nur wenn kein Key genutzt wird)
- -u  → User für SSH festlegen (falls nicht im Inventory angegeben)
- -K → fragt Sudo-Passwort ab (falls Playbook root-Rechte braucht)
- --list-hosts → zeigt, welche Hosts im Ziel sind
- --limit  → nur bestimmte Hosts/Gruppe ansprechen

---

## Inventory testen (Basics)

```bash
# Alle Hosts im Inventory anpingen  
ansible -i inventory.ini all -m ping  

# Nur Gruppe "dev" ansprechen  
ansible -i inventory.ini dev -m ping  

# Auf allen Hosts den Befehl "uptime" ausführen  
ansible -i inventory.ini all -m command -a "uptime"  

# Zeige welche Hosts angesprochen würden  
ansible -i inventory.ini all --list-hosts  
```

## Package Modul (apt/dnf)

- Funktion: Pakete installieren, aktualisieren, entfernen
- Module:

  - `ansible.builtin.apt` (Debian/Ubuntu)
  - `ansible.builtin.dnf` (Fedora/RHEL)

### Package Modul (apt/dnf) – Wichtige Parameter

- `name`: Paketname (oder Liste)
- `state`: present | absent | latest
- `update_cache`: ja/nein (apt: Paketindex aktualisieren)
- `upgrade`: yes | dist (apt: wie `apt upgrade` oder `apt full-upgrade`)

### Package Modul (apt/dnf) – Beispiel

```yaml
- name: nginx installieren
  ansible.builtin.apt:
    name: nginx
    state: present
    update_cache: yes
```

---

## Shell & Command Modul

- Funktion: Befehle direkt auf Zielsystem ausführen
- Module:

  - `ansible.builtin.command` → sicher, keine Shell (keine Pipes/Umleitungen)
  - `ansible.builtin.shell` → volle Shell, Pipes/Umleitungen möglich

### Shell & Command Modul – Wichtige Parameter

- `cmd` (bei command) oder direkt String
- `chdir`: Arbeitsverzeichnis setzen
- `creates`: führt nur aus, wenn Datei *nicht* existiert
- `removes`: führt nur aus, wenn Datei existiert

### Shell & Command Modul – Beispiel

```yaml
- name: uptime mit command
  ansible.builtin.command: uptime

- name: Ausgabe mit shell
  ansible.builtin.shell: echo "Hallo von $(hostname)" >> /tmp/info.txt
  chdir: /tmp
```

---

## File Modul

- Funktion: Dateien und Verzeichnisse verwalten
- Modul: `ansible.builtin.file`

### File Modul – Wichtige Parameter

- `path`: Pfad zur Datei/Verzeichnis
- `state`: file | directory | absent | touch | link | hard
- `mode`: Rechte (z. B. '0644')
- `owner`: Benutzer
- `group`: Gruppe

### File Modul – Beispiel

```yaml
- name: Verzeichnis anlegen
  ansible.builtin.file:
    path: /opt/testdir
    state: directory
    mode: '0755'

- name: Datei löschen
  ansible.builtin.file:
    path: /tmp/test.txt
    state: absent
```

---

## Benutzer und Gruppen Modul

- Funktion: User und Groups verwalten
- Module:

  - `ansible.builtin.user`
  - `ansible.builtin.group`

### Benutzer und Gruppen Modul – Wichtige Parameter (user)

- `name`: Benutzername
- `state`: present | absent
- `groups`: Zusatzgruppen (Liste)
- `append`: ja/nein (fügt Gruppen hinzu, überschreibt nicht)
- `shell`: Login-Shell
- `create_home`: ja/nein

### Benutzer und Gruppen Modul – Wichtige Parameter (group)

- `name`: Gruppenname
- `state`: present | absent

### Benutzer und Gruppen Modul – Beispiel

```yaml
- name: Benutzer anlegen
  ansible.builtin.user:
    name: testuser
    state: present
    groups: sudo
    shell: /bin/bash
    create_home: yes

- name: Gruppe anlegen
  ansible.builtin.group:
    name: devops
    state: present
```

---

## Service Modul (systemd/service)

- Funktion: Dienste starten, stoppen, aktivieren
- Module:

  - `ansible.builtin.service`
  - `ansible.builtin.systemd` (erweitert für systemd)

### Service Modul (systemd/service) – Wichtige Parameter

- `name`: Dienstname
- `state`: started | stopped | restarted | reloaded
- `enabled`: ja/nein (ob Dienst beim Booten startet)

### Service Modul (systemd/service) – Beispiel

```yaml
- name: nginx starten und aktivieren
  ansible.builtin.service:
    name: nginx
    state: started
    enabled: yes
```

---

## Variablen und deren Verwendung

- Definition: Variablen können im Inventory, Playbook oder über Extra-Args gesetzt werden
- Syntax im Playbook: `{{ variable_name }}`
- Arten von Variablen:

  - Inventory-Variablen (host_vars, group_vars)
  - Playbook-Variablen (vars)
  - Facts (automatisch gesammelte Systeminfos)
  - Extra-Variablen (`-e` beim Aufruf)

### Beispiel mit Variablen

```yaml
- name: Apache installieren
  hosts: web
  vars:
    web_package: apache2
  tasks:
    - name: Paket installieren
      ansible.builtin.apt:
        name: "{{ web_package }}"
        state: present
```

### Beispiel group_vars (Datei: group_vars/web.yml)

```yaml
web_package: apache2
```

Dann kann das Playbook dieselbe Variable nutzen, ohne sie im Playbook selbst zu definieren.

Alltagsvergleich: `group_vars` sind wie ein gemeinsamer Zettel an der Pinnwand – alle Hosts der Gruppe können die Info lesen, ohne dass man sie jedem einzeln in die Hand drückt.

---

## Debug Modul

- Funktion: Informationen oder Variablen ausgeben (zum Testen und Debugging)
- Modul: `ansible.builtin.debug`

### Debug Modul – Wichtige Parameter

- `msg`: gibt eine Nachricht aus
- `var`: gibt den Wert einer Variablen aus

### Debug Modul – Beispiel

```yaml
- name: Nachricht ausgeben
  ansible.builtin.debug:
    msg: "Playbook gestartet"

- name: Variable ausgeben
  ansible.builtin.debug:
    var: ansible_hostname
```

---

## Rollen und Projektstruktur

- Playbooks: enthalten Tasks
- Roles: bündeln wiederverwendbare Tasks, Variablen, Templates und Files
- Empfohlene Struktur (Best Practice):

```bash
projekt/
├── ansible.cfg
├── inventory.ini
├── playbook.yml
├── roles/
│   ├── common/
│   │   ├── tasks/
│   │   │   └── main.yml
│   │   ├── handlers/
│   │   │   └── main.yml
│   │   ├── templates/
│   │   ├── files/
│   │   └── vars/
│   │       └── main.yml
│   └── webserver/
│       └── tasks/
│           └── main.yml
```

- Vorteile: klare Trennung, Wiederverwendung, saubere Struktur

---

## Ansible Vault

- Funktion: sensible Daten verschlüsseln (Passwörter, Keys, Tokens)

- Befehle:

  - `ansible-vault create secrets.yml`
  - `ansible-vault edit secrets.yml`
  - `ansible-vault view secrets.yml`
  - `ansible-vault encrypt file.yml`
  - `ansible-vault decrypt file.yml`

- Nutzung im Playbook:

```yaml
- name: Geheimnisse einbinden
  hosts: all
  vars_files:
    - secrets.yml
  tasks:
    - name: Passwort debuggen
      ansible.builtin.debug:
        var: secret_password
```

- Extra-Args beim Ausführen:

  - `ansible-playbook playbook.yml --ask-vault-pass`
  - oder mit Passwortdatei: `--vault-password-file ~/.vault_pass.txt`

Alltagsvergleich: Vault ist wie ein Tresor – statt Passwörter im Klartext in die Playbooks zu schreiben, packst du sie verschlüsselt hinein und öffnest den Tresor nur bei Bedarf.

---

## Tasks validieren

- Syntaxprüfung: `ansible-playbook playbook.yml --syntax-check`
- Dry-Run: `ansible-playbook playbook.yml --check` (führt nichts aus, zeigt nur geplante Änderungen)
- List Tasks: `ansible-playbook playbook.yml --list-tasks`

Sinnvoll für: Fehler früh erkennen, ohne echte Änderungen durchzuführen.

---

## Troubleshooting und Debug

- Mehr Details: `-v`, `-vv`, `-vvv` für verschiedene Verbositätslevel
- Nur bestimmte Tasks ausführen: `--start-at-task "taskname"`
- Fehlerquellen: häufig fehlende Variablen, falsche Indentation, fehlende Module auf Zielsystem

Sinnvoll für: gezieltes Eingrenzen von Fehlern und bessere Nachvollziehbarkeit.

---

## Collections

- Funktion: bündeln Module, Plugins und Rollen
- Installation: `ansible-galaxy collection install <name>`
- Verwendung: `community.general.ping` statt nur `ping`

Sinnvoll für: Zugriff auf zusätzliche Funktionen und Community-Module.

---

## Tags

- Funktion: bestimmte Tasks markieren, selektiv ausführen
- Beispiel:

```yaml
- name: nginx installieren
  ansible.builtin.apt:
    name: nginx
    state: present
  tags: [web, nginx]
```

- Ausführen nur mit Tags: `ansible-playbook playbook.yml --tags web`

Sinnvoll für: gezielt nur einzelne Teile eines Playbooks laufen lassen, z. B. nur Webserver konfigurieren.

---

## Schleifen

- Funktion: wiederholte Ausführung über eine Liste, ähnlich wie eine Einkaufsliste, die du Punkt für Punkt abarbeitest.

```yaml
- name: mehrere Pakete installieren
  ansible.builtin.apt:
    name: "{{ item }}"
    state: present
  loop:
    - curl
    - git
    - vim
```

Sinnvoll für: statt drei einzelne Tasks für curl, git und vim zu schreiben, reicht ein Task mit einer Liste. Das spart Platz und macht Playbooks übersichtlicher.

---

## Bedingungen

- Funktion: Tasks nur unter bestimmten Bedingungen ausführen

```yaml
- name: nur auf Debian installieren
  ansible.builtin.apt:
    name: apache2
    state: present
  when: ansible_facts['os_family'] == "Debian"
```

Sinnvoll für: unterschiedliche Systeme oder Umgebungen flexibel handhaben.
