# user-story-builder

## Qué hace

Esta skill transforma requerimientos, definiciones de negocio, flujos, diseños, tickets relacionados y contexto funcional en una Historia de Usuario (HU) clara, trazable y accionable para Producto, UX, Desarrollo y QA.

La estructura se basa en el formato utilizado en historias como PRM-3445: parte desde la necesidad del usuario, documenta el problema de experiencia, divide el flujo en secciones cuando existe más de un comportamiento relevante, separa criterios de aceptación de reglas de negocio, vincula assets de diseño y deja explícitas métricas, dependencias y stakeholders cuando la información está disponible.

La skill NO debe inventar información para completar campos.

---

## Cuándo utilizarla

Utilizar cuando se necesite:

- Crear una HU desde cero a partir de contexto, notas o requerimientos.
- Convertir definiciones de UX o negocio en una HU estructurada.
- Documentar flujos con múltiples estados o casuísticas.
- Preparar una HU para hand-off a Desarrollo y QA.
- Ordenar información proveniente de Figma, Jira, reuniones o documentación.
- Revisar si una HU existente está completa.
- Separar criterios de aceptación, reglas de negocio, errores, métricas y dependencias.

No utilizarla para:

- Documentar exclusivamente una decisión visual menor.
- Crear una tarea técnica sin impacto o comportamiento de usuario.
- Inventar reglas de negocio que no estén confirmadas.
- Convertir automáticamente una iniciativa grande en una sola HU.

---

## Principio general

La HU debe permitir que una persona que no participó en las reuniones pueda entender:

1. Qué necesita el usuario.
2. Qué problema de experiencia se está resolviendo.
3. Qué alcance tiene.
4. Qué comportamientos debe soportar.
5. Qué reglas condicionan esos comportamientos.
6. Qué errores o estados alternativos existen.
7. Dónde están los diseños.
8. Qué tickets o reglas están relacionados.
9. Cómo se medirá o validará el resultado.
10. Quién debe aprobar o validar la solución.

---

# Flujo de trabajo de la skill

## Paso 1 — Analizar el requerimiento antes de redactar

Determinar si el contenido corresponde a:

- Épica
- Feature
- Historia de Usuario
- Tarea técnica

Si el requerimiento contiene varios objetivos independientes, NO crear una HU gigante.

En ese caso:

1. Explicar que el alcance debiera dividirse.
2. Proponer la separación.
3. Identificar dependencias entre las HU.
4. Redactar la HU principal solo si el usuario lo solicita o si es posible identificarla claramente.

---

# Estructura base de salida

## 1. Historia de usuario

Utilizar siempre:

**COMO** [tipo de usuario]

**QUIERO** [acción o necesidad]

**PARA** [beneficio o resultado esperado]

### Reglas

- El COMO debe representar al usuario o actor real del flujo.
- El QUIERO debe describir la necesidad, no una implementación visual.
- El PARA debe explicar el valor o resultado esperado.
- Evitar repetir la misma acción en QUIERO y PARA.

---

## 2. Problema de experiencia

**Categoría: Estrategia y contexto**

Explicar:

- Qué ocurre actualmente.
- Qué problema o ambigüedad existe.
- Qué reglas o condiciones hacen complejo el flujo.
- Qué necesita comprender o poder hacer el usuario.
- Qué parte del producto se ve afectada.

Debe explicar el problema antes de describir la solución.

### Profundidad esperada

Cuando corresponda, indicar:

- [ ] Flujo end-to-end
- [ ] Variante por país
- [ ] Cambio puntual
- [ ] Flujo nuevo
- [ ] Ajuste de experiencia
- [ ] Migración / homologación

No marcar opciones sin evidencia.

---

# 3. División por secciones funcionales

Si la HU contiene varios estados o comportamientos relacionados dentro del mismo objetivo, dividir el detalle por secciones.

Ejemplo:

- Sección 1 — Habilitación del input y estado inicial
- Sección 2 — Aplicación de cupón de extensión
- Sección 3 — Aplicación de cupón de descuento
- Sección 4 — Método de pago
- Sección 5 — Validaciones y errores

Cada sección debe representar una parte coherente del flujo.

No crear secciones artificiales si la HU es simple.

Cada sección puede contener:

### Descripción breve

Una frase que explique qué comportamiento cubre.

