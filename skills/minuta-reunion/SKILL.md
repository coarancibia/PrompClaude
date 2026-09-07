---
name: minuta-reunion
description: >-
  Genera minutas/actas de reunión en español a partir de una transcripción
  (.vtt de Teams/Stream, chat de Teams, o texto pegado), con formato fijo
  y detallado: encabezado proyecto/fecha/duración/fuente/alcance, nota de
  trazabilidad sobre hablantes no identificados, participantes con rol,
  objetivo de la sesión, temas en sub-secciones numeradas (2.1, 2.2...)
  con hallazgos/decisiones/acuerdos/riesgos/pendientes, tabla resumen de
  decisiones, pendientes abiertos, próximos pasos, y búsqueda de minutas
  relacionadas en el historial de chats. Usa esta skill SIEMPRE que el
  usuario suba un .vtt, mencione "minuta", "acta de reunión", "resumen de
  la reunión", "transcripción de Teams/Stream", o pegue el chat de una
  llamada y pida un resumen formal de lo tratado, incluso sin decir
  "minuta". No usar para resumir video/audio directamente (Claude no
  puede procesarlos): pide primero la transcripción .vtt o el chat.
---

# Minuta de Reunión

Skill para transformar transcripciones de reuniones (Teams/Stream .vtt, chats, o texto plano) en una minuta profesional con formato fijo y consistente.

## Cuándo usar esta skill

- El usuario sube un archivo `.vtt` (subtítulos/transcripción de Teams o Stream).
- El usuario pega texto de un chat de Teams o una transcripción de reunión y pide una minuta, acta, resumen formal, o "que quede como reunión".
- El usuario pide explícitamente generar/actualizar una minuta.

**No aplica** si el usuario solo tiene el archivo de video/audio (.mp4, .wav, etc.) sin transcripción — Claude no puede ver ni escuchar video/audio. En ese caso, pide la transcripción `.vtt` (se descarga desde la misma página de SharePoint/Stream del video, opción "Transcripción") o el chat de la reunión.

## Formato de salida (obligatorio, no simplificar)

La minuta sigue esta estructura exacta. No la reduzcas a un formato más simple aunque la reunión sea corta — adapta el nivel de detalle dentro de cada sección, pero conserva todas las secciones.

```
# Minuta — [Título descriptivo corto de la sesión]

**Proyecto:** [nombre del proyecto/producto]  **Fecha:** [fecha completa, ej. 26 de agosto de 2026]  **Duración aproximada:** ~[N] minutos
**Fuente:** [nombre del archivo .vtt o de la transcripción usada]  **Alcance:** [país/equipo/producto al que aplica lo discutido]

> Nota de trazabilidad: la transcripción automática no etiquetó a todos los hablantes; las intervenciones marcadas como @1, @2, etc. corresponden a una voz recurrente no identificada por nombre (por el contenido, parece ser [rol/equipo] — inferencia tentativa). No se infiere identidad para no atribuir erróneamente decisiones.

**Participantes identificados:**
- [Nombre completo] ([apodo usado en la reunión, si aplica] — [rol, ej. PD, TL Frontend, BA] [agregar "rol no confirmado" si es una inferencia])
- [...]
- @1 — participante sin identificar en la transcripción

---

## 1. Objetivo de la sesión

[Párrafo breve: qué se vino a revisar/decidir en esta sesión y contra qué se contrastó (ej. legado, otro país, otra landing).]

## 2. Temas tratados y acuerdos

### 2.1 [Nombre del sub-tema]
- **Hallazgo:** [algo que se descubrió/observó durante la revisión]
- **Decisión:** [algo que el grupo decidió zanjar]
- **Acuerdo:** [algo en lo que todos coincidieron]
  - [sub-bullet con detalle o condición asociada]
- **Riesgo:** [algo que se identificó como riesgo, si aplica]
- **Propuesta:** [algo que alguien propuso, aclarando si quedó aceptado o abierto]
- **Pendiente:** [algo que quedó sin cerrar — indicar quién debe resolverlo]

### 2.2 [Siguiente sub-tema]
- ...

(Repite un bloque `2.N` por cada sub-tema/feature/flujo distinto que se haya tratado. No mezcles temas distintos en un mismo bloque. Usa las etiquetas en negrita (**Hallazgo/Decisión/Acuerdo/Riesgo/Propuesta/Pendiente**) solo cuando apliquen — no fuerces las seis en cada bullet, usa la que describe mejor la naturaleza de ese punto.)

## 3. Decisiones / acuerdos (resumen)

| Tema | Decisión |
|---|---|
| [tema corto] | [decisión tomada, en una línea] |

## 4. Pendientes / preguntas abiertas

- [Pregunta o definición que quedó sin resolver, con contexto suficiente para retomarla sin releer toda la minuta]

## 5. Próximos pasos

- [Acción concreta] — [responsable] [fecha si se mencionó]

---

## Minutas relacionadas encontradas (búsqueda en historial de conversaciones)

[Ver sección "Buscar minutas relacionadas" más abajo. Si no se encuentra nada o no hay herramienta de búsqueda de conversaciones pasadas disponible, omite esta sección completa en vez de dejarla vacía o disculparte por ello.]

[Cierra con una línea breve notando cualquier vacío de información relevante detectado, ej.: "No se encontraron minutas previas que traten X — ese dato parece nuevo."]
```

