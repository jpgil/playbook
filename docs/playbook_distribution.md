# Estrategias de Distribución de Playbooks Personales

La regla 3 de nuestro manifiesto exige **Alta Portabilidad**. Un Playbook Personal debe poder acoplarse con la menor fricción posible a bases de código existentes, herramientas y estaciones de trabajo.

Aquí evaluamos las alternativas arquitectónicas para distribuir y utilizar un Playbook (`/playbook` y la carpeta de gobernanza `/MaC`) desde su repositorio de origen hacia otros proyectos.

## 1. El Ideal Técnico: Submódulos de Git (Git Submodules)
El método más robusto desde la perspectiva de la arquitectura de software. Un desarrollador incluye su repositorio "Playbook Maestro" como un submódulo de Git dentro de cualquier proyecto en el que trabaje.

- **Ventajas:**
  - Control de versiones preciso: El proyecto queda atado a una versión (commit) específica del playbook.
  - Aislamiento total: Los commits de actualización del playbook se separan limpiamente de los commits del proyecto huésped.
  - Actualización centralizada: Un comando (`git submodule update --remote`) baja la última filosofía operativa.
- **Desventajas:**
  - Fricción de usuario alta: Los submódulos son notoriamente complejos. Causan estados desincronizados y punteros rotos (dangling commits) si no se manejan con cuidado.
  - Exceso cognitivo: Obliga a desarrolladores no core a lidiar con estructuras de git anidadas.

## 2. El Atajo Local: Enlaces Simbólicos (Symlinks)
Una solución frecuente en la comunidad de "Dotfiles", donde se mantiene un único clon del playbook maestro en la máquina del desarrollador (ej. `~/.mia-playbook/`) y se crean enlaces simbólicos desde cada proyecto apuntando a esos archivos.

- **Ventajas:**
  - Cero fricciones de duplicación de datos: Una única fuente de verdad local.
  - Inmediatez: Cambias una regla y todos tus proyectos locales en tu máquina adoptan la nueva directiva al instante.
- **Desventajas:**
  - Fragilidad extrema en la colaboración: Al hacer *push* al repositorio compartido, los symlinks se rompen para cualquier otro desarrollador que clone el proyecto de trabajo (o intentan apuntar a directorios de sus propios discos duros que no existen).
  - Problemas multiplataforma: Ciertas herramientas de IA y sistemas operativos lidian mal con symlinks en entornos empaquetados (como Docker o WSL).

## 3. Dispersión por Plantilla (Clonado Directo / Template Repo)
El enfoque más pragmático. Distribuir el Playbook como un [Template Repository de GitHub] o simplemente copiar y pegar la carpeta `/playbook` y `/MaC` directamente en la raíz de cada nuevo proyecto.

- **Ventajas:**
  - Universalidad y simpleza: Funciona para cualquier proyecto, cualquier entorno y cualquier compañero de equipo. No requiere conocimiento especializado de Git.
  - Customización local: Si el proyecto requiere una desviación estricta (ej. modificar una regla del playbook porque el cliente actual lo prohíbe), esa modificación se queda solo en ese proyecto sin contaminar el Playbook Maestro original.
- **Desventajas:**
  - Deriva de configuración (Configuration Drift): Si el maestro desarrolla una nueva y grandiosa "Habilidad" de IA en su tiempo libre, tiene que copiar manualmente esa carpeta a todos los proyectos en paralelo si quiere el beneficio. No hay sincronización automática.

---

## 💡 Propuesta de Decisión
La fricción de los agentes de IA interactuando con **Submódulos** o leyendo a través de **Symlinks** puede ser impredecible, sumado a la frustración comunitaria habitual con esas herramientas. 

Si priorizamos democratizar el uso de este método (Iteración 1: "cómo compartirlo"), **la vía del Clonado / Plantilla (Opción 3) es la más segura y pragmática**, con los submódulos como opción "Avanzada" para ingenieros experimentados que asumen el riesgo de mantenimiento.

*¿Deseas adoptar la Opción 3 como el mecanismo estándar "por defecto" para la documentación oficial, o prefieres apostar por forzar el rigor del Submódulo?*
