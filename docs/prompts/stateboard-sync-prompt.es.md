# Prompt de sincronización de Stateboard

[English](stateboard-sync-prompt.md) · [中文](stateboard-sync-prompt.zh.md)

Este es el punto de entrada sin instalación de Stateboard. Copia el prompt de abajo y reemplaza el contenido entre corchetes.

```text
Organiza los siguientes proyectos o contexto de conversación en un tablero de estado de proyecto y sincronízalo con el destino que indique.

Contenido que quiero organizar:
[Por ejemplo: conversaciones de los últimos 60 días de Codex / ChatGPT / Claude / DeepSeek / WorkBuddy que pueda aportar o que puedas leer; el proyecto actual; una carpeta de proyecto; mis tareas existentes; varios chats de proyecto pegados]

Sincronizar con:
[Por ejemplo: Dida/TickTick, Notion, Google Calendar, Feishu/Lark, DingTalk, WeCom o solo Markdown]

Ubicación de destino:
[Por ejemplo: la lista "Project Control" en Dida/TickTick; una página/base de datos de Notion; "crea una lista nueva llamada XXX"; si solo es Markdown, escribe "responde directamente aquí"]

Actualización automática:
[No necesaria / diaria HH:MM / semanal día HH:MM. Si no hay una hora clara, escribe "no necesaria"]

Reglas:
- Usa solo contenido que puedas leer, buscar o que yo haya proporcionado. Si faltan conversaciones o materiales del proyecto, dime qué falta.
- Juzga primero el estado del proyecto a partir de evidencia. No conviertas directamente el historial de chat en muchas tareas.
- Por defecto, crea o actualiza solo una tarea de estado por proyecto real. Incluye progreso actual, riesgos/bloqueos, próximos pasos y evidencia.
- Mantén solo 3-5 próximos pasos realmente útiles por tarea.
- Busca tareas existentes antes de escribir. Si ya existe una tarea de estado del mismo proyecto, actualízala en vez de crear un duplicado.
- Si el entorno actual no puede escribir en la herramienta de destino, genera una versión Markdown lista para copiar y explica el bloqueo.
- Si pido actualización automática pero no doy frecuencia y hora exacta, pregunta primero. No asumas una hora por defecto. Si el entorno actual no puede crear la automatización, da instrucciones listas para copiar en lugar de afirmar que ya fue creada.
- No escribas tokens, webhook secrets, license keys, credenciales privadas ni identificadores privados del sistema de destino.
- Responde y escribe el contenido de destino en el idioma de mi solicitud, salvo que pida explícitamente salida bilingüe.
- Al terminar, dime qué se creó, qué se actualizó, cómo se verificó y qué sigue necesitando mi confirmación.
```

## Entrada mínima de prueba

```text
Contenido que quiero organizar:
El proyecto Stateboard actual o el proyecto en <your-project-path>

Sincronizar con:
Dida/TickTick

Ubicación de destino:
Crea una lista nueva llamada Project Status Test

Actualización automática:
No necesaria
```
