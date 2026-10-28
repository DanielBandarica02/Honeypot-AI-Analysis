# Modelo de amenazas de la infraestructura

Un honeypot está diseñado para ser atacado. La pregunta no es si el servidor de sensores caerá,
sino qué pasa cuando caiga.

El modelo de amenazas del agente de IA es un problema distinto y está en
[`../05-ai-security/`](../05-ai-security/).

## Qué se protege

| Activo | Si se pierde |
|---|---|
| La red doméstica | Compromiso real con impacto personal |
| Los datos recolectados | Meses de recolección irrepetibles |
| La reputación de la dirección IP | Quejas de abuso, cierre del servicio y responsabilidad propia |
| El servidor de sensores | Nada: se reconstruye desde código |

El señuelo es lo menos valioso del conjunto, y el diseño parte de ahí.

## El supuesto de partida

Alguien conseguirá ejecutar código en el servidor de sensores. No como fallo, sino como resultado
previsible. Todo lo demás se diseña asumiendo que ya ha ocurrido.

## Escenarios y qué los corta

| Escenario | Qué lo corta |
|---|---|
| El señuelo ataca a terceros o escanea internet | Salida denegada por defecto; solo se permite la descarga de cargas, con límites |
| El señuelo envía correo basura | Puerto de correo saliente bloqueado |
| Acceso al servicio de metadatos del proveedor | Bloqueado de forma explícita en el honeywall |
| Uso del túnel como pivote hacia casa | El túnel se inicia desde casa y solo deja alcanzable el puerto de eventos |
| Órdenes al recolector a través del agente | Ejecución remota y respuesta activa desactivadas |
| Fuga del contenedor al anfitrión | Contenedores sin privilegios, solo lectura, sin capacidades añadidas |
| Compromiso silencioso | El agente vigila la integridad de configuración y binarios |
| Borrado o manipulación de las pruebas | Los eventos enviados quedan fuera del alcance del atacante |

El control que no puede fallar es el primero. Perder el señuelo es irrelevante; que el señuelo
ataque a terceros es un problema legal y el fin del proyecto.

## Riesgos aceptados

| Riesgo | Por qué |
|---|---|
| Que identifiquen el entorno como señuelo | Inevitable con interacción media; se mide, no se evita |
| Saturar ancho de banda o disco | Alertas de capacidad y reconstrucción rápida |
| Envenenar los datos con tráfico fabricado | Exige conocer el proyecto; el etiquetado manual lo limita |
| Fuga del anfitrión al hipervisor del proveedor | Fuera de nuestro control |

## Si el servidor se compromete

1. Capturar una imagen del disco como evidencia, con su hash.
2. Cortar el túnel.
3. Destruir y reconstruir desde código.
4. Analizar y publicar el resultado en `docs/08-hallazgos/`.

La evidencia se captura antes de restaurar: un compromiso real del señuelo es uno de los
hallazgos más valiosos que puede dar el proyecto.

## Cómo se verifica

| Control | Prueba |
|---|---|
| Control de salida | `tests/egress/`, en cada cambio |
| Aislamiento del túnel | Escaneo desde el servidor contra el extremo doméstico |
| Reconstrucción desde código | Destruir y rehacer el laboratorio, cronometrado |

Un control sin prueba automatizada es una intención, no un control.
