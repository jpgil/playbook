# Reglas de un Playbook Personal

> **Para humanos y agentes IA.**
> Este documento define qué es un Playbook Personal, qué problema resuelve y las reglas que rigen su estructura. Léelo antes de crear o modificar guías en este repositorio.

---

## El problema

El conocimiento operativo de un profesional —cómo nombra variables, cómo estructura commits, qué patrones evita, cómo redacta documentación— vive en tres lugares ineficientes:

| Lugar | Falla |
|---|---|
| La cabeza del experto | Intransferible. Se pierde al cambiar de proyecto o de persona. |
| Wikis y documentos sueltos | Se desactualizan. Nadie los lee en el momento de ejecutar. |
| Archivos de reglas IA (`.cursorrules`, `AGENTS.md`) | Atados al repositorio. No viajan con el individuo. |

Un **Playbook Personal** resuelve esto: es un repositorio de guías en Markdown que externaliza ese conocimiento en archivos portátiles, modulares y consumibles tanto por humanos como por agentes IA, sin separación artificial entre ambas audiencias.

El ciclo es bidireccional: llevas tus prácticas a nuevos proyectos, y la experiencia ganada en esos proyectos alimenta de vuelta el playbook. Además, al publicarlo abiertamente:

- **Democratizas conocimiento** — otros desarrolladores pueden adoptar y adaptar tus guías.
- **Fortaleces tu perfil profesional** — demuestras las prácticas que realmente sigues, no solo las que enuncias.
- **Generas comunidad** — un método estandarizado de compartir conocimiento crea cohesión entre profesionales.

---

## Reglas fundamentales

### 1. Markdown puro, prosa primero

Las guías se redactan en **Markdown estándar**. Sin YAML frontmatter obligatorio, sin esquemas JSON, sin formatos inventados para la máquina.

- El texto explica el *porqué*, no solo el *qué*. Un agente que entiende la razón detrás de una convención la aplica mejor que uno que memoriza una regla ciega.
- La estructura del documento (encabezados, listas, tablas, bloques de código) es suficiente para que un agente lo parsee. No necesita metadatos adicionales.

> **💡 Principio:** Si un humano no disfruta leer la guía, está mal escrita. La máquina se adapta al formato humano, no al revés.

### 2. Modularidad: un tema, un archivo

Cada guía cubre **un solo dominio** (ej. convenciones de Git, estilo de documentación, configuración de agentes). Razones:

- **Evitar el colapso de contexto.** Los LLMs pierden rendimiento cuando procesan demasiadas instrucciones simultáneas ([ETH Zurich, 2026](https://www.infoq.com/news/2026/03/agents-context-file-value-review/)). Guías cortas y enfocadas permiten inyección selectiva.
- **Facilitar adopción parcial.** Otro profesional puede tomar solo las guías que le sirvan sin cargar con el playbook completo.

**Regla práctica:** Si una guía supera ~150 líneas, probablemente cubre dos temas y debe dividirse.

### 3. Portabilidad: el playbook viaja con el individuo

Las convenciones pertenecen al profesional, no al repositorio. El playbook está diseñado para ser copiado, clonado o enlazado en cualquier proyecto nuevo.

```
# Forma más simple: copiar las guías
cp -r ~/mi-playbook/*.md ./nuevo-proyecto/

# Alternativa avanzada: submódulo Git
git submodule add https://github.com/usuario/playbook.git
```

El playbook no asume tecnología, lenguaje ni framework. Sus guías pueden cubrir desde estándares de TypeScript hasta convenciones de redacción literaria o metodologías de gestión.

### 4. Política débil con fronteras duras

Las guías son **recomendaciones inteligentes**, no mandatos rígidos. El humano o el agente pueden desviarse si el contexto lo justifica. Pero toda guía debe dejar claro qué **no** es negociable.

Usa la estructura de tres niveles cuando aplique:

| Nivel | Significado | Ejemplo |
|---|---|---|
| **Hacer siempre** | Obligación de rutina | *Siempre ejecutar linter antes de commit.* |
| **Preguntar primero** | Requiere confirmación humana | *No agregar dependencias sin aprobación.* |
| **Nunca hacer** | Prohibición absoluta | *Nunca commitear credenciales o secrets.* |

No todas las guías necesitan los tres niveles. Solo inclúyelos cuando la guía toque acciones con consecuencias irreversibles.

---

## Anatomía de una guía del playbook

Una buena guía sigue este esqueleto (no es una plantilla rígida, es una orientación):

1. **Título y callout de audiencia** — Quién debe leerla y para qué.
2. **El problema** — Qué sale mal sin esta guía. Breve.
3. **La solución / Convenciones** — Reglas concretas con ejemplos reales.
4. **Fronteras** *(opcional)* — Hacer siempre / Preguntar primero / Nunca hacer.
5. **Recursos** *(opcional)* — Links de referencia.

> **💡 Regla de escritura:** Ejemplos sobre descripciones. Un fragmento real vale más que tres párrafos explicativos. Iterar, no planificar: la guía crece con el uso.

---

## Índice del playbook

El archivo README.md del repositorio actúa como índice. Cada guía nueva debe registrarse ahí con una línea descriptiva. Un agente consulta el índice para decidir qué guía leer antes de ejecutar una tarea (ver [Cadena de lectura del agente](../agents_good-practices.md)).


## Referencias

- GitHub Blog — Análisis de 2.500+ repositorios con AGENTS.md: [How to write a great agents.md](https://github.blog/ai-and-ml/github-copilot/how-to-write-a-great-agents-md-lessons-from-over-2500-repositories/)
- ETH Zurich — Evaluación empírica de archivos de contexto para agentes de código: [Evaluating AGENTS.md](https://www.infoq.com/news/2026/03/agents-context-file-value-review/)
- Método MaC (Management as Code) — Inspiración para la gobernanza de este playbook: [pewma-ai.github.io/mac](https://pewma-ai.github.io/mac/)