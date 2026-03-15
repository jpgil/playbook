# Reglas de MaC (Management as Code)

> Este documento define las pautas de gestión para este repositorio. En el caso de agentes IA, las reglas son imperativas y deben seguirse como un "prompt" operativo y ser leídas desde [MaC/ritual_de_sesion.md](./ritual_de_sesion.md) cada 30 minutos como máximo.

---

## §1. Ritual de Inicio de Sesión

Al iniciar cualquier sesión, el agente ejecuta estos pasos **en orden y antes de cualquier otra acción**:

1. Crear (o reanudar) el archivo `MaC/sesiones/sesion-YYYY-MM-DD.md` con información mínima (solo la hora de inicio).
2. **Actualizar `MaC/README.md`** según [`procesos/readme-MaC.md`](procesos/readme-MaC.md)
3. Preguntar al **(USUARIO)** por el objetivo y por qué iniciaron la sesión.
4. **Esperar** la respuesta del **(USUARIO)**.
5. Al recibir los objetivos, el agente revisa `MaC/log.md`, `MaC/roadmap.md` y las **Deudas abiertas** de la sesión más reciente para contextualizar la solicitud.
6. El agente luego propone un desglose de los objetivos en un conjunto de tareas (Checklist) y se lo presenta al **(USUARIO)**.
7. Solo después de que el **(USUARIO)** apruebe la lista de tareas, el agente actualiza el archivo de sesión con los Objetivos y la Checklist.

> El ritual asegura que la sesión comience con un propósito claro dictado por el usuario. **No se ejecutan tareas** y el plan no se finaliza hasta que el **(USUARIO)** apruebe la checklist propuesta.

---

## §2. Planificación y Ejecución

- Cualquier implementación requiere que el plan esté **descrito previamente** en la sesión activa.
- Al reanudar el trabajo, el agente busca la última checklist no completada en los tres archivos de sesión más recientes (orden cronológico).
- Si no hay una sesión activa, el agente crea una llamada `MaC/sesiones/sesion-YYYY-MM-DD.md`.
- Registra en el encabezado de cada sesión el **tiempo cronológico** (inicio, interrupciones, fin) y el **tiempo efectivo** de trabajo. Utiliza el formato de sesiones anteriores como referencia.

### Antes de implementar

Antes de ejecutar un ítem del Plan de Acción, consultar [`playbook/README.md`](../playbook/README.md) para verificar si existe una guía relevante al tema que se va a tocar. Si hay una guía, leerla antes de proceder. Esto aplica tanto para humanos como para agentes IA.

### Plantilla de Sesión

Utiliza [`sesiones/sesion-TEMPLATE.md`](sesiones/sesion-TEMPLATE.md) como base para cada nueva sesión.

---

## §3. Registros Obligatorios

### `log.md` — Registro histórico

`log.md` es la memoria a largo plazo del proyecto. Alguien que lea solo este archivo debería entender la evolución del proyecto sin abrir ninguna sesión. Al escribir en él:

- Agrupar entradas por fecha: `## YYYY-MM-DD - Título descriptivo`.
- Registrar **hitos** (una o dos líneas que describan qué cambió y por qué importa) y **decisiones importantes** (como hechos consumados, sin el contexto operativo).
- Seguir el tono y formato de las entradas existentes.
- Tanto el agente como el usuario escriben en el registro. Si el usuario agrega una entrada, no la modifiques.

### `## Log de la sesión` — Registro operativo

El `## Log de la sesión` dentro de cada `sesion-*.md` es el registro detallado de lo que realmente pasó: tareas ejecutadas, cambios de opinión, configuraciones, descubrimientos. Va siempre **al final del archivo de sesión**, después de la Introspección.

- **Se actualiza de forma inmediata**: cada vez que el agente completa una acción relevante (archivo creado, decisión tomada, cambio de rumbo), la registra en el log de la sesión sin esperar al cierre.
- Las **decisiones importantes aparecen en ambos sitios**: en `log.md` como hecho consumado (una línea), y en el log de la sesión con el contexto operativo (por qué, qué alternativas se descartaron).

### Correcciones y Mejoras

- Se registran en la `sesion-*.md` activa, bajo `## Correcciones` y `## Mejoras`, con síntoma/causa/solución.
- Las correcciones se identifican como `C-XX`, las mejoras como `M-XX` (numeración secuencial por sesión).
- Los cambios en la documentación y las reglas **no requieren una entrada en `MaC/sesiones/`**; solo se registran en `log.md`.

### Coherencia Documental

Al modificar cualquier documento, verifica si el cambio afecta a otros documentos en el repositorio y propaga las actualizaciones necesarias. Esto incluye referencias cruzadas, supuestos compartidos y decisiones que se mencionan en más de un lugar.

---

## §4. Cierre de Sesión

Se activa **solo cuando el usuario lo indica explícitamente**. Flujo estricto:

1. Registrar la **hora de finalización** en el encabezado de la sesión.
2. Completar la sección `## Introspección de la Sesión` siguiendo la estructura definida en [`sesion-TEMPLATE.md`](sesiones/sesion-TEMPLATE.md).
3. Se hace a un lado para que el usuario proporcione sus reflexiones en `### Reflexiones`. El usuario puede enviar múltiples mensajes. **Confirmar recepción sin tomar medidas** hasta que el usuario devuelva el control.
4. Al recibir el control, redactar las reflexiones del usuario y, basándose en todo el contexto, actualizar `## Deudas Abiertas` de la sesión.
5. **Actualizar `MaC/README.md`** según [`procesos/readme-MaC.md`](procesos/readme-MaC.md)

> **Tono**: Compacto pero con el desarrollo suficiente para extrapolar ideas sin dificultad.
