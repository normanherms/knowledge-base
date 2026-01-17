# Cluster Changelog

Das Changelog dient zur Übersicht der Arbeit am Cluster.

---

*Template:*

## YYYY-MM-DD - Titel

**Was:** Beschreibung der Änderung
**Wo:** Welcher Server
**Warum:** Grund/Motivation
**Auswirkung:** Technische Konsequenzen
**Fix:** Fixes und Issue Behebung

---

## 2026-01-17 - Baseline: Security Layer aktiv

**Was:** nftables, Fail2ban und auditd Baseline Rules aktiviert und geprüft. Host Inventare für alle Nodes erstellt.
**Wo:** mirror, load, prod, dash
**Warum:** Einheitlicher Security Standard vor DRBD und K3s Deployment.
**Auswirkung:** Nur SSH ist extern erreichbar, Fail2ban blockt SSH Bots via nftables, kritische Config Dateien werden auditiert, Baseline ist dokumentiert und vergleichbar.

## 2026-01-16 - Dokumentation

**Was:** Dokumentation reviewed und erweitert
**Warum:** Dokumentation meiner Aufbauphase
**Auswirkung:** Bessere Nachvollziehbarkeit was gemacht oder geändert wurde

## 2026-01-14 2/2 - Baseline: Storage Layout

**Was:** Einheitliches Storage-Layout eingerichtet und persistent eingebunden.
**Wo:** mirror, load, prod
**Warum:** Reproduzierbare Basis für Cluster, DRBD und sauberes Recovery.
**Auswirkung:** Logisches Standardlayout gewählt (256 GB)

- /root 64 GB
- swap 8 GB
- /cont 8 GB
- /data 128 GB
- /backup ~48 GB

Abweichungen:

- load: /root 128 GB, /data 64 GB (Control Plane, kein DRBD)
- mirror: physisch 1 TB, logisch erstmal auf 256 GB begrenzt

## 2026-01-14 1/2 - Baseline: User & SSH

**Was:** Einheitlicher Admin User angelegt, SSH gehärtet und System aktualisiert.
**Wo:** mirror, load, prod
**Warum:** Grundlage für einen konsistenten und sicheren Cluster Betrieb.
**Auswirkung:** Zentraler, abgesicherter SSH Zugriff auf allen Nodes.

## 2026-01-06 – Baseline & Monitoring Basis sowie Daily Backups

**Was:** Aufbau einer minimalen Monitoring Basis mit Node Exporter und Prometheus sowie Einführung eines Daily Backups
**Wo:** dash
**Warum:** Frühzeitige Beobachtbarkeit und Absicherung der Konfigurationen
**Auswirkung:** Neue Systemdienste aktiv, zusätzliche Ports nur lokal gebunden, tägliche Backup Jobs per Cron
