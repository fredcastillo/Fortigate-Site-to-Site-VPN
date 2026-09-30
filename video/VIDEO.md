# 🎥 Guion de video — Infraestructura 1

## Duración objetivo

**8:30–9:30 minutos**, dejando margen para pausas y pequeños retrasos. El máximo permitido por la práctica es 10 minutos.

## Reglas de grabación

- Mostrar fecha y hora en pantalla al inicio.
- Mantener cámara activa para que se vea el rostro.
- Usar voz durante toda la demostración.
- No cambiar de sistema operativo o entorno durante la demostración.
- Mostrar únicamente la evidencia necesaria para demostrar el objetivo.
- Evitar leer todos los detalles del README.

---

## 0:00–0:40 — Presentación

**En pantalla:** reloj/fecha + cámara + topología GNS3.

**Decir:**

> "Hola, mi nombre es Fred Sneyder Castillo Apolinar, matrícula 2025-2175. Esta es la demostración de la Infraestructura 1 de la práctica de Seguridad de Redes. El objetivo es comunicar un usuario con un servidor mediante una VPN Site-to-Site IPsec y comprobar que la comunicación depende de que el túnel VPN esté activo. La implementación fue realizada en GNS3 utilizando FortiOS 7.0.9."

---

## 0:40–1:25 — Presentación de la topología

**Mostrar:** `images/01-topology-gns3.png` / topología GNS3.

**Decir:**

> "En el Sitio A tenemos la red de usuarios 10.21.75.0/25, con FortiGate-A como gateway. En el Sitio B tenemos la red 10.21.75.128/28 y el servidor web 10.21.75.130. Ambos FortiGate están conectados por un Router-ISP que simula el tránsito WAN. También tenemos VLAN 10 y DHCP en la red de usuarios."

---

## 1:25–2:15 — FortiGate-A

**Mostrar:** GUI de FortiGate-A y la captura de VPN.

**Decir:**

> "En FortiGate-A, port1 utiliza 203.0.113.21/30 para el tránsito WAN y port2 utiliza 10.21.75.1/25 para la LAN de usuarios. El túnel hacia el segundo sitio se llama VPN-TO-SITE-B. Se configuró mediante la GUI en modo Custom, con IKEv2, autenticación mediante clave precompartida, propuesta DES-SHA256 y grupo Diffie-Hellman 14."

No leer la PSK en voz alta.

---

## 2:15–3:05 — FortiGate-B

**Mostrar:** GUI de FortiGate-B y la captura correspondiente.

**Decir:**

> "En FortiGate-B, port1 utiliza 203.0.113.26/30 y port2 utiliza 10.21.75.129/28. El túnel inverso se llama VPN-TO-SITE-A y utiliza los parámetros compatibles con el extremo A. El servidor web está ubicado en esta LAN con la dirección 10.21.75.130."

---

## 3:05–3:55 — Routing y políticas

**Mostrar:** las policies de ambos FortiGate.

**Decir:**

> "El tráfico hacia la red remota se dirige por la interfaz del túnel. Las políticas LAN hacia VPN y VPN hacia LAN tienen NAT desactivado para conservar las direcciones privadas de los dos sitios. Adicionalmente, existen políticas independientes para permitir la salida a Internet mediante NAT."

No detenerse a leer todas las columnas.

---

## 3:55–5:30 — VPN activa y comunicación

**Mostrar:** estado del túnel y PC1.

**Decir:**

> "Con el túnel activo, voy a verificar la comunicación desde el usuario hacia el servidor remoto. El destino es 10.21.75.130."

Ejecutar la prueba que hayas validado previamente.

Si utilizas ping:

```text
ping 10.21.75.130
```

Después mostrar el acceso HTTPS al servidor.

**Decir:**

> "La comunicación se establece correctamente a través de la infraestructura VPN."

---

## 5:30–6:20 — Traceroute

**Mostrar:** terminal de PC1.

**Decir:**

> "Ahora voy a realizar el traceroute solicitado por la práctica hacia el servidor 10.21.75.130, para observar el camino utilizado por el tráfico."

Ejecutar el comando correspondiente al sistema de PC1.

**Importante:** no memorices un resultado. Describe exactamente los saltos que aparezcan en pantalla.

---

## 6:20–7:25 — VPN inactiva

**Mostrar:** GUI del túnel.

Desactivar/interrumpir la VPN mediante la GUI.

**Decir:**

> "Ahora voy a interrumpir el enlace VPN para demostrar el comportamiento de seguridad solicitado."

Repetir la prueba de comunicación hacia `10.21.75.130`.

> "La prueba ya no obtiene la misma conectividad porque el enlace VPN se encuentra interrumpido. Esto demuestra la dependencia del acceso entre las dos redes respecto al túnel configurado."

Usa literalmente el resultado observado; no afirmes "timeout" si apareció otro tipo de error.

---

## 7:25–8:15 — Restauración

Volver a activar/restaurar el túnel desde la GUI.

**Decir:**

> "Finalmente restauro el enlace VPN y vuelvo a comprobar la comunicación hacia el servidor."

Repetir la prueba.

> "La comunicación vuelve a estar disponible con el túnel restablecido."

---

## 8:15–9:00 — VLAN/DHCP y cierre

**Mostrar:** rápidamente la configuración de DHCP/VLAN o la evidencia ya preparada.

**Decir:**

> "La red de usuarios utiliza VLAN 10 y DHCP desde el FortiGate-A, con un rango de 10.21.75.10 a 10.21.75.100. Durante esta práctica reforcé el uso de políticas de firewall, routing y VPN Site-to-Site, además de la validación de una comunicación que depende de un enlace seguro entre dos sitios."

> "Con esto queda demostrada la Infraestructura 1 y su objetivo de Seguridad de Redes. Gracias."

---

## 🎬 Evidencias que conviene tener abiertas antes de grabar

1. Topología GNS3.
2. VPN FortiGate-A.
3. VPN FortiGate-B.
4. Policies de FortiGate-A.
5. Policies de FortiGate-B.
6. PC1 con conectividad al servidor.
7. Traceroute.

No es necesario convertir cada una en una diapositiva: el objetivo es mostrar la evidencia dentro del entorno de laboratorio.
