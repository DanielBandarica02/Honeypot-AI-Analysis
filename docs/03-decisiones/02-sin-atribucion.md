# Agrupar por comportamiento, no atribuir a actores

## El problema

Es habitual que los informes de inteligencia asocien actividad a grupos concretos. La atribución
seria requiere fuentes múltiples, contexto geopolítico y recursos de los que este proyecto no
dispone. Hacerla con una sola fuente y un puñado de direcciones IP produce conclusiones atractivas
y erróneas.

## Qué se decidió

No atribuir actividad a actores ni a grupos. La actividad se agrupa por comportamiento observado:
secuencia de comandos, infraestructura de descarga, credenciales empleadas.

Cuando un conjunto de actividad coincide con una familia de malware o una campaña documentada
públicamente, se indica la coincidencia citando la fuente y asignando un nivel de confianza, sin
presentarla como conclusión propia.

## Qué se descartó

**Atribuir por geolocalización.** El país asociado a una dirección indica dónde está alojada la
máquina. Muchas son sistemas comprometidos de terceros.

**Atribuir por coincidencia de herramientas.** Las herramientas se comparten, se filtran y se
reutilizan entre grupos sin relación entre sí.

## Qué implica

A favor: los informes afirman solo lo que la evidencia sostiene. La distinción entre agrupar por
comportamiento y atribuir a un grupo es en sí misma una competencia profesional.

En contra: los productos no incluyen perfiles de actor, que algunos destinatarios esperan. Se
compensa explicando la distinción de forma explícita en cada informe.
