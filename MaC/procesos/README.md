# Procesos MaC

> **Audiencia:** Agente IA y humanos. Este archivo es el índice de todos los procesos formalizados. El agente lo consulta cuando necesita saber si existe un proceso para una solicitud específica.

## Índice de procesos

| Proceso | Archivo | Trigger | Descripción |
|---|---|---|---|
| **Amigo MaC** | [amigo-MaC.md](amigo-MaC.md) | Inicio de sesión/conversación | Modos de operación del agente principal. Punto de entrada obligatorio. |
| **Ritual de Sesión** | [ritual_de_sesion.md](../ritual_de_sesion.md) | Usuario pide abrir o cerrar sesión | Flujo completo de inicio (§1) y cierre (§4) de sesión. |
| **Mantener README MaC** | [readme-MaC.md](readme-MaC.md) | Inicio/cierre de sesión, nuevo/eliminado archivo en MaC/ | Reglas para mantener `MaC/README.md` actualizado. |

## Regla de mantenimiento

Cada vez que se cree un nuevo proceso en este directorio, **agregar una fila a la tabla anterior** con su nombre, archivo, trigger y descripción breve.
