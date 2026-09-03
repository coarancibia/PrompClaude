---
name: ds-token-builder
description: "Crea, organiza, documenta y audita los tokens fundacionales de un Design System en Figma: Colors, Layouts, Spacing, Radius, Stroke, Elevations, Overlay, Icons y Typography. Úsala cuando se necesite construir o mantener variables y estilos del DS; no para diseñar pantallas ni modificar componentes de producto."
---

# DS Token Builder

Construye las fundaciones del Design System a partir de fuentes reales. No inventes escalas, valores o reglas de marca. Distingue siempre entre lo encontrado, lo inferido y lo propuesto.

## Alcance

Trabaja con estas categorías, según lo que exista en el proyecto:

1. **Colors:** paletas base y roles semánticos para texto, fondos, superficies, bordes, íconos, feedback y estados.
2. **Layouts:** grid, columnas, márgenes, gutters, contenedores, breakpoints y anchos máximos.
3. **Spacing:** escala de separación, padding y gap.
4. **Radius:** radios de bordes por escala o intención.
5. **Stroke:** grosores y estilos de borde.
6. **Elevations:** sombras y niveles de profundidad.
7. **Overlay:** colores y opacidades de scrims, modales y fondos superpuestos.
8. **Icons:** tamaños, stroke, color y reglas de uso. No recrees cada ícono como token.
9. **Typography:** familia, tamaño, peso, line-height, letter-spacing y estilos tipográficos.

Lee [references/foundation-rules.md](references/foundation-rules.md) antes de proponer la estructura o crear tokens.

## Referencia de estructura, no de contenido

El archivo DS Token · Prime puede usarse únicamente como ejemplo de organización visual de las fundaciones:

- Colors: https://www.figma.com/design/mMM5ogwjtFkvYkaIJliy3g/Ds-Token-%C2%B7-Prime?node-id=1-6633
- Typography: https://www.figma.com/design/mMM5ogwjtFkvYkaIJliy3g/Ds-Token-%C2%B7-Prime?node-id=21-14
- Resto de fundaciones: https://www.figma.com/design/mMM5ogwjtFkvYkaIJliy3g/Ds-Token-%C2%B7-Prime?node-id=49-997

Usa esta referencia para comprender qué información conviene mostrar y cómo agrupar Colors, Layouts, Spacing, Radius, Stroke, Elevations, Overlay, Icons y Typography. **No copies sus colores, tipografía, nombres, escalas ni valores a otro proyecto.** Los tokens siempre deben construirse con las fuentes y decisiones del DS actual.

## Inputs

Obtén solo los datos disponibles y solicita lo que falte cuando sea decisivo:

- archivo o enlace de Figma del proyecto;
- guía de marca, UI kit o referencias que sean fuente de verdad;
- categorías incluidas en el alcance;
- plataformas y breakpoints;
- modos o temas, como light/dark o distintas marcas;
- formato final, si además de Figma se requiere JSON, Tokens Studio o CSS.

La fuente puede ser un Figma organizado, pantallas existentes, una guía de marca, una lista de valores, imágenes, archivos JSON/CSS o una combinación. No exijas que el usuario tenga previamente una página de tokens.

Si faltan datos, crea una propuesta estructural con campos pendientes y preguntas concretas. No completes valores visuales por intuición. Si hay varios proyectos o marcas, identifica cuál DS corresponde a cada uno y nunca apliques los tokens de otro DS por similitud.

## Flujo obligatorio

### 1. Modo lectura

Antes de modificar Figma:

- revisa las fuentes y declara cuál tiene prioridad;
- inventaría variables, estilos y valores sueltos de cada categoría;
- detecta duplicados, inconsistencias, huecos, nombres confusos y tokens deprecados;
- identifica qué puede representarse como variable y qué debe mantenerse como estilo compuesto;
- reúne desde las fuentes disponibles los colores, nombres, escalas y valores HEX/RGBA; si no hay nombres, propón una nomenclatura sin alterar los valores;
- identifica la familia tipográfica y las combinaciones disponibles de tamaño, peso, line-height y letter-spacing; marca como pendiente cualquier propiedad ausente;
- presenta el diagnóstico, la arquitectura propuesta y el plan completo.

No crees, renombres, elimines, publiques ni apliques variables hasta recibir aprobación explícita. Si el conector de Figma solo permite lectura, entrega una especificación implementable y no afirmes que realizaste cambios.

### 2. Propuesta

Entrega una tabla por categoría con:

| Token propuesto | Nivel | Tipo | Valor o alias | Modo | Uso | Origen | Estado |
|---|---|---|---|---|---|---|---|

Usa `Encontrado`, `Inferido` o `Propuesto` en Estado. Incluye también:

- estructura de colecciones y grupos;
- equivalencias entre lo actual y lo propuesto;
- decisiones que requieren revisión humana;
- impacto sobre variables, estilos y consumidores existentes;
- orden de implementación.

Pregunta: **“¿Apruebas este plan para que realice los cambios?”**

### 3. Implementación aprobada

Tras la aprobación:

1. Crea primero los tokens base o primitivos.
2. Crea tokens semánticos como alias de los primitivos.
3. Configura los modos aprobados.
4. Crea estilos compuestos para tipografía, elevaciones, grids u otros casos que Figma no represente completamente con una sola variable.
5. Aplica los tokens únicamente en el alcance aprobado.
6. Conserva nombres ya consumidos por desarrollo, salvo migración aprobada.
7. Marca tokens antiguos como deprecados y documenta su reemplazo; no los elimines sin autorización específica.

Para colores, crea variables primitivas con los valores aprobados y variables semánticas mediante alias. Para tipografía, crea variables para las propiedades compatibles y estilos tipográficos completos para que puedan aplicarse desde Figma. No reemplaces la familia tipográfica detectada por otra. Si el usuario todavía no tiene una paleta o escala aprobada, presenta primero una propuesta y espera validación.

No desprendas instancias, rompas componentes ni alteres pantallas para completar el trabajo.

### 4. Validación

Comprueba:

- nombres únicos y tipos correctos;
- alias válidos y sin ciclos en todos los modos;
- cobertura de los valores auditados;
- consistencia entre variables, estilos y documentación;
- contraste solo cuando existan contexto, fondo, tamaño y peso suficientes;
- contraste de texto normal mínimo 4.5:1 y texto grande mínimo 3:1 para nivel AA;
- contraste mínimo 3:1 para íconos informativos, bordes de controles y estados visuales esenciales;
- legibilidad de Typography en tamaños, pesos y line-height documentados, sin declarar accesible una tipografía solo por su familia;
- que el significado no dependa únicamente del color;
- que no existan modificaciones fuera del alcance.

Si una combinación no cumple, no alteres silenciosamente la paleta: informa el par evaluado, su ratio, el criterio esperado y una propuesta de ajuste para aprobación.

## Entrega final

Resume los cambios reales, tokens creados o modificados, elementos deprecados, elementos no tocados, incidencias pendientes y evidencia de validación. Adjunta el archivo exportable solicitado cuando corresponda.
