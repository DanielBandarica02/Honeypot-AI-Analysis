# El modelo analiza, no actúa

## El problema

La entrada de este sistema la escribe el adversario. Los comandos registrados, las cabeceras de
las peticiones y los nombres de los ficheros son texto bajo control de quien ataca. Cualquier
componente que lea ese texto y pueda actuar sobre el mundo es un objetivo.

## Qué se decidió

El modelo produce exclusivamente documentos estructurados con su análisis. No ejecuta comandos, no
modifica configuración, no consulta libremente el almacén de datos y no publica nada.

Entre su salida y cualquier efecto hay dos barreras: una validación automática que comprueba el
esquema, los identificadores de técnica y las vulnerabilidades citadas, y la aprobación humana de
un cambio en el repositorio.

Las consultas que necesita la fase de threat hunting salen de una biblioteca parametrizada y
versionada: el modelo elige plantilla y parámetros, nunca escribe la consulta.

## Qué se descartó

**Permitir acciones acotadas**, como marcar casos automáticamente. Añade superficie de ataque sin
ahorrar trabajo real a esta escala.

**Dar acceso directo al almacén de datos.** Convierte cualquier inyección en una consulta
arbitraria contra los datos propios.

## Qué implica

A favor: una inyección exitosa produce, como máximo, un análisis erróneo que la validación o la
revisión detectan. No produce una acción.

En contra: todo pasa por revisión humana, lo que limita el volumen diario. Aceptable, porque el
cuello de botella real es la capacidad de análisis, no la de publicación.
