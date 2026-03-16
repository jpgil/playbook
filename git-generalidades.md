# Convenciones Git

> **Para humanos y agentes IA.**
> Reglas para commits, branches y operaciones Git en un repositorio.

---

## El problema

Sin convenciones explícitas, el historial de Git se convierte en ruido: mensajes ambiguos, branches con nombres inconsistentes, y operaciones destructivas accidentales. Un agente IA sin reglas claras puede hacer `force push` o commitear en `main` directamente.

---

## Convenciones

### Commits

- **Prefijos obligatorios (Conventional Commits):** `feat:`, `fix:`, `docs:`, `refactor:`, `chore:`, `test:`, `ci:`.
- **Cuerpo del mensaje:** idioma del equipo (consistente).
- **Formato del cuerpo:** tiempo presente, modo imperativo.

Ejemplos:
```
docs: agregar guía de Docsify al playbook
feat: implementar sidebar de navegación
fix: corregir enlaces rotos en documentación
refactor: simplificar estructura de AGENTS.md
```

### Branches

- `main` — rama principal, siempre desplegable.
- Trabajo en progreso en branches descriptivos con prefijo y kebab-case:
  ```
  docs/agregar-guia-docsify
  feat/base-conocimiento
  fix/enlaces-rotos
  ```

### Identidad local

Si el repositorio pertenece a un contexto distinto al global de Git (ej. cuenta personal vs corporativa), configurar la identidad local al clonar:

```bash
git config user.name "Tu Nombre"
git config user.email "tu@email.com"
```

---

## Fronteras

| Nivel | Regla |
|---|---|
| **Hacer siempre** | Usar prefijo de Conventional Commits en cada mensaje. |
| **Preguntar primero** | Antes de ejecutar `git push`. |
| **Nunca hacer** | Rebase o force push en ramas públicas sin confirmación explícita. Nunca modificar historial público. |

---

## Recursos

- Conventional Commits: https://www.conventionalcommits.org
- Git branching model: https://nvie.com/posts/a-successful-git-branching-model/
