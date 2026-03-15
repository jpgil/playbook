# Convenciones Git

> **Para humanos y agentes IA.**
> Reglas para commits, branches y operaciones Git en este repositorio.

---

## Inicialización del repositorio

Al clonar o inicializar el repositorio por primera vez, configurar la identidad local:

```bash
git config user.name "Juan Pablo Gil R."
git config user.email "juanpablogil@gmail.com"
```

---

## Commits

- **Prefijos obligatorios (en inglés):** `feat:`, `fix:`, `docs:`, `refactor:`, `chore:`.
- **Cuerpo del mensaje:** idioma español.
- **Formato del cuerpo:** tiempo presente, modo imperativo.

Ejemplos:
```
docs: agregar guía de Docsify al playbook
feat: implementar sidebar de navegación
fix: corregir enlaces rotos en procesos-mac
refactor: simplificar estructura de AGENTS.md
```

## Branches

- `main` — rama principal, siempre desplegable.
- Trabajo en progreso en branches descriptivos. Nombres en español con kebab-case:
  ```
  docs/agregar-guia-docsify
  feat/base-conocimiento
  fix/enlaces-historias
  ```

## Operaciones restringidas

- **`git push`**: siempre preguntar al usuario antes de ejecutar.
- **Rebase o force push**: nunca sin confirmación explícita.
- **Modificar historial público**: nunca.
