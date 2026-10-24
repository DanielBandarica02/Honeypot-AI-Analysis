## El problema

La mayoría de los compromisos que sufre una empresa pequeña no empiezan con un ataque dirigido.
Empiezan con un servidor expuesto, una credencial débil o una vulnerabilidad web sin parchear que
alguien encuentra escaneando internet de forma indiscriminada.

Esa actividad es abundante y está poco documentada desde la perspectiva de quien la recibe.
Observarla de primera mano no es lo mismo que leer informes sobre ella: permite construir
detecciones basadas en comportamiento real y no en suposiciones.

## La aproximación

Exponer un conjunto de servicios coherentes con una empresa pequeña real, capturar lo que llega y
convertirlo en tres cosas: entendimiento del adversario, reglas de detección validadas y un caso
de estudio sobre cómo construir un agente de IA que procese datos escritos por el atacante sin
convertirse él mismo en el punto débil.

## Por qué los requisitos se escriben antes

Un requisito de inteligencia no describe lo que ya se sabe, sino lo que se quiere averiguar. Si se
recolecta primero y se pregunta después, se acaba analizando lo que casualmente se capturó.

Escribirlos antes tiene una consecuencia práctica: cada requisito determina qué sensor se despliega
y qué campos hay que registrar. El PIR-1 es la razón por la que Cowrie debe guardar las sesiones
completas con marca de tiempo por comando, y no solo los intentos de autenticación.

## Documentos de esta sección

| Documento | Contenido |
|---|---|
| [pirs.md](01-pirs.md) | Requisitos prioritarios de inteligencia |
| [alcance.md](02-alcance.md) | Qué captura esta fuente, qué no, y con qué sesgos |
| [politica-datos.md](03-politica-de-datos.md) | Retención, base legal y criterios de publicación |
