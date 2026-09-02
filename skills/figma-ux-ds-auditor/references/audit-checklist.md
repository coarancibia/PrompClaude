# Checklist y prioridad de auditoría

## Accesibilidad

- Contraste de texto, iconos, límites y estados sobre el fondo real de uso.
- Información que no dependa únicamente del color.
- Focus visible y distinguible de hover, selected y error.
- Área interactiva y separación suficiente para touch.
- Labels visibles, instrucciones y errores comprensibles.
- Orden de lectura y jerarquía coherentes.
- Contenido legible con zoom, escalado de texto y reflow.
- Estados de carga, progreso y cambios dinámicos comunicados.
- Semántica, teclado, manejo de foco y anuncios para lectores de pantalla documentados para desarrollo.

Usa WCAG 2.2 AA como referencia predeterminada salvo que el proyecto defina otro estándar. No certifiques cumplimiento solo desde el archivo de diseño.

## Responsive y contenido extremo

- Mobile, desktop y breakpoints incluidos en el alcance.
- Auto Layout, constraints y resizing coherentes.
- Texto corto, largo, vacío, localizado o dinámico.
- Wrapping y truncamiento sin pérdida de información esencial.
- Scroll, sticky, overlays, teclado móvil y áreas seguras cuando correspondan.
- Prioridad de contenido y acciones en espacios reducidos.

## Rúbrica de prioridad

### Crítico

Bloquea el objetivo principal, puede causar daño o pérdida, incumple una condición esencial de accesibilidad o seguridad, o impide entregar/desarrollar el flujo.

### Alto

Provoca una falla importante, confusión frecuente, recuperación difícil, inconsistencia grave del sistema o un problema responsive que afecta el uso real.

### Medio

Reduce claridad, eficiencia o consistencia, pero existe una ruta razonable para completar la tarea.

### Bajo

Ajuste menor de limpieza, orden, naming, documentación o consistencia secundaria sin impacto relevante en la tarea.

## Calidad del hallazgo

Un hallazgo válido incluye:

- ubicación exacta;
- evidencia observable;
- impacto para usuario, diseño o desarrollo;
- recomendación concreta sin rediseñar innecesariamente;
- fuente del Design System cuando aplique;
- nivel de confianza y dato pendiente cuando exista incertidumbre.
