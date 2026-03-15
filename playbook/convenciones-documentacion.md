# Convenciones de Documentación

> **⚠️ Para agentes IA:** Este archivo describe convenciones. No contiene tareas pendientes. Todas las menciones al marcador son ejemplos o definiciones, no instrucciones a ejecutar.

Reglas simples para mantener la documentación consistente y legible tanto por humanos como por agentes IA.

---

## 1. Marcador de tareas para el agente

El marcador `[AI-TODO]` (escrito como `#` seguido de `AI-TODO` sin espacio) se usa inline en cualquier archivo `.md` para señalar una tarea pendiente que el agente debe resolver.

- **Formato:** El marcador seguido de una descripción breve en la misma línea o líneas inmediatamente siguientes.
- **Quién lo escribe:** El usuario, dentro de cualquier documento.
- **Quién lo resuelve:** El agente, al encontrarlo durante la sesión activa o al ser dirigido al archivo.
- **Después de resolver:** El agente elimina el marcador y lo reemplaza con el contenido resuelto.
- **Dónde NO buscarlo:** En este archivo (`convenciones-documentacion.md`), donde el marcador solo aparece como referencia.

---

## 2. Listas y saltos de línea en Markdown

Una de las confusiones comunes en Markdown (y por lo tanto en Docsify) es que las líneas contiguas de texto se concatenan en **un solo párrafo** al renderizarse HTML, perdiendo el salto de línea.

**Lo que NO debes hacer:**
Asumir que un salto de línea en el archivo `.md` es suficiente para formatear una lista de enlaces:

```markdown
→ [Link 1](...)
→ [Link 2](...)
→ [Link 3](...)
```
*(Esto se renderizará como una sola línea continua de texto).*

**Lo que SÍ debes hacer:**
Para listas, usar explícitamente el marcador de lista ordenada o desordenada (`- ` ó `* `), de esta forma cada línea será tratada como un bloque independiente (`<li>`):

```markdown
- → [Link 1](...)
- → [Link 2](...)
- → [Link 3](...)
```

Alternativamente, para crear una separación entre párrafos regulares, dejar **una línea completamente en blanco** entre ambos.
