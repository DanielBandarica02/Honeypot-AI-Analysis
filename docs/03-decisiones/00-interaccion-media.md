# Honeypots que emulan el protocolo

## El problema

Un honeypot puede emular un servicio o exponer un sistema real. La segunda opción captura más, incluido el comportamiento del malware en ejecución, pero entrega una máquina real al atacante.

## Qué se decidió

Desplegar honeypots de interacción media: Cowrie, Dionaea, un honeypot web propio y uno de Redis.
Los comandos se registran y las cargas se descargan y almacenan con su hash, pero ninguna llega a
ejecutarse.

El alcance del proyecto es la amenaza oportunista, cuyo tráfico es mayoritariamente automatizado.
Un bot sigue un guion: comprueba el banner, prueba credenciales, ejecuta unos comandos de
reconocimiento, descarga su carga y establece persistencia. No verifica si hay un núcleo real
detrás.

## Qué se descartó

**Interacción alta desde el principio.** Requiere al menos el doble de memoria, aislamiento mucho
más estricto, restauración tras cada sesión y una exposición legal considerable si el sistema
llegara a atacar a terceros. Queda como ampliación posterior.

**T-Pot completo.** No cabe en el presupuesto de memoria previsto, y expone una combinación de
servicios dispares que es en sí misma una huella identificable de señuelo.

## Qué implica

A favor: coste bajo, riesgo acotado, mantenimiento asumible y suficiente para los requisitos PIR-1
a PIR-4.

En contra: no se observa el comportamiento del malware en ejecución, ni su comunicación con
infraestructura de mando, ni la propagación. Un operador humano atento puede identificar el
entorno. Los datos sobrerrepresentan la actividad automatizada.

Estos límites se declaran en todos los productos publicados.
