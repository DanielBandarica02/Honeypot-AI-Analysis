# Alcance y límites de la fuente

Declarar las limitaciones de la fuente forma parte del análisis. Un informe que no las declara
invita a conclusiones que los datos no sostienen.

## Qué captura esta fuente

- Credenciales probadas contra SSH, Telnet, FTP, MySQL y Redis
- Secuencias de comandos ejecutadas tras un acceso válido
- Mecanismos de persistencia intentados
- Peticiones de explotación contra aplicaciones web conocidas
- Cadenas de abuso de servicios de datos expuestos
- Metadatos de las cargas descargadas
- Reutilización de credenciales entre servicios, mediante cebos sembrados

## Qué no captura

| Límite | Motivo |
|---|---|
| Ataques dirigidos y APTs | Un señuelo sin valor aparente no atrae operaciones dirigidas |
| Movimiento lateral en entornos Windows o Active Directory | Fuera del perfil desplegado |
| Comportamiento del malware en ejecución | Los honeypots son de interacción media: no se ejecuta nada |
| Operadores humanos cuidadosos | Un analista atento puede identificar el entorno y retirarse |
| Tráfico contra servicios no desplegados | La superficie expuesta condiciona por completo lo observado |

## Sesgos conocidos

**Sobrerrepresentación de la automatización.** Los bots no verifican el entorno; los humanos sí. Lo
observado tiende hacia lo automatizado.

**Dependencia de la superficie expuesta.** Los resultados describen lo que le ocurre a este perfil
de servidor, no a internet en su conjunto.

**Geolocalización.** El país asociado a una dirección IP indica dónde está alojada la máquina, no
la nacionalidad ni la ubicación de quien la opera. Muchas son sistemas comprometidos de terceros.

**Evento no equivale a atacante.** Una sola dirección puede generar miles de eventos. Las cifras se
publican indicando siempre la unidad: eventos, sesiones, direcciones o conjuntos de comportamiento.

## Sobre la atribución

Este proyecto no atribuye actividad a actores ni a grupos. Agrupa campañas por comportamiento
observado.

Cuando un conjunto de actividad coincide con una familia documentada públicamente, se cita la
fuente y se indica el nivel de confianza, sin presentarlo como conclusión propia.
