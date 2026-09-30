# 03 — FortiGate-A

## Identificación

- Hostname: `FortiGate-A`
- FortiOS: `v7.0.9`
- WAN: `port1`
- LAN: `port2`

## Interfaces

| Interfaz | Dirección | Uso |
|---|---|---|
| `port1` | `203.0.113.21/30` | WAN |
| `port2` | `10.21.75.1/25` | LAN Usuarios |
| `VPN-TO-SITE-B` | túnel | IPsec Site-to-Site |

`port2` permite administración web y ping dentro de la LAN. La interfaz WAN se mantiene limitada al acceso de ping según la configuración consultada.

## Objetos de dirección

- `LAN_USUARIOS` → `10.21.75.0/25`
- `LAN_SERVIDOR` → `10.21.75.128/28`

## DHCP

El servidor DHCP del FortiGate-A se encuentra asociado a `port2`.

- Gateway: `10.21.75.1`
- Máscara: `255.255.255.128`
- Rango: `10.21.75.10–10.21.75.100`

## VPN mediante GUI

La VPN se configuró mediante la interfaz gráfica de FortiOS.

Ruta GUI:

`VPN > IPsec Tunnels > Create New > IPsec Tunnel > Custom`

### Phase 1

- Name: `VPN-TO-SITE-B`
- Interface: `port1`
- Remote Gateway: `203.0.113.26`
- IKE: `2`
- Authentication: Pre-Shared Key
- Proposal: `DES-SHA256`
- DH Group: `14`

### Phase 2

- Local selector: `10.21.75.0/25`
- Remote selector: `10.21.75.128/28`
- Proposal: `DES-SHA256`

## Rutas estáticas

- Default route → `203.0.113.22` por `port1`
- Red remota → `10.21.75.128/28` por `VPN-TO-SITE-B`

## Políticas

### LAN → VPN

- Incoming: `port2`
- Outgoing: `VPN-TO-SITE-B`
- Source: `LAN_USUARIOS`
- Destination: `LAN_SERVIDOR`
- Service: `ALL`
- NAT: Disabled

### VPN → LAN

- Incoming: `VPN-TO-SITE-B`
- Outgoing: `port2`
- Source: `LAN_SERVIDOR`
- Destination: `LAN_USUARIOS`
- Service: `ALL`
- NAT: Disabled

### Usuarios → Internet

- Name: `USUARIOS_A_INTERNET`
- Incoming: `port2`
- Outgoing: `port1`
- Source: `LAN_USUARIOS`
- Destination: `all`
- Service: `ALL`
- NAT: Enabled

## Evidencias

![VPN FortiGate-A](../images/02-vpn-fortigate-a.png)

![Policies FortiGate-A](../images/04-policies-fortigate-a.png)
