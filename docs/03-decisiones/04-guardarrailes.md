# Las reglas críticas viven en el código

## El problema

Es tentador escribir las reglas que no pueden fallar como instrucciones al modelo: «nunca
descartes una sesión con persistencia». Pero una instrucción en el prompt compite con el resto del
texto del prompt, incluido el que escribió el atacante, y su cumplimiento no es verificable.

## Qué se decidió

Las reglas críticas se implementan como nodos de n8n que se ejecutan **después** de la respuesta
del modelo, y tienen pruebas unitarias propias.

Reglas iniciales:

- Una sesión con autenticación válida seguida de ejecución de comandos nunca se clasifica como
  ruido conocido.
- Una sesión con descarga de carga útil, persistencia o movimiento hacia otros servicios nunca se
  clasifica como ruido conocido.
- Un conjunto de comportamiento nunca visto nunca se clasifica como ruido conocido.
- Una sesión marcada por el detector de inyección queda excluida del camino automatizado y pasa a
  revisión.
- Una respuesta vacía o que no valida contra su esquema nunca equivale a «sin hallazgos»: se
  reintenta y, si vuelve a fallar, pasa a revisión.

## Qué se descartó

**Reglas en el prompt.** No verificables y vulnerables al propio texto que analizan.

**Confiar en la confianza declarada por el modelo.** Es una salida del modelo, no una medida
independiente. Se registra y se compara con la realidad, pero no decide nada por sí sola.

## Qué implica

A favor: las reglas críticas son auditables, versionadas y comprobables en integración continua.
El comportamiento no cambia al cambiar de modelo.

En contra: más casos llegan a revisión de los que serían estrictamente necesarios. Es el sentido
de un diseño que falla hacia el lado seguro.
