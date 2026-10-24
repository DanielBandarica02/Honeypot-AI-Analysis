# Política de datos

## Naturaleza de los datos

Los registros contienen direcciones IP, que en la Unión Europea se consideran datos personales.
También contienen credenciales probadas por los atacantes, que pueden proceder de filtraciones
reales de terceros.

## Tratamiento

| Aspecto | Decisión |
|---|---|
| Base legal | Interés legítimo en la investigación de seguridad |
| Retención de registros en crudo | 90 días |
| Retención de datos agregados | Indefinida |
| Muestras capturadas | Solo en el servidor de sensores, cifradas; nunca sincronizadas a la red doméstica |
| Credenciales observadas | Se analizan de forma agregada; nunca se publican pares completos asociados a un servicio real |
| Alertas en tiempo real | Canal privado, con los datos mínimos; nunca direcciones completas de terceros |

## Publicación

- Los indicadores se publican neutralizados y con fecha de validez.
- Toda publicación advierte de que muchas direcciones corresponden a sistemas comprometidos de
  terceros y no al origen real de la actividad.
- Las direcciones completas de terceros no se publican.
- Las muestras de malware no se publican en ningún caso; solo sus hashes.

## Datos de la empresa ficticia

Todos los datos del perfil son sintéticos. El procedimiento de verificación de que no coinciden con
entidades o personas reales está en
[`../03-decisiones/ADR-0003-persona-ficticia.md`](../03-decisiones/ADR-0003-persona-ficticia.md).
