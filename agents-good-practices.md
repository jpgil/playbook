---
title: Buenas Prácticas para Agentes en un Repositorio
description: Cómo configurar estándares únicos de contexto y documentar reglas operativas dentro de un repositorio.
date: 2026-03-15
source: https://github.com/jpgil/playbook/blob/main/agents-good-practices.md
---
# Buenas Prácticas para Agentes en un Repositorio

## El problema

Cada herramienta de codificación IA tiene su propio archivo de instrucciones:

| Herramienta | Archivo nativo |
|---|---|
| Claude Code | `CLAUDE.md` |
| Gemini CLI | `GEMINI.md` |
| Cursor | `.cursorrules` → `.cursor/rules/*.mdc` |
| GitHub Copilot | `.github/copilot-instructions.md` |
| OpenAI Codex CLI | `AGENTS.md` |
| Windsurf | `.windsurfrules` |

El contenido es casi idéntico en todos. Mantenerlos separados es un problema de sincronización garantizado.

## La solución: `AGENTS.md` como estándar

`AGENTS.md` es el estándar emergente. Adoptado por la Linux Foundation (diciembre 2025) bajo la Agentic AI Foundation (AAIF). Más de 60.000 repositorios open source lo usan (marzo 2026).

### Compatibilidad nativa

- ✅ OpenAI Codex CLI (lo originó)
- ✅ Cursor (también lee `.cursorrules` y `.cursor/rules/`)
- ✅ GitHub Copilot
- ✅ Windsurf
- ✅ Gemini CLI (configurable vía `settings.json`)
- ✅ Aider, Zed, Warp, RooCode, Kilo Code
- ⚠️ Claude Code — no nativo; workaround: referenciar desde `CLAUDE.md`

---

## Estructura recomendada

```
/
├── AGENTS.md              ← fuente de verdad compartida
├── .cursorrules           ← apunta a AGENTS.md (compatibilidad legacy)
├── *.md                   ← guías operativas (playbooks)
└── README.md              ← índice del repositorio
```

### Cadena de lectura del agente

Un agente **no necesita leer todo el repo**. Sigue una cadena progresiva:

1. Lee `AGENTS.md` (obligatorio al inicio).
2. Consulta el `README.md` para localizar guías relevantes.
3. Lee solo la guía específica que aplica a la tarea.

> **💡 Principio:** Cuantas menos instrucciones simultáneas, mejor rendimiento del agente. Solo cargar lo necesario.

---

## Anatomía de un buen `AGENTS.md`

Las secciones recomendadas, en orden:

1. **Descripción del proyecto** — Qué es, en una línea.
2. **Comandos** — Build, test, lint. Lo que el agente necesita ejecutar.
3. **Estructura del proyecto** — Solo si no es obvia.
4. **Convenciones y estilo** — O un link al playbook que las define.
5. **Límites en tres niveles** — Crítico para prevenir daños:

| Nivel | Significado | Ejemplo |
|---|---|---|
| **Hacer siempre** | Obligación automática | *Ejecutar tests antes de commitear.* |
| **Preguntar primero** | Requiere confirmación | *No agregar dependencias sin aprobación.* |
| **Nunca hacer** | Prohibición absoluta | *Nunca commitear credenciales.* |

6. **Contexto adicional** — Links a recursos, playbooks o documentación externa.

> **💡 Tip:** Si el repositorio tiene un playbook con guías detalladas, el `AGENTS.md` puede ser muy breve: descripción, comandos, límites, y un link al índice de guías. Evitas duplicar contenido.

### Reglas de escritura efectiva

- **Brevedad.** ~150 líneas máximo. Los archivos largos entierran lo importante.
- **Ejemplos sobre descripciones.** Un fragmento real vale más que párrafos.
- **Iterar, no planificar.** El mejor `AGENTS.md` crece con el tiempo — agregar una regla la segunda vez que el agente comete el mismo error (¡y volver a leerlo!)
- **Tratar como código.** Revisar en PRs, versionar, mantener actualizado.

---

## Cómo replicar en otro repositorio

1. Crear `AGENTS.md` en la raíz como fuente de verdad.
2. Si se usa Claude Code: crear `CLAUDE.md` que referencie `@AGENTS.md`.
3. Si se usa Cursor legacy: crear `.cursorrules` con el mismo contenido o una referencia.
4. Colocar guías operativas como archivos `.md` con un `README.md` que las indexe.
5. En el `AGENTS.md`, incluir la instrucción de consultar el índice antes de implementar.

---

## Agentes
Esta tabla debe ser respetada por agentes IA.

| Nivel | Regla |
|---|---|
| **Hacer siempre** | Incluir los tres niveles de límites en todo `AGENTS.md`. |
| **Preguntar primero** | Antes de modificar `AGENTS.md` en un repo ajeno, confirmar con el responsable. |
| **Nunca hacer** | Nunca incluir credenciales, tokens o secrets en archivos de contexto. |

---

## Recursos

- Especificación AGENTS.md: https://agents.md
- GitHub Blog (análisis de 2.500+ repos): https://github.blog/ai-and-ml/github-copilot/how-to-write-a-great-agents-md-lessons-from-over-2500-repositories/
- Guía completa: https://www.aihero.dev/a-complete-guide-to-agents-md