### Notas sobre el formato

- El encabezado de metadatos (Proyecto/Fecha/Duración/Fuente/Alcance) va siempre en dos líneas como en la plantilla, con los labels en negrita.
- **Duración aproximada**: si el input es un `.vtt`, calcúlala restando el primer timestamp de inicio al último timestamp de fin (formato `HH:MM:SS.mmm`). Redondea a minutos.
- **Alcance**: infiérelo del contenido (país, producto, storefront mencionado). Si no es evidente, pregunta al usuario en vez de adivinar.
- La nota de trazabilidad sobre hablantes sin identificar (@1, @2...) va **solo si existen** ese tipo de etiquetas en la transcripción; si todos los hablantes están identificados por nombre, omite la nota completa.
- Para el rol de cada participante: solo escríbelo si se puede inferir razonablemente del contenido (lo que dice, lo que se le pregunta) o si el usuario lo confirma. Si es una inferencia, márcalo explícitamente como "rol no confirmado" — nunca presentes un rol inferido como un hecho.
- Las etiquetas en negrita dentro de "Temas tratados" (**Hallazgo**, **Decisión**, **Acuerdo**, **Riesgo**, **Propuesta**, **Pendiente**) son las categorías estándar; puedes usar otras si la conversación lo pide (ej. **Regla de negocio**), pero mantén el mismo estilo (negrita + dos puntos).
- La tabla de la sección 3 es un resumen ejecutivo — cada fila debe poder leerse sola, sin necesitar el detalle de la sección 2.

## Buscar minutas relacionadas

Antes de cerrar la minuta, si tienes disponible alguna herramienta de búsqueda sobre el historial de conversaciones (revisa tu lista de herramientas por si existe una capacidad de "buscar chats pasados"), búscala usando palabras clave del proyecto/feature tratado en esta sesión (nombres de flujos, features, o el nombre del proyecto). Si encuentras minutas anteriores relacionadas:
- Lístalas con: título breve, fecha, y enlace si el resultado de búsqueda incluye uno.
- No repitas el contenido de esas minutas, solo indica de qué trataban en una línea.

Si no tienes esa herramienta disponible en la sesión actual, omite la sección "Minutas relacionadas encontradas" por completo — no la deje como placeholder vacío ni menciones que "no se pudo buscar".

## Flujo de trabajo

### 1. Obtener y limpiar la transcripción

Si el input es un archivo `.vtt`, NO lo leas línea por línea con el formato crudo (tiene timestamps y cue-ids que ensucian el contexto y duplican texto fragmentado). En su lugar, procésalo con Python para consolidarlo por hablante:

