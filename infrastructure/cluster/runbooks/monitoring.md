# Runbook Monitoring Baseline

Node Exporter, Prometheus, Grafana

## Scope

Minimalistisches Infrastruktur Monitoring zur Überwachung.

Ziele:

- Sichtbarkeit aller Nodes
- Reboot stabil
- Keine offenen internen Services
- Keine Optimierung, kein Alerting, kein Tuning

Komponenten:

- Node Exporter auf allen Nodes
- Prometheus zentral auf dash
- Grafana lokal auf dash, nicht öffentlich

---

## Architektur

Nodes liefern Metriken ausschließlich über WireGuard an dash.

Netz:

- WireGuard 10.99.99.0/24
- Firewall Default DROP

---

## Node Exporter Installation

### Download und Ablage

```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.10.2/node_exporter-1.10.2.linux-amd64.tar.gz
tar xvfz node_exporter-*.tar.gz
sudo mkdir /usr/local/bin/node_exporter
sudo mv node_exporter-1.10.2.linux-amd64/* /usr/local/bin/node_exporter
rm -rf node_exporter-1.10.2.linux-amd64*
```

### System User

```bash
sudo useradd --system --no-create-home --shell /usr/sbin/nologin node_exporter
sudo chown root:root /usr/local/bin/node_exporter/node_exporter
sudo chmod 755 /usr/local/bin/node_exporter/node_exporter
```

---

## Node Exporter systemd Unit

Datei:

```bash
/etc/systemd/system/node_exporter.service
```

Inhalt:

```ini
[Unit]
Description=Prometheus Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
ExecStart=/usr/local/bin/node_exporter/node_exporter \
  --web.listen-address=<WG-IP>:9100
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Aktivieren:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now node_exporter
```

---

## Firewall Regel Node Exporter

Datei:

```bash
/etc/nftables.conf
```

Relevanter Abschnitt:

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

        tcp dport 9100 iifname "wg0" accept
    }
}
```

Reload:

```bash
sudo systemctl restart nftables
```

---

## Node Exporter Verifikation

Listening:

```bash
sudo ss -ltnp | grep 9100
```

Remote Test:

```bash
curl http://<WG-IP>:9100/metrics
```

Erwartung:

- HTTP 200
- Metrics Output

---

## Prometheus Installation auf dash

### Download und Ablage Prometheus

```bash
wget https://github.com/prometheus/prometheus/releases/download/v3.8.1/prometheus-3.8.1.linux-amd64.tar.gz
tar xvfz prometheus-*.tar.gz
sudo mkdir /usr/local/bin/prometheus
sudo mv prometheus-3.8.1.linux-amd64/* /usr/local/bin/prometheus
rm -rf prometheus-3.8.1.linux-amd64*
```

### System User und Verzeichnisse

```bash
sudo useradd --system --no-create-home --shell /usr/sbin/nologin prometheus
sudo mkdir /etc/prometheus /var/lib/prometheus
sudo chown -R root:prometheus /etc/prometheus
sudo chown -R prometheus:prometheus /var/lib/prometheus
sudo chmod 750 /etc/prometheus /var/lib/prometheus
```

---

## Prometheus Konfiguration

Datei:

```bash
/etc/prometheus/prometheus.yml
```

Inhalt:

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: node_exporter
    static_configs:
      - targets:
          - 10.99.99.1:9100
          - 10.99.99.2:9100
          - 10.99.99.3:9100
          - 10.99.99.4:9100
```

Validierung:

```bash
sudo /usr/local/bin/prometheus/promtool check config /etc/prometheus/prometheus.yml
```

---

## Prometheus systemd Unit

Datei:

```bash
/etc/systemd/system/prometheus.service
```

Inhalt:

```ini
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
ExecStart=/usr/local/bin/prometheus/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/var/lib/prometheus \
  --web.listen-address=127.0.0.1:9090
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Aktivieren:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now prometheus
```

---

## Prometheus Verifikation

```bash
ss -ltnp | grep 9090
curl http://127.0.0.1:9090/-/healthy
curl -s http://127.0.0.1:9090/api/v1/targets | grep -E '"health"|"scrapeUrl"'
```

Erwartung:

- Alle Targets health up

---

## Grafana Installation

```bash
sudo apt-get install -y apt-transport-https gpg
sudo mkdir -p /etc/apt/keyrings/
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
sudo apt-get update
sudo apt-get install grafana
```

---

## Grafana Bindung absichern

Datei:

```bash
/etc/grafana/grafana.ini
```

```ini
[server]
http_addr = 127.0.0.1
http_port = 3000
```

Restart:

```bash
sudo systemctl restart grafana-server
```

---

## Grafana Verifikation

```bash
sudo ss -ltnp | grep 3000
curl http://127.0.0.1:3000
curl -I http://127.0.0.1:3000/login
journalctl -u grafana-server --since "5 min ago" --no-pager
```

---

## Sicherheitsstatus

- Node Exporter nur über WireGuard erreichbar
- Prometheus nur localhost
- Grafana nur localhost
- Keine offenen Monitoring Ports
- Reboot stabil

---

## Status

Monitoring Baseline abgeschlossen
Dokumentiert
Reproduzierbar
Produktionsreif als Fundament
