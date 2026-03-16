# Playbooks Abiertos

> Tu conocimiento operativo, versionado, portable y listo para compartir.

---

## Por qué hacer un Playbook Personal

Cada profesional acumula años de decisiones, trucos y convenciones que definen cómo trabaja. Ese conocimiento suele quedarse en la cabeza (intransferible), en wikis abandonadas (desactualizadas) o en archivos de configuración atados a un solo proyecto (no portables).

Un Playbook Personal cambia eso. Es un repositorio de guías en Markdown que:

- **Viajan contigo** — de proyecto en proyecto, de empresa en empresa.
- **Funcionan para humanos y máquinas** — un agente IA lee la misma guía que lees tú, sin necesidad de formatos separados.
- **Mejoran con el uso** — cada proyecto nuevo alimenta de vuelta tus prácticas.
- **Democratizan conocimiento** — al publicarlos abiertamente, otros pueden adoptar, adaptar y contribuir.

> *"Si un humano no disfruta leer la guía, está mal escrita. La máquina se adapta al formato humano, no al revés."*

---

## Documentación

- [Reglas de un Playbook Personal](playbook_rules.md) — Las 4 reglas fundamentales: Markdown puro, modularidad, portabilidad y fronteras de gobernanza.
- [Estrategias de distribución](playbook_distribution.md) — Cómo compartir tu playbook: submódulos, symlinks o plantillas.

---

## Ejemplo real

Este repositorio es un playbook en acción: el de **[@jpgil](https://github.com/jpgil)**. Puedes explorarlo, tomar las guías que te sirvan, o usarlo como plantilla para crear el tuyo.

👉 [Ver las guías operativas](https://github.com/jpgil/playbook#guías-operativas)

---

## Inspiración y referencias

- [How to write a great agents.md](https://github.blog/ai-and-ml/github-copilot/how-to-write-a-great-agents-md-lessons-from-over-2500-repositories/) — GitHub Blog, análisis de 2.500+ repositorios.
- [Evaluating AGENTS.md](https://www.infoq.com/news/2026/03/agents-context-file-value-review/) — ETH Zurich, 2026. Por qué los archivos de contexto monolíticos hacen más daño que bien.
- [Management as Code (MaC)](https://pewma-ai.github.io/mac/) — Método de gestión en texto plano que inspiró la gobernanza de este proyecto.

---

## Notas de implementación del sitio

> **Estado actual:** El sitio usa Docsify (renderizado en el cliente, sin build).
>
> **Pendiente de evaluación:** Migrar a Hugo o Jekyll para obtener SEO nativo, indexación HTML estática y soporte multilingüe integrado (es/en/pt vía estructura de directorios `i18n`). Hugo tiene ventaja en velocidad de build y soporte de idiomas out-of-the-box (`config.toml` con `[languages]`). Si se decide migrar, crear una guía operativa para documentar el proceso.