# Proceso: Mantener MaC/README.md

> **Qué es este documento:** Instrucciones para que un agente IA mantenga `MaC/README.md` actualizado. Este archivo es el **panel de control** del proyecto: quien lo lea (humano o agente) debe saber en segundos qué está pasando y dónde ir.

---

## Estructura del README

El `MaC/README.md` tiene cuatro bloques, siempre en este orden:

### 1. Encabezado
```markdown
# MaC de <NOMBRE DEL PROYECTO>
*(Basado en Management as Code, https://pewma-ai.github.io/mac/)*
```
- `<NOMBRE DEL PROYECTO>` se toma del `README.md` raíz del repositorio.

### 2. Estado Actual (callouts)
Dos bloques de tipo callout, inmediatamente después del encabezado:

```markdown
>[!Ultima sesión]
>[sesion-YYYY-MM-DD.md](sesiones/sesion-YYYY-MM-DD.md) (Estado)

>[!Deudas Abiertas]
>Resumen breve de deudas, o "Nada pendiente por ahora"
```

**Reglas:**
- **Última sesión**: Apuntar siempre a la sesión más reciente. Estado puede ser `Abierta` o `Cerrada`.
- **Deudas Abiertas**: Copiar las deudas de la sección `Deudas abiertas` de la última introspección de sesión cerrada. Si no hay deudas, escribir "Nada pendiente por ahora".

### 3. Contenidos MaC/
Listado plano de archivos con su rol MaC entre paréntesis:

```markdown
## Contenidos MaC/

- [`MaC/`](README.md): Qué hacer a continuación
- [`../README.md`](../README.md): **Identidad** (Propósito de este repositorio).
- [`roadmap.md`](roadmap.md): **Dirección** (Metas e hitos).
- [`../AGENTS.md`](../AGENTS.md): **Capacidad** (Reglas y límites IA).
- [`sesiones/sesion-*.md`](sesiones/): **Planificación, Tareas y Resultados**, Decisiones (Ciclo táctico por sesión).
- [`sesiones/sesion-TEMPLATE.md`](sesiones/sesion-TEMPLATE.md): **Molde** para nuevas sesiones.
- [`log.md`](log.md): **Decisiones** (Registro histórico y hechos consumados).
- [`ritual_de_sesion.md`](ritual_de_sesion.md): **Políticas de Gestión** (Cómo administramos).
- [`procesos/`](procesos/): **Procesos MaC** (Skills de agente que formalizan procesos recurrentes).
- [Playbook](../playbook/README.md): **Políticas Operativas** (Cómo ejecutamos).
```

**Reglas:**
- Este bloque es **estático** a menos que se agreguen o eliminen archivos del directorio `MaC/`.
- Si se agrega un nuevo archivo, clasificarlo en la capa MaC correspondiente (Estrategia, Acción o Aprendizaje) y añadirlo con el formato `[nombre](ruta): **Subcapa** (descripción corta)`.
- Si se elimina un archivo, remover la línea correspondiente.

### 4. Sesiones Anteriores
```markdown
---
### Sesiones Anteriores
- [sesion-YYYY-MM-DD.md](sesiones/sesion-YYYY-MM-DD.md)
- ...
```

**Reglas:**
- Mantener las **últimas tres** sesiones cerradas, de más reciente a más antigua.
- Si no hay sesiones anteriores, escribir `- N/A`.

---

## Cuándo actualizar

| Evento | Qué hacer |
|---|---|
| **Inicio de sesión** | Actualizar callout `Ultima sesión` → nueva sesión `(Abierta)`. |
| **Cierre de sesión** | Cambiar estado a `(Cerrada)`. Actualizar `Deudas Abiertas` con las deudas de la introspección. Rotar `Sesiones Anteriores` (máximo 3). |
| **Nuevo archivo en MaC/** | Agregar línea en `Contenidos MaC/` con su clasificación. |
| **Archivo eliminado de MaC/** | Remover la línea correspondiente de `Contenidos MaC/`. |

---

## Principio rector
**Brevedad y precisión.** Este archivo se lee de un vistazo. No agregar prosa, explicaciones largas ni secciones adicionales.
