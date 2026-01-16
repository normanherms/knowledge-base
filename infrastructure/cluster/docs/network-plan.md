# Cluster Netzwerk- und Adressplanung (v1.6)

## Wireguard Mesh Adressplanung

## WireGuard Mesh (10.99.99.0/24)

- A = primäre WG-IP
- B = sekundäre WG-IP
- Start bei 10.99.99.1
- nur Cluster Nodes + Backup brauchen Wireguard

### prod

A: 10.99.99.1 (Primary WG)
B: 10.99.99.101 (DRBD Replication)

#### Rolle

- K3s Worker
- DRBD Primary

### load

A: 10.99.99.2 (Primary WG)
B: 10.99.99.102 (Secondary WG)

#### Rolle

- K3s Control Plane
- Quorum Node
- Loadbalancing für OpenCloud

### mirror

A: 10.99.99.3 (Primary WG)
B: 10.99.99.103 (DRBD Replication)

#### Rolle

- K3s Worker
- DRBD Secondary

### dash

A: 10.99.99.4 (Primary WG)
B: 10.99.99.104 (Secondary WG)

#### Rolle

- Monitoring Node (Prometheus / Grafana)


### Synology

A: 10.99.99.5 (Primary WG)

#### Rolle

- Backup
