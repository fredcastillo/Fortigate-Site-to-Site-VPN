# Scripts y comandos

## Criterio del laboratorio

La configuración funcional de los FortiGate (redes, VPN, rutas y políticas) se realizó mediante la **GUI de FortiOS**, de acuerdo con el requisito de la asignación.

La CLI se utilizó en dos contextos:

1. **Bootstrap inicial:** configuración mínima necesaria para disponer de conectividad y acceso a la GUI.
2. **Consulta/verificación:** comandos `show` y `diagnose` utilizados posteriormente para confirmar el estado de la configuración.

## Importante

No se conserva en este material un transcript completo de los comandos exactos utilizados durante el bootstrap inicial. Por ese motivo, este repositorio **no inventa un script de despliegue FortiGate**.

Los bloques CLI completos que aparecían en documentación anterior no deben interpretarse como el método mediante el cual se implementó la VPN.

## Archivos

- `verification-commands.txt` — comandos de consulta/verificación realmente ejecutados.
- `fortigate-bootstrap-note.md` — alcance de la inicialización CLI.
