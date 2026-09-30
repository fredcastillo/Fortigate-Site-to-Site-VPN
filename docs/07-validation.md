# 07 — Validación y demostración

## Objetivo de validación

La prueba final debe demostrar dos estados:

1. **VPN activa:** el usuario alcanza el Web Server remoto.
2. **VPN no activa:** el acceso entre las LAN deja de funcionar.

## Prueba 1 — VPN activa

1. Confirmar que el túnel IPsec está operativo.
2. Desde PC1 ejecutar la prueba de conectividad hacia `10.21.75.130`.
3. Verificar el acceso al servicio HTTPS.

![VPN activa / conectividad](../images/08-connectivity-vpn-up.png)

## Prueba 2 — VPN inactiva

1. Interrumpir el túnel IPsec desde la GUI.
2. Repetir la prueba hacia `10.21.75.130`.
3. Registrar el resultado observado.

![VPN inactiva / conectividad](../images/09-connectivity-vpn-down.png)

## Prueba 3 — Traceroute

Ejecutar traceroute desde el equipo de usuarios hacia `10.21.75.130`.

![Traceroute](../images/10-traceroute.png)

## Evidencia de políticas

![Policies FortiGate-A](../images/04-policies-fortigate-a.png)

![Policies FortiGate-B](../images/05-policies-fortigate-b.png)

## Nota sobre el video

Estas pruebas se mostrarán en el video como demostración del objetivo de seguridad de la práctica. El guion está diseñado para mantenerse dentro del límite de 10 minutos.
