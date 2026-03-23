---
title: Usar TAGS en Markdown
description: Marcadores inline estructurados para designar tareas pendientes, preguntas y acciones de agentes.
date: 2026-03-22
source: https://github.com/jpgil/playbook/blob/main/markdown-inline-AI-tags.md
---

# Usar TAGS en Markdown

Un TAG ayuda a ordenar las notas más adelante, y también dan pistas a los agentes IA para ejecutar acciones.

## Contexto

En documentos Markdown extensos es fácil perder el rastro de decisiones pendientes, preguntas abiertas e ideas. Sin marcadores explícitos, un agente no puede distinguir entre una nota informativa y una acción esperada.

## TAGS sugeridos

Los tags usan `#` seguido de una palabra clave en mayúsculas, sin espacio entre `#` y la palabra. Este formato permite buscarlos con `grep -r "#TODO\|#AI-TODO\|#WISH\|#IDEA" *.md` o herramientas equivalentes.

- `#ASK-USER (the question)`: el agente dialoga con el usuario, y cuando la pregunta está respondida sin ambigüedad modifica el archivo **de inmediato**. Al crear un nuevo archivo el agente puede decidir agregar ASK-USER de modo inline cuando la ambigüedad no puede resolverse.
- `#AI-TODO (expected actions)`: el agente decide cuidadosamente qué hacer y ejecuta **de inmediato**, luego transforma el AI-TODO en un `#TODO` con un texto pidiendo al usuario revisar el resultado, y modifica el archivo.
- `#TODO user notes`: notas que el usuario deja para sí, no requieren acción pero cada cierto tiempo un recordatorio en medio de un chat.
- `#WISH user notes`: deseo o idea a futuro. No requiere acción inmediata. El agente lo tiene en cuenta como contexto pero no actúa sobre ello salvo que el usuario lo pida.
- `#IDEA user notes`: idea técnica o de producto. Similar a `#WISH` pero orientado a implementación. No requiere acción. El agente lo registra como contexto y puede agrupar ideas relacionadas si se le pide.

---

## Fronteras

| Nivel | Regla |
|---|---|
| **Hacer siempre** | Respetar los tags existentes al editar un archivo. |
| **Hacer siempre** | Ejecutar `#AI-TODO` de inmediato y transformar en `#TODO` para revisión del usuario. |
| **Preguntar primero** | Antes de eliminar o cambiar un `#TODO` o `#ASK-USER` existente sin que esté resuelto. |
| **Nunca hacer** | Ignorar un `#ASK-USER` sin responder ni un `#AI-TODO` sin ejecutar. |