### Criterios de aceptación

Definir comportamientos observables y verificables.

Ejemplos de redacción:

- El input se habilita únicamente cuando...
- Si el usuario ya cuenta con..., entonces...
- Al aplicar correctamente..., se muestra...
- Cuando el servicio responde con error..., se informa...

Los criterios deben poder ser validados por QA.

### Reglas de negocio y casuísticas

Separar las reglas que condicionan el comportamiento.

Ejemplos:

- Requiere renovación automática activa.
- Un cupón de extensión bloquea únicamente otra extensión.
- El pago con Puntos aplica solo a determinado tipo de cupón.
- El límite de cupones bloquea nuevos ingresos.

No repetir como regla una simple decisión visual.

### Copy

Agregar solo cuando exista copy definido o relevante para la implementación.

No inventar textos.

### Assets

Cuando exista diseño, indicar:

**Pantalla**

| Estado / pantalla | Desktop | Mobile |
|---|---|---|
| Nombre del estado | Link Figma | Link Figma |

Conservar los links originales.

---

# 4. Estados y errores

Cuando el flujo lo requiera, validar explícitamente:

- Estado inicial
- Loading / skeleton
- Éxito
- Error de validación
- Error de servicio
- Disabled / bloqueado
- Máximo alcanzado
- Sin información
- Estados alternativos
- Diferencias entre métodos de pago
- Diferencias por país

Los estados deben ser mutuamente excluyentes cuando el flujo así lo determine.

Para errores de servicio, incluir:

1. Condición que genera el error.
2. Feedback visible para el usuario.
3. Posibilidad de reintento, si está definida.
4. Cobertura esperada en QA.

No inventar soluciones técnicas.

---

# 5. Árbol de decisión

Incluir cuando existan múltiples reglas condicionales que hagan difícil comprender el flujo solo leyendo criterios.

Formato recomendado:

```text
Inicio
 └─ ¿Condición principal?
      ├─ No → comportamiento
      └─ Sí →
           ├─ Estado A → comportamiento
           ├─ Estado B → comportamiento
           └─ Estado C → comportamiento
```

El árbol debe resumir reglas ya documentadas.

No introducir reglas nuevas dentro del árbol.

---

# 6. Métrica de éxito

**Categoría: Estrategia y contexto**

Incluir solo cuando exista definición o una propuesta explícita.

Formato:

| KPI principal | Meta esperada | Cómo se mide |
|---|---|---|
| KPI | Meta | Fuente / validación |

Si la métrica aún no está validada, indicar:

**Propuesta — pendiente de validación con Negocio.**

Ejemplos:

- Claridad del estado aplicado.
- Tasa de éxito del flujo.
- Cobertura de feedback en estados bloqueantes.
- Manejo de error de servicio.

No inventar porcentajes ni metas.

---

# 7. País y variantes

Indicar explícitamente cuando corresponda:

**País:** Chile / Brasil / Colombia / Perú / Transversal

Si la HU aplica únicamente a una variante, dejarlo explícito.

Ejemplo:

**Cambio de copy y actualización entre países:** No aplica — HU acotada a variante Chile.

Si existen diferencias por país:

- Separar reglas.
- Separar copy cuando corresponda.
- No asumir que una definición de Chile aplica a otros países.

---

# 8. Flujos e insumos de diseño

Agregar una tabla de trazabilidad cuando existan recursos relacionados.

| Recurso | Link / referencia |
|---|---|
| Archivo Figma | URL |
| Ticket de origen | Jira |
| Regla cruzada | Jira / Confluence |
| Tarea contenedora | Jira |
| Documento funcional | URL |

Conservar las referencias originales entregadas por el usuario.

No inventar relaciones entre tickets.

---

# 9. Equipo y stakeholders

**Categoría: Factibilidad y alineación**

Incluir cuando estén identificados.

| Rol | Nombre / equipo | Responsabilidad |
|---|---|---|
| UX | Persona / equipo | Definición de flujo, estados y hand-off |
| PO / BA | Persona / equipo | Aprobación de criterios y reglas |
| TL Frontend | Persona / equipo | Factibilidad técnica |
| Backend | Persona / equipo | Servicios y reglas técnicas |
| QA | Persona / equipo | Cobertura y validación |

Solo incluir personas y responsabilidades que estén disponibles en el contexto.

