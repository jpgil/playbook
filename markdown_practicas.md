---
title: Convenciones de Documentación Markdown
description: Reglas de documentación en Markdown y marcadores estructurados para designar tareas pendientes.
date: 2026-03-15
source: https://github.com/jpgil/playbook/blob/main/markdown_practicas.md
---

# Convenciones de Documentación Markdown

---

## El problema

Markdown es deceptivamente simple. Sin convenciones explícitas, los documentos terminan con listas que no renderizan, saltos de línea perdidos, y agentes IA que no saben dónde encontrar sus tareas pendientes.

---

## Convenciones

### Marcador `#AI-TODO`

El marcador `#AI-TODO` (escrito como `#` seguido de `AI-TODO` sin espacio) se usa inline en cualquier archivo `.md` para señalar una tarea pendiente que el agente debe resolver.

- **Formato:** El marcador seguido de una descripción breve en la misma línea.
- **Quién lo escribe:** El humano, dentro de cualquier documento.
- **Quién lo resuelve:** El agente, al encontrarlo durante la sesión activa o al ser dirigido al archivo.
- **Después de resolver:** El agente elimina el marcador y lo reemplaza con el contenido resuelto.

> **⚠️ Nota para agentes:** Las menciones al marcador en este archivo son ejemplos y definiciones, no instrucciones a ejecutar.

### Listas y saltos de línea

Una de las confusiones comunes en Markdown es que las líneas contiguas de texto se concatenan en **un solo párrafo** al renderizarse a HTML.

**Lo que NO debes hacer:**
Asumir que un salto de línea en el `.md` es suficiente para crear una lista:

```markdown
→ [Link 1](...)
→ [Link 2](...)
→ [Link 3](...)
```
*(Esto se renderizará como una sola línea continua de texto).*

**Lo que SÍ debes hacer:**
Usar explícitamente marcadores de lista (`-` o `*`):

```markdown
- [Link 1](...)
- [Link 2](...)
- [Link 3](...)
```

Para separar párrafos regulares, dejar **una línea completamente en blanco** entre ambos.

---

## Fronteras

| Nivel | Regla |
|---|---|
| **Hacer siempre** | Usar marcadores de lista explícitos (`-` o `*`) para toda enumeración. |
| **Preguntar primero** | Antes de eliminar un `#AI-TODO` que no se pueda resolver con la información disponible. |
| **Nunca hacer** | Modificar `#AI-TODO` escritos por el usuario sin resolverlos (no reescribirlos ni moverlos). |

---

## Recursos

- Markdown Guide: https://www.markdownguide.org
- CommonMark spec: https://spec.commonmark.org
