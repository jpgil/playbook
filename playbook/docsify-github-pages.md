# Publicar `/docs/` como sitio Docsify en GitHub Pages

> **Para humanos y agentes IA.**  
> Este documento describe el estado objetivo del repositorio para publicar la carpeta `/docs/` como un sitio de documentación navegable usando Docsify, sin proceso de build, con publicación automática en cada `git push`.

---

## Estado objetivo

Cuando este setup está completo, el repositorio debe tener:

```
/docs/
  index.html        ← motor Docsify (único archivo de infraestructura)
  _sidebar.md       ← navegación lateral (editable como cualquier MD)
  README.md         ← portada del sitio (homepage)
  *.md              ← contenido, sin modificar
  historias/        ← subdirectorios con contenido adicional
```

Y en GitHub → Settings → Pages:
- **Source**: `Deploy from a branch`
- **Branch**: `main` / **Folder**: `/docs`

Resultado: cada `git push` publica en `https://<org>.github.io/<repo>` en ~30 segundos. Sin Actions, sin build, sin dependencias locales.

---

## Verificación: checklist para agentes IA

Un agente puede verificar si el repo está correctamente configurado comprobando:

- [ ] Existe `docs/index.html` con `window.$docsify` definido
- [ ] Existe `docs/_sidebar.md` con al menos una entrada
- [ ] Existe `docs/README.md` como portada del sitio
- [ ] Existe `docs/.nojekyll` (vacío) para evitar que Jekyll ignore `_sidebar.md`
- [ ] `docs/index.html` carga docsify-themeable CSS **y** JS desde CDN
- [ ] Los archivos `.md` referenciados en `_sidebar.md` existen en las rutas indicadas
- [ ] Todo el contenido que debe verse en la web está **dentro** de `/docs/` (no fuera)
- [ ] `basePath` está configurado si el sitio vive en un subpath (ej. `/mac/`)
- [ ] GitHub Pages está configurado en el branch y carpeta correctos

---

## Archivo 1: `docs/index.html`

Este es el único archivo que no es Markdown. Contiene el motor Docsify y el CSS personalizado.

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>MaC — Management as Code</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <!-- FUENTES: cambiar aquí para personalizar tipografía -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">

  <!-- TEMA BASE: docsify-themeable (las variables CSS lo personalizan) -->
  <!-- ⚠️ SIN ESTE CSS EL SITIO SE VE COMO HTML CRUDO -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/css/theme-simple-dark.css">

  <style>
    /* ============================================================
       VARIABLES DE TEMA — editar esta sección para personalizar
       Docsify-themeable expone estas variables CSS.
       Referencia completa: https://jhildenbiddle.github.io/docsify-themeable
    ============================================================ */
    :root {
      /* Tipografía */
      --base-font-family: 'Inter', -apple-system, sans-serif;
      --base-font-size: 16px;
      --base-line-height: 1.75;

      /* Colores base */
      --base-color: #d4d4d4;               /* texto principal */
      --base-background-color: #0f0f0f;    /* fondo de contenido */
      --heading-color: #f0f0f0;            /* títulos */
      --heading-font-weight: 500;

      /* Links */
      --link-color: #a78bfa;               /* color de acento — cambiar aquí */
      --link-color--hover: #c4b5fd;
      --link-text-decoration: none;

      /* Sidebar */
      --sidebar-background: #141414;
      --sidebar-border-color: #262626;
      --sidebar-width: 260px;
      --sidebar-color: #a3a3a3;
      --sidebar-name-color: #f0f0f0;
      --sidebar-nav-link-color: #a3a3a3;
      --sidebar-nav-link-color--active: #f0f0f0;
      --sidebar-nav-link-font-weight--active: 500;
      --sidebar-nav-link-border-color--active: #a78bfa; /* acento activo */

      /* Código */
      --code-font-family: 'JetBrains Mono', 'Fira Code', monospace;
      --code-background: #1a1a1a;
      --code-color: #c4b5fd;
      --code-block-border-radius: 6px;

      /* Blockquotes */
      --blockquote-border-color: #a78bfa;
      --blockquote-color: #a3a3a3;

      /* Tablas */
      --table-row-odd-background: #1a1a1a;
      --table-row-even-background: #141414;

      /* Búsqueda */
      --search-input-background-color: #1a1a1a;
      --search-input-border-color: #333;
      --search-input-color: #d4d4d4;

      /* Separadores */
      --hr-border: 1px solid #262626;
    }

    /* ============================================================
       CSS ADICIONAL — ajustes fuera del sistema de variables
    ============================================================ */
    body {
      font-feature-settings: 'kern', 'liga';
    }

    .app-name-link {
      font-weight: 600;
      letter-spacing: 0.02em;
    }

    h1, h2, h3 {
      letter-spacing: -0.01em;
    }

    /* Responsive */
    @media (max-width: 768px) {
      :root {
        --base-font-size: 15px;
        --sidebar-width: 240px;
      }
    }
  </style>
