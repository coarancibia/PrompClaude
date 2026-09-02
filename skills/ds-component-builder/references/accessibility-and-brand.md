# Accesibilidad y marca

Consulta esta referencia al definir, crear o revisar un componente. Aplica solo los criterios relevantes para su función.

## Accesibilidad

### Percepción visual

- Verifica contraste de texto, iconos informativos, bordes y estados respecto del fondo real de uso.
- Usa como referencia WCAG 2.2 AA: 4.5:1 para texto normal, 3:1 para texto grande y 3:1 para componentes gráficos o límites necesarios para comprender o interactuar.
- No comuniques estado, error, selección o éxito únicamente mediante color.
- Considera zoom, escalado de texto, reflow y contenido extenso.
- Evita truncar información esencial sin una alternativa accesible.

### Interacción

- Define un focus visible y diferenciado de hover, selected y error.
- Mantén orden de lectura y navegación coherentes.
- Considera teclado, touch y tecnologías asistivas.
- Revisa el tamaño del objetivo interactivo conforme al estándar del proyecto; si no existe, usa 24 × 24 CSS px como mínimo WCAG y recomienda áreas más amplias para interfaces táctiles.
- No uses gestos complejos como único método de operación.
- Asegura que controles deshabilitados, carga y progreso comuniquen su estado de forma comprensible.

### Semántica y contenido

- Define nombre accesible, rol, estado y valor esperados para controles.
- Mantén labels visibles cuando el contexto pueda perderse; no uses placeholder como sustituto del label.
- Vincula errores con el campo correspondiente y explica cómo resolverlos.
- Describe en el handoff las interacciones que Figma no puede validar: teclado, anuncios de lectores de pantalla, manejo de foco, semántica HTML y regiones dinámicas.

## Marca

- Identifica primero la fuente oficial: variables, tokens, librería o guía de marca.
- Diferencia color de marca de color funcional. Un color corporativo no reemplaza automáticamente tokens de error, warning, success, focus o superficie.
- Mapea los colores por función semántica y por modo; no copies valores de una captura.
- Conserva el contraste aunque un color oficial necesite una combinación, superficie o tratamiento alternativo.
- Usa logos e iconos oficiales sin deformar proporciones ni recrearlos manualmente.
- Si varias marcas conviven, respeta las reglas declaradas de jerarquía y convivencia. Si no existen, detente y solicita definición.
- No crees nuevos tokens de marca sin aprobación de gobernanza.

## Evidencia y límites

- Registra el token, estilo o recurso exacto utilizado.
- Señala cualquier valor local o equivalencia no confirmada.
- No certifiques accesibilidad basándote únicamente en Figma.
- Separa hallazgos de diseño, requisitos para desarrollo y pruebas posteriores.
