# Runbook WireGuard Full Mesh Setup mit systemd Autostart und nftables

---

## Scope

Aufbau eines WireGuard Full Mesh zwischen mehreren Linux Nodes
Optionaler NAT Node wird unterstützt
Restriktive Firewall mit nftables
Bootfester Autostart via systemd

---

## Voraussetzungen

- Debian oder kompatible Distribution
- Root Zugriff
- systemd aktiv
- nftables aktiv

---

## 1. Installation

```bash
sudo apt update
sudo apt install wireguard -y
````

---

## 2. Key Management

### Key Verzeichnis anlegen

```bash
sudo mkdir -p /etc/wireguard/keys
sudo chmod 700 /etc/wireguard/keys
```

---

### Keypaar pro Node erzeugen

```bash
sudo wg genkey \
| sudo tee /etc/wireguard/keys/private_$HOSTNAME.key \
| wg pubkey \
| sudo tee /etc/wireguard/keys/public_$HOSTNAME.key
```

---

### Rechte setzen

```bash
sudo sh -c 'chmod 600 /etc/wireguard/keys/private_*.key'
sudo sh -c 'chmod 644 /etc/wireguard/keys/public_*.key'
```

---

## 3. WireGuard Konfiguration

Datei:

```bash
sudo nano /etc/wireguard/wg0.conf
```

### Template

```ini
[Interface]
PrivateKey = <PRIVATE_KEY>
Address = <WG_IP>/24
ListenPort = 51820
```

```ini
[Peer]
# Peer A
PublicKey = <PUBLIC_KEY_A>
AllowedIPs = <WG_IP_A>/32
Endpoint = <PUBLIC_IP_A>:51820
PersistentKeepalive = 25
```

```ini
[Peer]
# Peer B
PublicKey = <PUBLIC_KEY_B>
AllowedIPs = <WG_IP_B>/32
Endpoint = <PUBLIC_IP_B>:51820
PersistentKeepalive = 25
```

```ini
[Peer]
# Peer C (NAT Node)
PublicKey = <PUBLIC_KEY_C>
AllowedIPs = <WG_IP_C>/32
PersistentKeepalive = 25
```

Hinweis
Für NAT Nodes wird kein Endpoint gesetzt
Der NAT Node initiiert alle Verbindungen selbst

---

### Dateirechte setzen

```bash
sudo chown root:root /etc/wireguard/wg0.conf
sudo chmod 600 /etc/wireguard/wg0.conf
```

---

## 4. Firewall Vorbereitung (nftables)

Vor dem Testen muss der WireGuard Port freigegeben sein

Datei:

```bash
sudo nano /etc/nftables.conf
```

### Minimal restriktive Konfiguration

```nft
table inet filter {

    chain input {
        type filter hook input priority 0;
        policy drop;

        iif lo accept
        ct state established,related accept

        ip protocol icmp accept
        ip6 nexthdr icmpv6 accept

        tcp dport 22 accept

        udp dport 51820 ct state new accept
    }

    chain forward {
        type filter hook forward priority 0;
        policy drop;
    }

    chain output {
        type filter hook output priority 0;
        policy accept;
    }
}
```

---

### Firewall laden

```bash
sudo nft -c -f /etc/nftables.conf
sudo systemctl reload nftables
```

---

## 5. WireGuard Testbetrieb

### Status prüfen

```bash
sudo wg show
ip route show | grep wg0
```

---

### Konnektivität testen

```bash
ping <WG_IP_A>
ping <WG_IP_B>
ping <WG_IP_C>
```

Erwartung
Alle Peers erreichbar
RX und TX Zähler steigen

---

## 6. Autostart aktivieren

```bash
sudo systemctl enable wg-quick@wg0
```

Optional sofort starten falls noch nicht aktiv:

```bash
sudo systemctl start wg-quick@wg0
```

Status prüfen:

```bash
systemctl status wg-quick@wg0
```

Hinweis
active exited ist der korrekte Zustand für wg quick

---

## 7. Reboot Test

```bash
sudo reboot
```

Nach dem Reboot prüfen:

```bash
sudo systemctl status wg-quick@wg0
sudo wg show wg0
```

Erwartung
Interface vorhanden
Handshakes aktiv
Kein manueller Eingriff nötig

---

## Status

- WireGuard Full Mesh aktiv
- NAT Nodes korrekt integriert
- Firewall restriktiv und funktionsfähig
- Autostart bootfest
- Setup produktionsbereit

## Nächste Ausbaustufen

### Ausbaustufe 1 – PreUp und PostUp Hooks

Ziel
Deterministischer Zustand beim Start von WireGuard.

Mögliche Maßnahmen

- nftables Regeln bei jedem Start erzwingen
- sysctl Werte explizit setzen
- wg0 nur starten, wenn Abhängigkeiten valide sind

Beispiele

- PreUp nftables Syntax prüfen und laden
- PreUp sysctl net.ipv4.ip_forward explizit setzen
- PostUp Logging des Interface Starts

Nutzen

- kein Konfigurationsdrift
- reproduzierbares Verhalten nach Reboot

---

### Ausbaustufe 2 – Trennung der Traffic Klassen

Ziel
Saubere Trennung von Rollen im WireGuard Netz.

Mögliche Maßnahmen

- separate WireGuard IPs oder Netze für Storage Traffic
- dedizierte AllowedIPs für DRBD oder K3s Kommunikation
- optionale MTU Feinjustierung je Traffic Klasse

Nutzen

- bessere Fehlersuche
- klare Verantwortlichkeiten im Netzwerk

---

### Ausbaustufe 3 – Monitoring und Observability

Ziel
Sichtbarkeit des WireGuard Zustands.

Mögliche Maßnahmen

- Monitoring der Handshake Zeiten
- Alerting bei Peer Ausfall
- Export von wg show Metriken

Nutzen

- frühzeitige Fehlererkennung
- höhere Betriebssicherheit

---

### Ausbaustufe 4 – Deklarative Verwaltung

Ziel
Vollständige Reproduzierbarkeit ohne manuelle Schritte.

Mögliche Maßnahmen

- Ansible Rollen für WireGuard
- deklarative Firewall Definition
- versionierte Konfigurationsstände

Nutzen

- schnelle Wiederherstellung
- saubere Dokumentation
- weniger manuelle Fehler

---

### Ausbaustufe 5 – Erweiterte Sicherheitsmechanismen

Ziel
Defense in Depth für das WireGuard Setup.

Mögliche Maßnahmen

- Rate Limiting für WireGuard UDP
- zusätzliche nftables Logging Regeln
- geregeltes Key Rotation Verfahren

Nutzen

- höhere Resilienz
- bessere Nachvollziehbarkeit
- langfristige Wartbarkeit
