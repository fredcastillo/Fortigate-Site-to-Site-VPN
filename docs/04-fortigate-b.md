# 04 — FortiGate-B

## Identificación

- Hostname: `FortiGate-B`
- FortiOS: `v7.0.9`
- WAN: `port1`
- LAN: `port2`
- Interfaz auxiliar de configuración observada: `port5` (`20.21.75.1/24`, alias `PORT_FOR_CONFIG`)

## Interfaces principales

| Interfaz | Dirección | Uso |
|---|---|---|
| `port1` | `203.0.113.26/30` | WAN |
| `port2` | `10.21.75.129/28` | LAN Servidor |
| `VPN-TO-SITE-A` | túnel | IPsec Site-to-Site |

## Objetos de dirección

- `LAN_USUARIOS` → `10.21.75.0/25`
- `LAN_SERVIDOR` → `10.21.75.128/28`

## VPN mediante GUI

La VPN se configuró mediante la interfaz gráfica de FortiOS.

Ruta GUI:

`VPN > IPsec Tunnels > Create New > IPsec Tunnel > Custom`

### Phase 1

- Name: `VPN-TO-SITE-A`
- Interface: `port1`
- Remote Gateway: `203.0.113.21`
- IKE: `2`
- Authentication: Pre-Shared Key
- Proposal: `DES-SHA256`
- DH Group: `14`

### Phase 2

- Local selector: `10.21.75.128/28`
- Remote selector: `10.21.75.0/25`
- Proposal: `DES-SHA256`

## Rutas estáticas

- Default route → `203.0.113.25` por `port1`
- Red remota → `10.21.75.0/25` por `VPN-TO-SITE-A`

## Políticas

### LAN → VPN

- Incoming: `port2`
- Outgoing: `VPN-TO-SITE-A`
- Source: `LAN_SERVIDOR`
- Destination: `LAN_USUARIOS`
- Service: `ALL`
- NAT: Disabled

### VPN → LAN

- Incoming: `VPN-TO-SITE-A`
- Outgoing: `port2`
- Source: `LAN_USUARIOS`
- Destination: `LAN_SERVIDOR`
- Service: `ALL`
- NAT: Disabled

### Web Server → Internet

- Name: `WEBSERVER_A_INTERNET`
- Incoming: `port2`
- Outgoing: `port1`
- Source: `LAN_SERVIDOR`
- Destination: `all`
- Service: `ALL`
- NAT: Enabled

## Evidencias

![VPN FortiGate-B](../images/03-vpn-fortigate-b.png)

![Policies FortiGate-B](../images/05-policies-fortigate-b.png)