</head>
<body>
  <div id="app"></div>

  <script>
    /* ============================================================
       CONFIGURACIÓN DOCSIFY — opciones principales
       Referencia: https://docsify.js.org/#/configuration
    ============================================================ */
    window.$docsify = {
      name: 'MaC',                              // nombre en sidebar
      nameLink: '/mac/#/',                       // ⚠️ debe incluir el subpath
      repo: 'https://github.com/pewma-ai/mac',  // ícono GitHub arriba derecha
      basePath: '/mac/',                         // ⚠️ necesario en subpaths de GitHub Pages
      loadSidebar: true,                         // usa _sidebar.md
      subMaxLevel: 2,                            // niveles de TOC en sidebar
      homepage: 'README.md',                     // página de entrada (portada)
      themeColor: '#a78bfa',                     // color de acento (progress bar)
      notFoundPage: true,                        // página 404 automática
      auto2top: true,                            // scroll al inicio al cambiar de página
      search: {
        placeholder: 'Buscar...',
        noData: 'Sin resultados.',
      },
      pagination: {
        previousText: 'Anterior',
        nextText: 'Siguiente',
        crossChapter: true,
        crossChapterText: true,
      },
      mermaid: {
        theme: 'dark',                           // tema para diagramas Mermaid
      },
    }
  </script>

  <!-- ==========================================
       PLUGINS QUE DEBEN IR ANTES DE DOCSIFY
       ========================================== -->
  <!-- Mermaid: docsify-mermaid ANTES de docsify.min.js y docsify-themeable -->
  <script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
  <script>mermaid.initialize({ startOnLoad: false });</script>
  <script src="https://cdn.jsdelivr.net/npm/docsify-mermaid@2/dist/docsify-mermaid.min.js"></script>

  <!-- ==========================================
       MOTOR CORE DOCSIFY
       ========================================== -->
  <!-- Motor de temas (debe ir ANTES de docsify.min.js) -->
  <script src="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/js/docsify-themeable.min.js"></script>
  <!-- Motor Docsify -->
  <script src="https://cdn.jsdelivr.net/npm/docsify@4/lib/docsify.min.js"></script>
  <!-- Plugin de búsqueda -->
  <script src="https://cdn.jsdelivr.net/npm/docsify@4/lib/plugins/search.min.js"></script>

  <!-- Plugins adicionales -->
  <script src="https://cdn.jsdelivr.net/npm/docsify/lib/plugins/zoom-image.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/docsify-copy-code@2/dist/docsify-copy-code.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/docsify-pagination/dist/docsify-pagination.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/docsify-tabs@1/dist/docsify-tabs.min.js"></script>
</body>
</html>
```

---

## Archivo 2: `docs/_sidebar.md`

Define la navegación lateral. Se edita como cualquier Markdown.

```markdown
* [Inicio](/)

* **Documentos**
  * [Para impacientes](mac-para-impacientes.md)
  * [Implementación](implementacion-mac.md)
  * [Método MaC](metodo-mac.md)
  * [Procesos](procesos-mac.md)
  * [Preguntas](preguntas-mac.md)

* **Historias**
  * [Javiera](historias/javiera%20-%20relato%20de%20un%20independiente.md)
  * [Nexo](historias/nexo%20-%20relato%20de%202%20a%2010%20personas.md)
  * [NovaTech](historias/novatech%20-%20relato%20empresa%20mediana.md)
```

> **Nota sobre espacios en nombres de archivo:** Docsify puede fallar con espacios en rutas. Usar `%20` en el `_sidebar.md` es más seguro, aunque los archivos físicos mantengan sus nombres originales.

---

## Configurar GitHub Pages (una sola vez)

1. Ir a **Settings** del repositorio
2. Sección **Pages** en el menú lateral
3. En **Source** seleccionar: `Deploy from a branch`
4. **Branch**: `main` / **Folder**: `/docs`
5. Click en **Save**

Desde ese momento, cada `git push` a `main` publica automáticamente. No se requiere ningún workflow de GitHub Actions.

La URL resultante será: `https://pewma-ai.github.io/mac`

---

## Flujo completo

```
Obsidian / Editor
   ↓ edita *.md en /docs/
git push origin main
   ↓ ~30 segundos
GitHub Pages sirve /docs/ como sitio Docsify
   ↓ disponible en
pewma-ai.github.io/mac
```

Docsify es una capa de lectura sobre los archivos originales. No los modifica ni compila. El repositorio sigue siendo la fuente de verdad.

---

## Lecciones aprendidas (sesión 2026-03-14)

