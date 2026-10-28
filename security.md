# Política de seguridad del repositorio

Este es un proyecto defensivo y de observación. La infraestructura registra lo que llega; no
interactúa con los sistemas de origen ni los ataca.

Esta política cubre dos cosas distintas: qué información no puede salir de aquí, y cómo reportar
un problema de seguridad en el propio proyecto.

## Qué nunca se publica

| Dato | Motivo |
|---|---|
| IP, dominio o nombre de host del servidor de sensores | Publicar la dirección de un señuelo permite identificarlo, evitarlo o atacarlo de forma dirigida |
| El perfil de la empresa ficticia, en cualquier forma | Ni el fichero real ni un ejemplo con su estructura rellena: revelaría qué vulnerabilidad se emula, dónde están los cebos y qué usuarios existen |
| Las credenciales válidas del servidor ficticio | Permitirían entrar sin esfuerzo y distinguir a quien las conoce de un atacante real |
| IP administrativa personal y topología de la red doméstica | Exponen la infraestructura de análisis, que es el objetivo valioso |
| IPs completas de terceros observados | Muchas son sistemas comprometidos de personas ajenas al ataque |
| Credenciales, claves privadas, tokens, cookies y claves de API | Incluye las del proveedor, Wazuh, n8n y los webhooks de alerta |
| Muestras de malware, payloads o binarios capturados | Distribuirlos es un riesgo para terceros; solo se publican sus hashes |

De lo capturado se publican únicamente indicadores seguros: hashes, marcas de tiempo y metadatos
saneados. Los indicadores van neutralizados, de forma agregada y con fecha de caducidad.

## Cómo se verifica

`tests/sin-datos-sensibles.sh` se ejecuta en cada cambio y rechaza los que introduzcan
direcciones IP públicas en texto plano, claves privadas o patrones de credencial. Los rangos
privados y los reservados para documentación están permitidos.

La comprobación automática es una red de seguridad, no una garantía. La revisión antes de
publicar sigue siendo responsabilidad de quien escribe.

## Si algo se publica por error

Un dato que ha llegado a un repositorio público debe considerarse comprometido, aunque se borre a
los pocos minutos. El orden de actuación es:

1. **Invalidar primero.** Rotar la credencial, revocar la clave o cambiar la dirección expuesta.
   Esto va antes que limpiar el repositorio.
2. **Reescribir el histórico.** Un commit que elimina el dato no lo borra: sigue accesible en el
   historial, en los forks y en la caché de la plataforma. Hay que reescribir el histórico y
   forzar el envío.
3. **Anotarlo en el diario de laboratorio**, con qué se expuso, durante cuánto tiempo y qué se
   hizo. Un incidente ocultado no sirve de nada; uno documentado es material de aprendizaje.

## Uso responsable

No se escanean las direcciones observadas, no se accede a sistemas externos y no se ejecuta nada
de lo capturado. El honeywall bloquea cualquier uso del señuelo para atacar a terceros, y una
batería de pruebas lo verifica en cada cambio.

Nada de lo publicado aquí debe usarse para atacar sistemas ajenos ni para tomar represalias contra
las direcciones observadas.

## Datos personales

Las direcciones IP son datos personales en la Unión Europea. La base legal, el plazo de retención
y los criterios de publicación están en
[`docs/01-concepto/03-politica-datos.md`](docs/01-concepto/03-politica-datos.md).

## Reportar un problema

| Qué has encontrado | Qué hacer |
|---|---|
| Datos publicados que no deberían estar | Abrir una incidencia indicando el fichero y la línea, **sin incluir el dato** |
| Una vulnerabilidad en el código o la configuración del proyecto | Contacto privado por [LinkedIn](https://linkedin.com/in/danielbandarica), sin publicar los detalles hasta que esté corregida |

Este repositorio documenta un laboratorio personal, no un servicio en producción: no hay plazos
de respuesta comprometidos ni programa de recompensas.
