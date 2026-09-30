# 01 — Arquitectura y alcance

## Propósito

La Infraestructura 1 consiste en dos sitios de red conectados mediante un enlace WAN simulado y una VPN IPsec Site-to-Site.

El Sitio A representa la red de usuarios y el Sitio B representa la red donde reside el servidor web. El túnel IPsec se utiliza para proteger el tráfico entre `10.21.75.0/25` y `10.21.75.128/28`.

## Componentes

| Componente | Función |
|---|---|
| FortiGate-A | Gateway y firewall del Sitio A |
| FortiGate-B | Gateway y firewall del Sitio B |
| Router-ISP | Simulación del tránsito WAN |
| Switch-A | Acceso a la VLAN 10 |
| PC1 | Host de pruebas del Sitio A |
| Web Server | Recurso HTTPS del Sitio B |
| Browser-PC | Administración auxiliar de GUI |

## Topología

![Topología](../images/01-topology-gns3.png)

## Flujo esperado

```text
PC1
  |
  | 10.21.75.0/25
  v
FortiGate-A
  |
  | IPsec Site-to-Site
  v
FortiGate-B
  |
  | 10.21.75.128/28
  v
Web Server 10.21.75.130
```

## Criterio de éxito

La infraestructura cumple el objetivo cuando el usuario puede alcanzar el servidor a través de la VPN y el acceso entre las dos redes deja de estar disponible al interrumpirse el túnel.
