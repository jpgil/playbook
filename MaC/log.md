# Log

> **Sugerencia de escritura:** Priorizar la acción y el valor aportado sobre el nombre del archivo para una lectura más fluida del progreso. Sigue los ejemplos anteriores.

## 2026-03-14 - Configuración inicial
- Creación del repo en base a las ideas de playbook recopiladas en el playbook de MaC https://github.com/pewma-ai/mac/playbook
- Configuración de capas MaC y refactorización del README.md.
- Creación de Skills de agente (`readme-MaC`, `amigo-MaC`) radicadas en el directorio `MaC/procesos/`.
- `AGENTS.md` redirigido a `amigo-MaC.md` como punto exclusivo de entrada para agentes IA y cadena de lectura documentada en el playbook.
- Branch `feat/01-definicion-playbook` creado con las configuraciones iniciales consolidadas (incluyendo formato de convención local en git).

## 2026-03-15 - Reestructuración del concepto de Playbook
- Manifiesto del playbook redactado en `docs/playbook_rules.md`: 4 pilares (Simetría Literaria, Divulgación Progresiva, Alta Portabilidad, Fronteras de Gobernanza).
- **Decisión:** Distribución por defecto será Clonado Directo / Template Repo, priorizando simplicidad sobre submódulos o symlinks. Documentado en `docs/playbook_distribution.md`.
- **Decisión:** Reestructuración en dos capas: guías operativas en la raíz del repo, documentación filosófica/conceptual en `docs/`.
- Todas las guías movidas de `playbook/` a la raíz. Directorio `playbook/` eliminado (la URL `playbook/playbook/` era redundante).
- `configuracion-agentes.md` renombrado a `agents_good-practices.md` como estándar agnóstico para convenciones de agentes IA.
- 4 playbooks reescritos con anatomía estándar (callout → problema → solución → fronteras → recursos), eliminando datos específicos de proyectos anteriores.
- `README.md` raíz reescrito como landing page con tabla-índice de guías operativas.