No inventar stakeholders.

---

# 10. Pendientes por definir

Si falta información necesaria, agregar:

## Pendientes por definir

- Pregunta pendiente.
- Regla que requiere validación.
- Copy aún no definido.
- Métrica sin meta.
- Error sin comportamiento acordado.
- Dependencia pendiente.

No completar vacíos con supuestos.

---

# Reglas de redacción

1. Utilizar lenguaje claro y directo.
2. Mantener terminología del producto.
3. Evitar lenguaje excesivamente técnico en la Historia de Usuario.
4. Separar comportamiento funcional de implementación técnica.
5. Separar criterios de aceptación de reglas de negocio.
6. No inventar copy.
7. No inventar reglas.
8. No inventar métricas.
9. No inventar responsables.
10. Mantener referencias de Figma, Jira y documentación.
11. Escribir pensando en Producto, UX, Desarrollo y QA.
12. Evitar duplicar la misma regla en distintas secciones salvo que sea necesario para comprender el flujo.
13. Si una regla ya está documentada en otro ticket, referenciarla y resumir solo lo necesario.
14. Mantener explícitas las variantes por país.
15. Identificar errores de servicio y estados bloqueantes cuando afecten la experiencia.

---

# Criterios de calidad antes de entregar

Antes de generar la HU final, revisar:

- [ ] La Historia de Usuario explica usuario, necesidad y valor.
- [ ] Existe un problema de experiencia entendible.
- [ ] El alcance está claro.
- [ ] Las secciones representan partes coherentes del flujo.
- [ ] Los criterios de aceptación son verificables.
- [ ] Las reglas de negocio están separadas.
- [ ] Los principales estados están cubiertos.
- [ ] Los errores relevantes están contemplados.
- [ ] Los diseños están vinculados cuando existen.
- [ ] Los tickets relacionados están referenciados.
- [ ] Las variantes por país están explícitas.
- [ ] Las métricas no se presentan como confirmadas si aún son propuesta.
- [ ] Los stakeholders están identificados cuando existe esa información.
- [ ] Los pendientes están visibles.
- [ ] No se inventó información.

---

# Formato final recomendado

```markdown
# [Título de la HU]

## 1. Historia de usuario

**COMO** ...

**QUIERO** ...

**PARA** ...

## 2. Problema de experiencia

**Categoría:** Estrategia y contexto

[Contexto]

**Profundidad esperada:** [...]

## Sección 1 — [Nombre]

[Descripción]

### Criterios de aceptación

- ...

### Reglas de negocio y casuísticas

- ...

### Copy

- ...

### Assets

| Pantalla | Desktop | Mobile |
|---|---|---|
| ... | ... | ... |

## Sección 2 — [Nombre]

[...]

## Árbol de decisión

[...]

## Métrica de éxito

**Categoría:** Estrategia y contexto

**Propuesta — pendiente de validación con Negocio.**

| KPI principal | Meta esperada | Cómo se mide |
|---|---|---|
| ... | ... | ... |

## País y variantes

[...]

## Flujos e insumos de diseño

| Recurso | Link / referencia |
|---|---|
| ... | ... |

## Equipo y stakeholders

**Categoría:** Factibilidad y alineación

| Rol | Nombre / equipo | Responsabilidad |
|---|---|---|
| ... | ... | ... |

## Pendientes por definir

- ...
```

---

# Decisiones que siempre requieren revisión humana

La skill puede estructurar y detectar vacíos, pero NO debe decidir por sí sola:

- Reglas comerciales.
- Límites de uso.
- Elegibilidad.
- Políticas de renovación.
- Medios de pago permitidos.
- Copy legal.
- Métricas objetivo.
- Priorización.
- Responsables.
- Factibilidad técnica.
- Comportamientos no documentados.

Cuando uno de estos puntos no esté definido, debe marcarse como pendiente.

---

# Nombre recomendado

**user-story-builder**

Motivo:

- Mantiene coherencia con nombres como `component-builder` y `naming-validator`.
- Es entendible fuera del contexto local de Cencosud.
- Describe que la skill construye y estructura Historias de Usuario.
- Permite reutilizarla en distintos productos, países y equipos.

Nombre del archivo recomendado:

**SKILL.md**

Ruta sugerida en GitHub:

```text
/skills/user-story-builder/SKILL.md
```
