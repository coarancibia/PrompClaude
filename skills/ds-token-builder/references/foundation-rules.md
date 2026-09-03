# Reglas para las fundaciones del DS

## Arquitectura

Usa hasta tres niveles cuando aporten valor:

- **Primitivos:** valor sin contexto, como `color.magenta.500`, `spacing.400` o `radius.200`.
- **Semánticos:** intención de uso, como `color.text.primary`, `color.surface.brand` o `spacing.component.gap`.
- **Componente:** solo para una decisión repetida y específica, como `button.primary.background.hover`.

Los componentes deben consumir tokens semánticos cuando exista uno adecuado. No crees un token por cada propiedad de cada componente.

## Convención de nombres

- Usa minúsculas y niveles consistentes separados por `/` en Figma o por `.` en exportaciones.
- Nombra los semánticos por intención, no por color o valor visual.
- Mantén la convención existente si es consistente y ya tiene consumidores.
- Los estados `default`, `hover`, `pressed`, `focus`, `selected` y `disabled` son tokens distintos; no son modos.

## Variables y estilos en Figma

- Variables recomendadas: colores, números, strings y booleanos que necesiten alias, modos o reutilización.
- Los estilos pueden agrupar propiedades compuestas: text styles, effect styles y grid styles.
- En Typography, enlaza a variables las propiedades que Figma permita, pero conserva estilos tipográficos consumibles.
- En Elevations, conserva cada sombra completa como estilo si no puede representarse fielmente con variables.
- En Icons, tokeniza tamaños, stroke y colores; los gráficos pertenecen a la librería de íconos, no a una escala de tokens.
- En Layouts, documenta comportamiento responsive además de valores; un breakpoint aislado no define la regla de layout.

## Modos

- Usa modos para significados equivalentes con valores alternativos: light/dark o temas compatibles.
- No uses modos para tamaños responsive ni estados interactivos salvo que la arquitectura existente lo exija y esté documentado.
- Todos los tokens publicados deben resolver en cada modo.

## Criterios por categoría

- **Colors:** separa paleta base de roles semánticos; evita que la UI consuma hex directos.
- **Spacing:** busca una escala coherente, pero no completes pasos inexistentes sin aprobación.
- **Radius y Stroke:** documenta el uso esperado de cada nivel.
- **Overlay:** registra tanto color como opacidad y valida el resultado sobre los fondos reales.
- **Typography:** no omitas line-height ni peso; registra fallback cuando sea relevante.
- **Layouts:** especifica viewport, columnas, margen, gutter, contenedor y cambio entre breakpoints.

## Accesibilidad

- Evalúa colores por combinación semántica de foreground y background, no de manera aislada.
- WCAG AA: texto normal 4.5:1; texto grande 3:1; componentes e información gráfica esencial 3:1.
- Considera texto grande desde 24 px en peso normal o aproximadamente 18.66 px en negrita.
- Verifica default, hover, pressed, focus, selected, disabled y error cuando existan en la fuente.
- No uses solo color para comunicar error, éxito, selección o estado.
- Las combinaciones que no cumplen se reportan y se proponen; solo se cambian con aprobación.
- Registra en una matriz: token de primer plano, token de fondo, ratio, criterio, resultado y contexto de uso.

## Calidad

- Ningún valor nuevo sin fuente o aprobación.
- Ningún alias roto, circular o de tipo incompatible.
- Ningún duplicado con igual intención salvo compatibilidad documentada.
- La cobertura se calcula como usos tokenizados dividido por usos auditados, no por cantidad de tokens creados.
- Cada deprecación incluye reemplazo y consumidores conocidos.
