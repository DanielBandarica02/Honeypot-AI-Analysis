# Requisitos prioritarios de inteligencia (PIR)

Los PIR se escriben antes de recolectar nada. Determinan qué sensores se despliegan, qué campos se
registran y qué productos se publican. Un dato que no sirve a ningún PIR no justifica el coste de
recogerlo ni el riesgo de guardarlo.

Cada apartado de **qué necesito observar** es un requisito técnico sobre la configuración de los
sensores, no una lista de deseos.

---

## PIR-1 — Comportamiento posterior al acceso por SSH

**Pregunta:** ¿Qué hacen los bots en los primeros minutos tras conseguir un acceso válido por SSH
contra el servidor de una pyme europea?

**Qué necesito observar**

- La secuencia completa de comandos ejecutados, en orden y con marca de tiempo por comando
- Tiempo entre el login y el primer comando, y entre el login y la primera acción con impacto
- URL de origen de cada descarga y hash de lo descargado
- Mecanismos de persistencia intentados: claves autorizadas, tareas programadas, servicios
- Si la sesión se cierra sola o permanece abierta, y cuánto dura

**Sensor:** Cowrie
**Producto:** informe de campaña y reglas de detección de persistencia en Linux

---

## PIR-2 — Velocidad de explotación de vulnerabilidades web

**Pregunta:** ¿Cuánto tarda una vulnerabilidad web conocida en aparecer en el tráfico oportunista
desde que se hace pública?

**Qué necesito observar**

- Petición completa: método, ruta, cabeceras y cuerpo
- Primera y última observación de cada patrón de explotación
- Vulnerabilidad asociada al patrón, cuando es identificable, y su fecha de publicación
- Volumen diario por patrón, para distinguir una prueba aislada de una campaña
- Si la explotación va seguida de un intento de subir o ejecutar algo

**Sensor:** honeypot web
**Producto:** cronología de explotación y reglas sobre registros de servidor web

---

## PIR-3 — Credenciales en circulación

**Pregunta:** ¿Qué credenciales se están probando, cuáles son nuevas respecto a las listas públicas
conocidas, y se reutilizan entre servicios distintos?

**Qué necesito observar**

- Par usuario y contraseña de cada intento, con servicio, marca de tiempo y origen
- Orden en que se prueban dentro de una misma sesión, que revela la lista de origen
- Comparación de cada par contra un conjunto de listas públicas de referencia, congelado y
  versionado, para poder afirmar que algo es nuevo
- Uso de las credenciales sembradas por nosotros en un servicio distinto de aquel donde se
  plantaron, con el identificador del cebo y el tiempo transcurrido desde la siembra

**Sensor:** Cowrie, Dionaea (FTP y MySQL), honeypot de Redis, honeytokens
**Producto:** análisis de tendencias de credenciales

---

## PIR-4 — Campañas de minería contra servicios expuestos

**Pregunta:** ¿Cómo se despliegan las campañas de criptominería contra servicios de datos
expuestos, y qué infraestructura comparten entre sí?

**Qué necesito observar**

- Cadena completa desde el acceso inicial hasta el minero: comandos del protocolo, escritura de
  ficheros, descarga y ejecución
- Infraestructura de descarga: dominios y rutas, con su primera observación
- Agrupación de minado y dirección de pago, cuando aparecen en la configuración
- Coincidencias de infraestructura entre conjuntos de comportamiento distintos

**Sensor:** honeypot de Redis, Dionaea (MySQL), Cowrie
**Producto:** informe de campaña y reglas de detección de minería

---

## PIR-5 — Inyección de instrucciones dirigida a agentes de IA

**Pregunta:** ¿Existen ya en el tráfico oportunista de internet intentos de inyectar instrucciones
dirigidas a sistemas de IA que procesen esos registros?

**Qué necesito observar**

- Patrones de texto dirigidos a modelos de lenguaje en comandos, cabeceras, nombres de fichero y
  cuerpos de petición
- Frecuencia y evolución en el tiempo, y en qué sensor aparecen
- Si el patrón parece deliberado o es texto casual que coincide con el detector
- Si, en pruebas controladas, esos payloads alteran el resultado del triaje

**Sensor:** todos
**Producto:** informe de seguridad del agente

> Este requisito solo puede responderse con datos propios. Una respuesta negativa también es un
> resultado válido y se publicará como tal.
