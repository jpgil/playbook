---
title: Convenciones de Markdown en Obsidian
description: Sintaxis específica de Obsidian para checklists, callouts y plegado que difiere del Markdown estándar.
date: 2026-03-22
source: https://github.com/jpgil/playbook/blob/main/obsidian-markdown-conventions.md
---

# Convenciones de Markdown en Obsidian

Sintaxis propia de Obsidian que complementa el Markdown estándar. Útil para mantener consistencia al escribir notas que luego se leen en otras herramientas.

## Checklists

Requieren `- ` antes de los corchetes:
- `- [ ]` Sin completar
- `- [x]` Completada

## Callouts

En Obsidian cada callout asigna un color e icono distinto:

- **Generales:** `note`, `info`, `todo`
- **Resúmenes:** `abstract`, `summary`, `tldr`
- **Destacados:** `tip`, `hint`, `important`
- **Éxito:** `success`, `check`, `done`
- **Consultas:** `question`, `help`, `faq`
- **Precaución:** `warning`, `caution`, `attention`
- **Problemas críticos:** `failure`, `fail`, `missing`, `danger`, `error`, `bug`
- **Otros:** `example`, `quote`, `cite`

### Plegado (Collapse)

Puedes hacer que el callout se pueda expandir y contraer añadiendo un signo `+` o `-` junto al tipo:

- `> [!info]+` (Inicia desplegado)
- `> [!info]-` (Inicia plegado)

---

## Recursos

- Obsidian Callouts: https://help.obsidian.md/Editing+and+formatting/Callouts
- Obsidian Markdown: https://help.obsidian.md/Editing+and+formatting/Basic+formatting+syntax
