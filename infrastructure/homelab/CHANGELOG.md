# Homelab Changelog

Das Changelog dient zur Übersicht der Arbeit am Homelab.

Hinweis: Die Deployments aus Ende 2025 wurden nicht im Changelog erfasst. Einige Einträge enthalten daher nur Monatsangaben (XX) und wurden nachträglich rekonstruiert oder weggelassen. Den aktuellen Stand kann man im [Inventory](/infrastructure/homelab/inventory/edge.md) finden.

---

*Template:*

### YYYY-MM-DD - Titel

**Was:** Beschreibung der Änderung
**Wo:** Welcher Server
**Warum:** Grund/Motivation
**Auswirkung:** Technische Konsequenzen
**Fix:** Fixes und Issue Behebung
**Referenz:** Link oder Pfad zur Doku oder ähnlichem

---

### 2026-01-12 - Debian upgrade

**Was:** Debian upgrade zu Kernel 6.12.63 und Debian zu 6.13
**Wo:** edge
**Warum:** Kernel Update, Sicherheit
**Auswirkung:** Reboot
**Fix:** Nach dem Reboot ist Wiki.js in einen Restart Loop gelaufen. Ursache war, dass der Wiki.js Container gestartet ist, bevor die PostgreSQL Datenbank bereit war. Zusätzlich hat die Logging Einstellung `logging: driver: none` unter `containerd` Probleme verursacht. Behoben durch einen Healthcheck für PostgreSQL und eine feste Startabhängigkeit in der Compose Datei.

---

### 2026-01-11 - Dokumentation Repository erstellt

**Was:** Komplette Homelab Dokumentation als strukturiertes Repository aufgebaut
**Wo:** Dokumentation
**Warum:** Vorher nur fragmentierte Dokuschnipsel, keine zentrale Struktur
**Auswirkung:** System ist nachvollziehbar und übergabefähig

---

### 2025-12-XX - Anytype Self Hosted Deployment

**Was:** Anytype Stack deployed (Multi Container Setup)
**Wo:** edge
**Warum:** Self hosted Notion Alternative
**Auswirkung:** Multi Container Stack aktiv

---

### 2025-12-XX - Tandoor Recipes Deployment

**Was:** Tandoor Recipes deployed (App plus Datenbank)
**Wo:** edge
**Warum:** Rezeptverwaltung mit strukturierter Datenbank
**Auswirkung:** Service läuft als Container Setup

---

### 2025-12-XX - Wiki.js Deployment

**Was:** Wiki Plattform deployed (App plus Datenbank)
**Wo:** edge
**Warum:** Zentrale Dokumentation
**Auswirkung:** Wiki läuft als Container Setup

---

### 2025-11-XX - AdGuard Migration auf Container

**Was:** DNS Dienst von Bare Metal auf Container migriert
**Wo:** edge
**Warum:** Portabilität, einfacheres Backup, bessere Isolation
**Auswirkung:** DNS Dienst containerisiert, Uptime stabil
**Fix:** Troubleshooting bei Container Netzwerk, Host gebunden für IPV6 Funktionalität

---

### 2025-11-25 - Netzwerk und Storage Baseline Setup

**Was:** Netzwerk und Storage Foundation Setup dokumentiert und standardisiert
**Wo:** edge
**Warum:** Reproduzierbarkeit und Disaster Recovery
**Auswirkung:** Bridge Netzwerk, Partitionierung, automatische Mounts via fstab

---

### 2025-11-24 - OS Installation (Baseline)

**Was:** Debian 13 Basisinstallation durchgeführt
**Wo:** edge
**Warum:** Homelab Startpunkt und saubere Grundlage
**Auswirkung:** Basissystem erstellt, weitere Services darauf aufgebaut
