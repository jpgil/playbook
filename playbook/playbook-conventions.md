---
title: Convenciones para Playbooks
description: Cómo escribir, nombrar y organizar guías dentro de este repositorio.
date: 2026-03-22
source: https://github.com/jpgil/playbook/blob/main/playbook/playbook-conventions.md
---
# Convenciones para Playbooks

Cómo escribir y organizar playbooks en este repositorio. Estas convenciones aplican a todas las guías de la raíz; el directorio `docs/` queda fuera de alcance en caso de que el usuario decida tener documentación propia.

## Contexto
Las buenas prácticas, acuerdos y políticas de un proyecto suelen quedar dispersos en documentos externos o conversaciones. Cada vez que alguien nuevo se incorpora,  persona o agente IA, el conocimiento debe transferirse de nuevo. Mantener un directorio `playbook/` dentro de cada repositorio resuelve esto: las convenciones viajan con el código, son versionables y cualquier agente puede comprenderlas de inmediato.

## Estructura de un playbook

Plantilla de referencia para un playbook:

```markdown
---
title: Nombre descriptivo
description: Una línea que explique qué cubre.
date: 2026-03-22
source: https://github.com/jpgil/playbook/blob/main/nombre-del-archivo.md
---

# Nombre descriptivo

Frase de contexto: qué resuelve esta guía.

## Contexto

Por qué existe esta guía. Qué sale mal sin ella, o qué motivó crearla. Breve.

## (Cuerpo libre)

El contenido principal de la guía. La estructura interna es libre: puede ser una lista de convenciones, pasos numerados, ejemplos comentados, etc.

## Agentes *(opcional)*
Esta tabla debe ser respetada por agentes IA.

| Nivel | Regla |
|---|---|
| **Hacer siempre** | ... |
| **Preguntar primero** | ... |
| **Nunca hacer** | ... |

## Checklist *(opcional)*

- [ ] Verificación 1
- [ ] Verificación 2

## Recursos *(opcional)*

- [Referencia](url)
```

### Recomendaciones

- **Front matter YAML obligatorio.** Los campos `title` y `description` son compatibles con el formato SKILLS de agentes. `date` refleja la última actualización significativa. `source` apunta al archivo específico, no al repositorio — así quien recibe una copia sabe de dónde vino.
- **Markdown puro, prosa primero.** El contenido debe ser completamente comprensible con metadatos mínimos.
- **Un tema, un archivo.** Si supera ~150 líneas, probablemente cubre dos temas y debe dividirse.
- **Ejemplos sobre descripciones.** Un fragmento de código real vale más que tres párrafos.
- **Iterar, no planificar.** La guía crece con el uso. Crear la versión mínima y refinarla después.

## Nombres de archivo

- Minúsculas, separados por guiones (`-`), **de lo más general a lo más particular**. Esto permite agrupar por subdirectorios en el futuro si es necesario.
  - ✅ `git-commits.md`, `git-branching.md`, `obsidian-sync-gdrive.md`
  - ❌ `commits-de-git.md`, `sync.md`, `MiGuia.md`
- Sin prefijos numéricos ni categorías en el nombre. El índice (`README.md`) organiza.
- El nombre debe ser suficientemente descriptivo para que se pueda inferir por título si la guía es relevante antes de abrirla.
- El slug (nombre sin extensión) debe ser apto para convertirse en ruta de subdirectorio. Si las guías crecen, `git-commits.md` podría moverse a `git/git-commits.md` sin cambiar la lógica del nombre. Se mantiene el nombre completo porque los playbooks de otros repositorios tal vez no tienen necesidad de separar.
- Nombre de archivo en inglés, aunque el contenido esté en español.

## README

Toda guía nueva debe registrarse en [`README.md`](README.md). Cada entrada extrae del nombre de archivo y front matter:
```markdown
- **[file_name1.md](./file_name1.md)**: ({date}) {description}
- **[dir/file_name2.md](dir/file_name2.md)**: ({date}) {description}
```

## Agentes
Esta tabla debe ser respetada por agentes IA.

| Nivel | Regla |
|---|---|
| **Hacer siempre** | Incluir front matter YAML completo (`title`, `description`, `date`, `source`) al crear o modificar una guía. |
| **Hacer siempre** | Registrar toda guía nueva en el `README.md` con una línea descriptiva. |
| **Preguntar primero** | Dividir una guía existente en dos archivos (puede afectar links y el índice). |
| **Preguntar primero** | Renombrar un archivo de guía (rompe referencias externas y el campo `source`). |
| **Preguntar primero** | Crear subdirectorios para agrupar playbooks cuando la cantidad de guías lo justifique. |
| **Nunca hacer** | Crear guías sin front matter YAML. |
| **Nunca hacer** | Usar prefijos numéricos o categorías en los nombres de archivo. |

## Recursos

- [Open Playbooks](https://pewma-ai.github.io/open-playbook/)