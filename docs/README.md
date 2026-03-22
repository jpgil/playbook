# Open Playbooks

> Tu conocimiento operativo, versionado, portable y listo para compartir.

---

## Plan del sitio (pendiente de implementación)

Este sitio (`jpgil.github.io/playbook`) es la cara pública del movimiento **Open Playbooks**: la idea de que cada profesional publique sus prácticas operativas como archivos Markdown abiertos, consumibles por humanos y agentes IA por igual.

### Páginas planificadas

#### 1. Portada (este README)
- Qué es un Open Playbook y por qué importa.
- La visión: una comunidad donde cada profesional tiene su `github.com/<usuario>/playbook`.
- Link al repo de ejemplo (este mismo: `github.com/jpgil/playbook`).

#### 2. Reglas de un Playbook (`playbook_rules.md`) — ya existe
- Las 4 reglas fundamentales: Markdown puro, modularidad, portabilidad, fronteras de gobernanza.
- Anatomía de una buena guía.
- Cuándo dividir, cuándo fusionar.
- **Convención adoptada (2026-03-22):** Front matter YAML opcional y mínimo (`title`, `description`, `date`, `source`) en cada playbook. Compatible con SKILLS de agentes y preparado para motores estáticos (Hugo/Jekyll).

#### 3. Estrategias de distribución (`playbook_distribution.md`) — ya existe
- Cómo llevar tus playbooks a otros proyectos: copia directa, submódulos, symlinks.
- Recomendación por defecto: copiar lo que necesitás.

#### 4. Cómo lanzar tu Open Playbook (`como-empezar.md`) — por crear
- Guía paso a paso para que alguien arranque su propio repo.
- Crear el repo, elegir licencia, escribir el primer playbook.
- Estructura mínima viable: README + 1 guía + LICENSE.
- Cómo publicar el sitio con Docsify (link a la guía `github_pages-docsify.md`).
    - [ ] No, usar un motor estático, very si es mejor Jekyll o Hugo. 

#### 5. Cómo mantenerlo (`mantenimiento.md`) — por crear
- Cuándo agregar una guía nueva vs. actualizar una existente.
- El ciclo bidireccional: proyecto → playbook → proyecto.
- Versionado y changelog (¿vale la pena?).

#### 6. Roadmap de la idea (`roadmap.md`) — por crear
- Internacionalización (es/en/pt).
- Registro comunitario de playbooks (¿un awesome-list?).
- Evaluación de migrar de Docsify a Hugo/Jekyll para SEO e i18n nativos.
- Integración con ecosistema de agentes: ¿cómo un agente descubre y consume playbooks de terceros?

#TODO: agregar instrucciones para el AGENTS.md
#TODO: wish list, cosas que me gustaria que tenga en el futuro, no es lo mismo que un roadmap.
#TODO: Como agregar comentarios en linea de los usuarios?
#TODO: Mecanismo de retroalimentacion de los usuarios

---

## Estado actual

- **Motor del sitio:** Docsify (renderizado en cliente, sin build).
- **Contenido existente:** `playbook_rules.md`, `playbook_distribution.md`.
- **Contenido por crear:** `como-empezar.md`, `mantenimiento.md`, `roadmap.md`.
- **Decisión pendiente:** Evaluar migración a Hugo/Jekyll para SEO nativo y soporte multilingüe.

---

## Notas de implementación

> El sitio Docsify ya está funcional. Las páginas nuevas se crean como archivos `.md` en esta carpeta y se registran en `_sidebar.md`. No requiere build ni deploy manual — cada `git push` actualiza el sitio.