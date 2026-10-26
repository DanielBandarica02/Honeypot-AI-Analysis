# Cuándo deja entrar el honeypot

## El problema

Si nunca concede acceso, el único dato son intentos fallidos y los requisitos PIR-1 y PIR-4 se
quedan sin responder. Si acepta cualquier credencial, se identifica de inmediato: basta con probar
una contraseña imposible y ver si entra.

## Qué se decidió

Dos condiciones, en el mismo intento:

- **La credencial es una de las válidas del servidor.** Define *qué* contraseñas funcionan.
- **Se ha superado el umbral.** Define *cuándo* empiezan a funcionar. Un número entre 3 y 12,
  elegido al azar por cada dirección de origen.

El umbral no concede el acceso: solo activa la posibilidad. A partir de ahí hay que acertar con
una credencial válida.

Con un umbral de 7, por ejemplo:

| Qué prueba el atacante | Resultado |
|---|---|
| 50 contraseñas aleatorias | No entra: ninguna es válida |
| Una credencial válida en el intento 1 | No entra: aún no ha alcanzado el umbral |
| Una credencial válida en el intento 7 | Entra |
| Credenciales no válidas hasta el 15, y una válida en el 16 | Entra en el 16 |

Ese retraso inicial hace que el acceso parezca el resultado de un ataque de fuerza bruta y no un
regalo.

## Las dos listas de credenciales

El proyecto maneja dos conjuntos de credenciales con funciones distintas. Conviene no confundirlos.

### Las credenciales del servidor ficticio

Un fichero propio, versionado en el repositorio, con las credenciales que de verdad abren la
sesión. Es el equivalente a la contraseña de un servidor real, y son las únicas que conceden
acceso.

Se eligen con dos criterios:

- **Que los bots las prueben.** Si se elige una contraseña que ningún atacante intenta nunca,
  nadie entrará jamás y el honeypot no producirá datos. Por eso una parte se toma de las
  credenciales más repetidas en los diccionarios que circulan por internet.
- **Que encajen con la empresa ficticia.** Otra parte se deriva del perfil: usuarios y
  contraseñas coherentes con su nombre, su dominio y su sector. Aportan verosimilitud, y si
  alguna de ellas llega a usarse desde otro sitio, indica que el contenido del servidor se ha
  filtrado.

Ninguna es aleatoria ni de alta entropía: si una contraseña imposible concediera acceso, el
entorno quedaría identificado como señuelo.

Versionarlas permite saber, al analizar una sesión, con qué credencial exacta se entró y desde
cuándo era válida.

### Los diccionarios públicos

Son las listas de credenciales que circulan por internet y que usan los propios atacantes. No
conceden acceso a nada: se emplean como material de referencia, con dos fines.

- **Elegir bien las credenciales del servidor.** Indican qué prueban realmente los bots, que es
  lo que hace que el honeypot reciba accesos.
- **Saber qué es novedad.** Para afirmar que una credencial observada es nueva hace falta
  compararla con algo. Se descarga una versión concreta de esos diccionarios, se congela y se
  versiona; lo que no aparece en ella es candidato a credencial recién puesta en circulación.
  Esto es lo que responde al requisito PIR-3.

Congelar la versión es importante: si el diccionario de referencia cambia por debajo, dos
análisis hechos en fechas distintas dejan de ser comparables.

### Credenciales que ya han funcionado

Una credencial que concedió acceso una vez entra directamente desde cualquier otra dirección, sin
esperar al umbral. Refleja cómo circula una credencial dentro de una campaña una vez alguien la
descubre.

## Qué se descartó

| Alternativa | Por qué no |
|---|---|
| Aceptar cualquier credencial tras N intentos, que es lo que trae Cowrie de serie | Falla la prueba de la contraseña imposible |
| Aceptar solo por lista, sin contar intentos | Concede el acceso al primer acierto y elimina la fase de fuerza bruta |
| Probabilidad creciente por intento | Un servidor real no se vuelve gradualmente más permisivo |
| Umbrales de cientos de intentos | La mayoría de los bots abandonan antes |

## Qué implica

Se obtienen sesiones posteriores al acceso sin fallar la comprobación habitual de detección de
señuelos.

A cambio, el conjunto de credenciales válidas introduce un sesgo: solo se observan campañas que
usan credenciales habituales. Y el contador es por dirección de origen, así que una campaña
distribuida podría no alcanzar el umbral en ninguna. Ambas limitaciones se declaran en los
informes.

## Cómo se ajusta

| Métrica | Objetivo | Si se desvía |
|---|---|---|
| Sesiones con acceso al día | Entre 5 y 30 | Bajar o subir el umbral mínimo |
| Sesiones con acceso que ejecutan comandos | Más del 50 % | El entorno resulta poco creíble una vez dentro |
| Sesiones que prueban alta entropía y se desconectan | Vigilar tendencia | Si crece, están identificando el señuelo |
| Credenciales válidas que nunca se prueban | Revisar cada mes | No reflejan lo que circula |
