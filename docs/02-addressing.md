# 02 — Direccionamiento y conectividad

## WAN

| Nodo | Interfaz | IP | Máscara | Peer |
|---|---|---|---|---|
| FortiGate-A | `port1` | `203.0.113.21` | `/30` | `203.0.113.22` |
| Router-ISP | `Gi1/0` | `203.0.113.22` | `/30` | `203.0.113.21` |
| Router-ISP | `Gi2/0` | `203.0.113.25` | `/30` | `203.0.113.26` |
| FortiGate-B | `port1` | `203.0.113.26` | `/30` | `203.0.113.25` |

## LAN

### Sitio A

- Subred: `10.21.75.0/25`
- Gateway: `10.21.75.1`
- FortiGate-A `port2`: `10.21.75.1/25`
- DHCP: `10.21.75.10–10.21.75.100`
- PC1: `10.21.75.10`

### Sitio B

- Subred: `10.21.75.128/28`
- Gateway: `10.21.75.129`
- FortiGate-B `port2`: `10.21.75.129/28`
- Web Server: `10.21.75.130/28`

## Rutas

### FortiGate-A

```text
0.0.0.0/0          -> 203.0.113.22 / port1
10.21.75.128/28   -> VPN-TO-SITE-B
```

### FortiGate-B

```text
0.0.0.0/0          -> 203.0.113.25 / port1
10.21.75.0/25      -> VPN-TO-SITE-A
```

## Evidencia

![Topología](../images/01-topology-gns3.png)