### ⚠️ Sin el CSS de tema, el sitio se ve roto

Docsify-themeable requiere **dos** cosas:
1. El `<link>` al CSS del tema (ej. `theme-simple-dark.css`) — **sin esto, el sitio es HTML crudo**.
2. El `<script>` del JS de docsify-themeable — procesa las variables CSS personalizadas.

### ⚠️ Subpath en GitHub Pages rompe sidebar y logo

Si el sitio vive en `org.github.io/<repo>/` (no en la raíz), se necesitan **dos** config:
- `basePath: '/<repo>/'` — para que Docsify encuentre `_sidebar.md` y los `.md`.
- `nameLink: '/<repo>/#/'` — para que el logo del sidebar lleve a la portada, no a `org.github.io/`.

### ⚠️ Jekyll ignora archivos con guión bajo (`_sidebar.md`)

Por defecto, GitHub Pages corre Jekyll, el cual ignora automáticamente cualquier archivo o carpeta que empiece con `_`. Si no se desactiva, el `_sidebar.md` nunca se publica y Docsify muestra un sidebar vacío. 
**Solución**: crear un archivo vacío llamado `.nojekyll` dentro de `/docs/`.

### ⚠️ Todo el contenido debe vivir dentro de `/docs/`

GitHub Pages solo sirve archivos desde la carpeta configurada. Archivos fuera de `/docs/` (como estaba `historias/`) no se cargan aunque Docsify intente usar rutas relativas con `../`. La solución fue mover `historias/` a `docs/historias/`.

### Mermaid requiere orden específico de scripts

Orden obligatorio contrario a lo intuitivo: `mermaid` inicializado con `startOnLoad: false`, luego `docsify-mermaid`, y todo esto **antes** de cargar el core de `docsify.min.js`. Si se hace al revés, Docsify inicializa antes que el plugin y bloquea el renderizado.

### Docsify mantiene el scroll entre páginas

Por defecto, al hacer click en un enlace de otra página, Docsify la carga pero se queda en la misma posición de scroll en la que estabas. **Solución**: agregar `auto2top: true` en el config `window.$docsify` para forzar que empiece desde arriba.

---

## Personalización CSS: guía de referencia

### Cambiar color de acento

Buscar y reemplazar las tres ocurrencias de `#a78bfa` en `index.html`:

```css
--link-color: #TU_COLOR;
--sidebar-nav-link-border-color--active: #TU_COLOR;
--blockquote-border-color: #TU_COLOR;
```

Y en la configuración JS:

```js
themeColor: '#TU_COLOR',
```

### Cambiar a tema claro

Cambiar el `<link>` de CSS a `theme-simple.css` (sin el `-dark`) y reemplazar las variables de color base:

```css
:root {
  --base-color: #1a1a1a;
  --base-background-color: #ffffff;
  --heading-color: #111111;
  --sidebar-background: #f5f5f5;
  --sidebar-border-color: #e5e5e5;
  --sidebar-color: #555555;
  --code-background: #f0f0f0;
  --table-row-odd-background: #f9f9f9;
  --table-row-even-background: #ffffff;
}
```

### Cambiar tipografía

Reemplazar el `<link>` de Google Fonts y la variable:

```html
<!-- Ejemplo con otra fuente -->
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
```

```css
--base-font-family: 'DM Sans', sans-serif;
```

### Variables completas disponibles

Referencia oficial de todas las variables del sistema de temas:  
`https://jhildenbiddle.github.io/docsify-themeable/#/customization`

---

## Plugins adicionales disponibles

Agregar después de los scripts existentes según necesidad:

```html
<!-- Emojis -->
<script src="https://cdn.jsdelivr.net/npm/docsify/lib/plugins/emoji.min.js"></script>

<!-- Resaltado de sintaxis para más lenguajes -->
<script src="https://cdn.jsdelivr.net/npm/prismjs@1/components/prism-python.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/prismjs@1/components/prism-bash.min.js"></script>
```

---

## Limitaciones conocidas

- **SEO**: Docsify renderiza en el browser (JS requerido). Google indexa eventualmente, pero de forma lenta. No usar si el posicionamiento en buscadores es prioritario.
- **Sin JS**: el sitio no funciona sin JavaScript habilitado.
- **Espacios en rutas**: los nombres de archivo con espacios requieren `%20` en los links del `_sidebar.md`.
- **Archivos fuera de `/docs/`**: GitHub Pages **no los sirve**. Todo contenido que deba verse en la web debe vivir dentro de `/docs/`.

---

## Recursos

- Docsify: https://docsify.js.org
- Docsify-themeable: https://jhildenbiddle.github.io/docsify-themeable
- Docsify-mermaid: https://github.com/Leward/mermaid-docsify
