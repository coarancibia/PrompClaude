---
name: medir-ejecucion-skill
description: Mide una tarea de diseño realizada con otra skill de Claude y compárala con el mismo trabajo manual. Úsala cuando pidan medir un handoff, tiempos, dedicación humana, ahorro o tokens. También permite registrar una referencia manual.
---

# Medir una ejecución

Versión 1.0. Acompaña la tarea desde el inicio hasta que la persona apruebe el entregable. Conserva el registro en la conversación y devuelve una fila para la planilla del equipo.

## Abrir el registro

Identifica el caso, la skill de trabajo y su versión si se conoce. Define qué significa «listo» en una frase. Para un handoff podría ser «desarrollo puede identificar estados, interacciones y pendientes del flujo». Reutiliza los datos que entregue la persona. La referencia manual puede agregarse al cierre.

Antes de preparar insumos, toma la hora con un reloj accesible. Si careces de reloj, pide iniciar un cronómetro y responder «partí». Si los insumos ya estaban preparados, registra ese alcance y usa una referencia manual equivalente. Si la tarea ya terminó, acepta marcas documentadas o tiempos declarados indicando su fuente. Deja como «sin dato» lo que falte.

## Acompañar la tarea

En modo asistido, usa la skill de trabajo indicada. Si está fuera de tu alcance, pide que la persona la active o la adjunte. En modo manual, acompaña solo la medición mientras la persona realiza el trabajo.

Al entregar el primer resultado, toma la hora o pide marcar una vuelta en el cronómetro. Incluye reintentos, revisión y correcciones hasta que la persona diga «listo» o confirme aprobación. Si hay una interrupción ajena a la tarea, registra su duración y descuéntala solo cuando se conozca, aplicando el mismo criterio al caso manual. Si se abandona, conserva el registro como incompleto.

## Cerrar y comparar

Toma la hora de aprobación o pide el tiempo final del cronómetro. Pregunta una sola vez por los minutos de trabajo activo de la persona, incluyendo preparación, revisión y correcciones. Identifica si son medidos o estimados. Distingue esa dedicación del tiempo transcurrido.

Registra los tokens de entrada y salida de todos los intentos y el modelo solo cuando la herramienta o la persona aporte datos verificables. Usa diferencias entre contadores acumulados únicamente si el intervalo pertenece por completo al caso. Identifica si el consumo incluye la propia medición. Cuando solo exista un total del chat o un dato parcial, descríbelo en notas y deja «sin dato» en las columnas que no puedas atribuir a la ejecución.

Compara casos de alcance, calidad y punto de cierre equivalentes. Calcula ahorro de tiempo total = minutos manuales totales − minutos asistidos totales. Calcula ahorro de dedicación solo si también conoces los minutos activos en ambos métodos. Conserva diferencias negativas. Si algún valor es estimado, etiqueta la comparación como estimada. Sin base comparable o aprobación, deja el ahorro pendiente.

Si se conoce el esfuerzo de creación y prueba de la skill, regístralo una sola vez por versión, aparte de las ejecuciones. Para estimar en cuántos usos se recupera, divide ese esfuerzo en minutos por el ahorro de dedicación humana por uso y redondea hacia arriba. Hazlo solo si ese ahorro es positivo.

## Entrega

Resume el resultado en una frase. Entrega luego un bloque TSV con encabezado y una fila por ejecución, con estas columnas en orden. Expresa los tiempos en minutos y usa «sin dato» para valores desconocidos.

Fecha | Caso | Método | Skill y versión | Estado | Criterio de aprobación | Min al primer resultado | Min totales | Min activos persona | Min manuales de referencia | Ahorro total min | Ahorro humano min | Tokens entrada | Tokens salida | Modelo | Fuente de tiempos y tokens | Correcciones y notas

Ejemplo de activación: «Usa medir-ejecucion-skill junto con mi skill de handoff. Mide desde que preparemos los insumos hasta que revise el entregable y te diga listo. Al final dame la fila para la planilla».
