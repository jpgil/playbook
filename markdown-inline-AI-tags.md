---
title: Usar TAGS en Markdown
description: Reglas de documentación en Markdown y marcadores estructurados para designar tareas pendientes.
date: 2026-03-15
source: https://github.com/jpgil/playbook/blob/main/markdown_practicas.md
---
# Usar TAGS en Markdown
Un TAG ayuda a ordenar las notas más adelante, y también dan pistas a los agentes IA para ejecutar acciones.

# TAGS sugeridos

Los tags usan `#` seguido de una palabra clave en mayúsculas, sin espacio entre `#` y la palabra. Este formato permite buscarlos con `grep -r "#TODO\|#AI-TODO\|#WISH\|#IDEA" *.md` o herramientas equivalentes.

- `#ASK-USER (the question)`: el agente dialoga con el usuario, y cuando la pregunta esta respondida sin ambigüedad modifica el archivo **de inmediato**. Al crear un nuevo archivo el agente puede decidir agregar ASK-USER de modo inline cuando la ambiguedad no puede resolverse.
- `#AI-TODO (expected actions)`: el agente decide cuidadosamente que hacer y ejecuta **de inmediato**, luego transforma el AI-TODO en un `#TODO` con un texto pidiendo al usuario revisar el resultado, y modifica el archivo.
- `#TODO user notes`: notas que el usuario deja para sí, no requieren acción pero cada cierto tiempo un recordatorio en medio de un chat.
- `#WISH user notes`: deseo o idea a futuro. No requiere acción inmediata. El agente lo tiene en cuenta como contexto pero no actúa sobre ello salvo que el usuario lo pida.
- `#IDEA user notes`: idea técnica o de producto. Similar a `#WISH` pero orientado a implementación. No requiere acción. El agente lo registra como contexto y puede agrupar ideas relacionadas si se le pide.
