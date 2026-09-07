---
name: minuta-reunion
description: >-
  Genera minutas/actas de reunión en español a partir de una transcripción
  (archivo .vtt de Teams/Stream, chat de Teams, o texto pegado directamente)
  con el formato fijo Fecha / Asistentes / Temas tratados / Acuerdos / Tareas.
  Usa esta skill SIEMPRE que el usuario suba un archivo .vtt, mencione
  "minuta", "acta de reunión", "resumen de la reunión", "transcripción de
  Teams/Stream", o pegue el chat/transcripción de una llamada y pida un
  resumen o documento formal de lo tratado, incluso si no usa la palabra
  exacta "minuta". No usar para resumir videos o audios directamente,
  ya que Claude no puede procesarlos. Si el usuario solo tiene el video,
  pídele la transcripción .vtt o el chat de la reunión primero.
---

# Minuta de Reunión

Skill para transformar transcripciones de reuniones (Teams/Stream .vtt, chats, o texto plano) en una minuta profesional con formato fijo y consistente.

## Cuándo usar esta skill

- El usuario sube un archivo `.vtt` (subtítulos/transcripción de Teams o Stream).
- El usuario pega texto de un chat de Teams o una transcripción de reunión y pide una minuta, acta, resumen formal, o "que quede como reunión".
- El usuario pide explícitamente generar/actualizar una minuta.

**No aplica** si el usuario solo tiene el archivo de video/audio (.mp4, .wav, etc.) sin transcripción — Claude no puede ver ni escuchar video/audio. En ese caso, pide la transcripción `.vtt` (se descarga desde la misma página de SharePoint/Stream del video, opción "Transcripción") o el chat de la reunión.

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

Usa siempre esta estructura exacta:

```
**MINUTA DE REUNIÓN**

**Fecha:** [fecha o "No especificada"]

**Asistentes:**
- [Nombre 1]
- [Nombre 2]
- [etc.]

**Temas tratados:**
- [Tema 1]: resumen breve de qué se discutió, en prosa, sin transcribir literalmente.
- [Tema 2]: ...

**Acuerdos:**
- [Acuerdo 1]
- [Acuerdo 2]

**Tareas / Próximos pasos:**

| Tarea | Responsable | Fecha límite |
|---|---|---|
| [descripción] | [nombre] | [fecha o "No especificada"] |
```

### Reglas de redacción

- Usa solo información explícita en la transcripción; no inventes acuerdos, tareas, fechas ni responsables.
- Si un dato no está disponible, escribe "No especificado" — no lo omitas ni lo rellenes con una suposición.
- Tono profesional, conciso, en español.
- No incluyas comentarios fuera de tema, chistes internos, ni saludos de apertura/cierre.
- Redacta los temas y acuerdos en tus propias palabras (resumen), nunca como cita textual larga de la transcripción.
- Si la reunión trató varios sub-flujos o features distintos (común en critiques de UX/producto), usa un sub-bullet o tema separado por cada uno en vez de mezclarlos en un solo párrafo genérico.

### 4. Entrega

Por defecto, entrega la minuta como texto en la conversación (markdown), lista para copiar. Solo genera un archivo `.docx` si el usuario lo pide explícitamente o si el contexto deja claro que la necesita como documento formal para compartir/archivar (en ese caso, usa la skill `docx`).