```python
import re
with open('/mnt/user-data/uploads/ARCHIVO.vtt', encoding='utf-8') as f:
    content = f.read()

pattern = re.compile(r'<v ([^>]+)>(.*?)</v>', re.DOTALL)
matches = pattern.findall(content)

lines = []
prev_speaker = None
buffer = ""
for speaker, text in matches:
    text = text.replace('\n', ' ').strip()
    if speaker == prev_speaker:
        buffer += " " + text
    else:
        if prev_speaker is not None:
            lines.append(f"{prev_speaker}: {buffer}")
        prev_speaker = speaker
        buffer = text
if prev_speaker is not None:
    lines.append(f"{prev_speaker}: {buffer}")

with open('/home/claude/transcript_clean.txt', 'w', encoding='utf-8') as f:
    f.write("\n".join(lines))
```

Esto reduce el tamaño del archivo considerablemente (típicamente a menos de un tercio) y agrupa las intervenciones fragmentadas de cada persona en un solo turno de habla, lo que hace la lectura mucho más eficiente y precisa.

Si la transcripción es muy larga (varios miles de líneas), léela en tramos con `view` usando `view_range` hasta cubrir el archivo completo — no te saltes secciones intermedias asumiendo que no importan; los acuerdos y decisiones suelen aparecer distribuidos a lo largo de toda la reunión, no solo al inicio o al final.

Si el input ya es texto plano (chat pegado, transcripción ya limpia), sáltate este paso y trabaja directamente sobre el texto.

### 2. Extraer la información

Mientras lees, identifica:
- **Fecha de la reunión**: si no aparece explícita en el texto, revisa el nombre del archivo (suele incluir fecha en formato YYYYMMDD) o pregunta al usuario. Nunca la inventes.
- **Asistentes**: lista de nombres de hablantes identificados. Si hay hablantes genéricos sin nombre (ej. "@1", "@2" en archivos .vtt de Teams — esto pasa cuando Teams no pudo mapear la voz a un perfil), indícalos como "participante no identificado en la transcripción" en vez de omitirlos o inventarles un nombre.
- **Temas tratados**: agrupa la conversación en bloques temáticos coherentes (no cronológicos turno por turno). Ignora saludos, chistes, comentarios técnicos sobre la llamada ("no me dejaba entrar", "se cortó el audio") y demás ruido conversacional que no aporta contenido de negocio/trabajo.
- **Acuerdos**: decisiones explícitas tomadas por el grupo. Distingue un acuerdo real de una idea que se propuso pero luego se descartó o quedó abierta — si quedó abierta, va en tareas o se omite, no en acuerdos.
- **Tareas / próximos pasos**: quién se compromete a hacer qué, y con qué plazo (si se menciona explícitamente).

### 3. Redactar la minuta

Usa la plantilla exacta definida arriba en "Formato de salida (obligatorio, no simplificar)". No la sustituyas por una versión resumida tipo Fecha/Asistentes/Temas/Acuerdos/Tareas plana — esa versión simple ya no es el estándar; el estándar es la plantilla con encabezado de metadatos, nota de trazabilidad, objetivo de la sesión, sub-temas numerados (2.1, 2.2...) con etiquetas en negrita, tabla resumen de decisiones, pendientes y próximos pasos.

Reglas de redacción, válidas para toda la minuta:
- Usa solo información explícita en la transcripción; no inventes acuerdos, tareas, fechas, responsables ni roles.
- Si un dato no está disponible, escríbelo como tal (ej. "no especificada", "rol no confirmado") — no lo omitas ni lo rellenes con una suposición.
- Tono profesional, conciso, en español.
- No incluyas comentarios fuera de tema, chistes internos, ni saludos de apertura/cierre ni problemas técnicos de la llamada (audio, conexión, etc.).
- Redacta cada punto en tus propias palabras (resumen), nunca como cita textual larga de la transcripción.
- Cada sub-tema de la sección 2 debe corresponder a un flujo/feature/decisión de negocio distinto — no mezcles dos temas en un mismo bloque 2.N.

### 4. Entrega

Por defecto, entrega la minuta como texto en la conversación (markdown), lista para copiar. Solo genera un archivo `.docx` si el usuario lo pide explícitamente o si el contexto deja claro que la necesita como documento formal para compartir/archivar (en ese caso, usa la skill `docx`).
