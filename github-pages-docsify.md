---
title: Publicar docs con Docsify en GitHub Pages
description: Publicar /docs/ como sitio navegable usando Docsify en GitHub Pages, sin procesos de compilación.
date: 2026-03-15
source: https://github.com/jpgil/playbook/blob/main/github-pages-docsify.md
---

# Publicar `/docs/` como sitio Docsify en GitHub Pages

---

## El problema

Publicar documentación suele requerir pipelines de CI/CD, generadores estáticos con build steps, y configuraciones complejas. Docsify elimina esa fricción: renderiza Markdown directamente en el browser, sin compilar nada.

---

## Estado objetivo

Cuando el setup está completo, el repositorio debe tener:

```
/docs/
  index.html        ← motor Docsify (único archivo de infraestructura)
  _sidebar.md       ← navegación lateral (editable como cualquier MD)
  README.md         ← portada del sitio (homepage)
  .nojekyll         ← archivo vacío (evita que Jekyll ignore _sidebar.md)
  *.md              ← contenido, sin modificar
```

Y en GitHub → Settings → Pages:
- **Source**: `Deploy from a branch`
- **Branch**: `main` / **Folder**: `/docs`

Resultado: cada `git push` publica en `https://<org>.github.io/<repo>` en ~30 segundos. Sin Actions, sin build, sin dependencias locales.

---

## Checklist de verificación

Un agente puede verificar si el repo está correctamente configurado comprobando:

- [ ] Existe `docs/index.html` con `window.$docsify` definido
- [ ] Existe `docs/_sidebar.md` con al menos una entrada
- [ ] Existe `docs/README.md` como portada del sitio
- [ ] Existe `docs/.nojekyll` (vacío)
- [ ] `docs/index.html` carga docsify-themeable CSS **y** JS desde CDN
- [ ] Los archivos `.md` referenciados en `_sidebar.md` existen en las rutas indicadas
- [ ] Todo el contenido visible en la web está **dentro** de `/docs/`
- [ ] `basePath` está configurado si el sitio vive en un subpath (ej. `/mi-repo/`)
- [ ] GitHub Pages está configurado en el branch y carpeta correctos

---

## Archivo 1: `docs/index.html`

Este es el único archivo que no es Markdown. Contiene el motor Docsify y el CSS personalizado.

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Mi Documentación</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <!-- FUENTES: cambiar aquí para personalizar tipografía -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">

  <!-- TEMA BASE: docsify-themeable -->
  <!-- ⚠️ SIN ESTE CSS EL SITIO SE VE COMO HTML CRUDO -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/css/theme-simple-dark.css">

  <style>
    :root {
      /* Tipografía */
      --base-font-family: 'Inter', -apple-system, sans-serif;
      --base-font-size: 16px;
      --base-line-height: 1.75;

      /* Colores base */
      --base-color: #d4d4d4;
      --base-background-color: #0f0f0f;
      --heading-color: #f0f0f0;

      /* Links — cambiar color de acento aquí */
      --link-color: #a78bfa;
      --link-color--hover: #c4b5fd;
      --link-text-decoration: none;

      /* Sidebar */
      --sidebar-background: #141414;
      --sidebar-border-color: #262626;
      --sidebar-width: 260px;
      --sidebar-nav-link-color--active: #f0f0f0;
      --sidebar-nav-link-border-color--active: #a78bfa;

      /* Código */
      --code-font-family: 'JetBrains Mono', 'Fira Code', monospace;
      --code-background: #1a1a1a;
      --code-color: #c4b5fd;
      --code-block-border-radius: 6px;

      /* Blockquotes */
      --blockquote-border-color: #a78bfa;
    }
  </style>
</head>
<body>
  <div id="app"></div>

  <script>
    window.$docsify = {
      name: 'Mi Proyecto',                        // nombre en sidebar
      // nameLink: '/mi-repo/#/',                  // ⚠️ descomentar si hay subpath
      repo: 'https://github.com/user/repo',       // ícono GitHub
      // basePath: '/mi-repo/',                    // ⚠️ descomentar si hay subpath
      loadSidebar: true,
      subMaxLevel: 2,
      homepage: 'README.md',
      themeColor: '#a78bfa',
      notFoundPage: true,
      auto2top: true,
      search: {
        placeholder: 'Buscar...',
        noData: 'Sin resultados.',
      },
    }
  </script>

  <!-- Mermaid: ANTES de docsify -->
  <script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
  <script>mermaid.initialize({ startOnLoad: false });</script>
  <script src="https://cdn.jsdelivr.net/npm/docsify-mermaid@2/dist/docsify-mermaid.min.js"></script>

  <!-- Motor Docsify -->
  <script src="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/js/docsify-themeable.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/docsify@4/lib/docsify.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/docsify@4/lib/plugins/search.min.js"></script>

  <!-- Plugins adicionales -->
  <script src="https://cdn.jsdelivr.net/npm/docsify/lib/plugins/zoom-image.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/docsify-copy-code@2/dist/docsify-copy-code.min.js"></script>
</body>
</html>
```

---

## Archivo 2: `docs/_sidebar.md`

Define la navegación lateral. Se edita como cualquier Markdown.

```markdown
* [Inicio](/)

* **Sección 1**
  * [Página A](pagina-a.md)
  * [Página B](pagina-b.md)

* **Sección 2**
  * [Página C](pagina-c.md)
```

> **Nota sobre espacios en nombres de archivo:** Docsify puede fallar con espacios en rutas. Usar `%20` en el `_sidebar.md` es más seguro.

---

## Configurar GitHub Pages (una sola vez)

1. Ir a **Settings** del repositorio.
2. Sección **Pages** en el menú lateral.
3. En **Source** seleccionar: `Deploy from a branch`.
4. **Branch**: `main` / **Folder**: `/docs`.
5. Click en **Save**.

Desde ese momento, cada `git push` a `main` publica automáticamente. No se requiere ningún workflow de GitHub Actions.

---

## Flujo completo

```
Editor / Obsidian
   ↓ edita *.md en /docs/
git push origin main
   ↓ ~30 segundos
GitHub Pages sirve /docs/ como sitio Docsify
   ↓ disponible en
<user>.github.io/<repo>
```

Docsify es una capa de lectura sobre los archivos originales. No los modifica ni compila. El repositorio sigue siendo la fuente de verdad.

---

## Lecciones aprendidas

### ⚠️ Sin el CSS de tema, el sitio se ve roto

Docsify-themeable requiere **dos** cosas:
1. El `<link>` al CSS del tema (ej. `theme-simple-dark.css`) — **sin esto, el sitio es HTML crudo**.
2. El `<script>` del JS de docsify-themeable — procesa las variables CSS personalizadas.

### ⚠️ Subpath en GitHub Pages rompe sidebar y logo

Si el sitio vive en `user.github.io/<repo>/` (no en la raíz), se necesitan **dos** configs:
- `basePath: '/<repo>/'` — para que Docsify encuentre `_sidebar.md` y los `.md`.
- `nameLink: '/<repo>/#/'` — para que el logo del sidebar lleve a la portada.

### ⚠️ Jekyll ignora archivos con guión bajo (`_sidebar.md`)

GitHub Pages corre Jekyll por defecto, que ignora archivos que empiezan con `_`.
**Solución**: crear un archivo vacío `.nojekyll` dentro de `/docs/`.

### ⚠️ Todo el contenido debe vivir dentro de `/docs/`

GitHub Pages solo sirve archivos desde la carpeta configurada. Archivos fuera de `/docs/` no se cargan aunque Docsify intente usar rutas relativas con `../`.

### Mermaid requiere orden específico de scripts

Orden obligatorio: `mermaid.js` → `docsify-mermaid.js` → `docsify-themeable.js` → `docsify.min.js`. Si se invierte, los diagramas no renderizan.

### Docsify mantiene el scroll entre páginas

Por defecto, al navegar entre páginas Docsify conserva la posición de scroll.
**Solución**: agregar `auto2top: true` en el config.

---

## Personalización CSS rápida

### Cambiar color de acento

Buscar y reemplazar `#a78bfa` en las variables CSS y en `themeColor`:

```css
--link-color: #TU_COLOR;
--sidebar-nav-link-border-color--active: #TU_COLOR;
--blockquote-border-color: #TU_COLOR;
```

### Cambiar a tema claro

Cambiar el `<link>` a `theme-simple.css` (sin `-dark`) y ajustar las variables de color.

### Cambiar tipografía

Reemplazar el `<link>` de Google Fonts y la variable `--base-font-family`.

---

## Fronteras

| Nivel | Regla |
|---|---|
| **Hacer siempre** | Verificar la checklist antes de hacer push de cambios en `/docs/`. |
| **Preguntar primero** | Antes de modificar `docs/index.html` (archivo de infraestructura). |
| **Nunca hacer** | Colocar contenido fuera de `/docs/` si se espera que sea visible en el sitio. |

---

## Recursos

- Docsify: https://docsify.js.org
- Docsify-themeable: https://jhildenbiddle.github.io/docsify-themeable
- Docsify-mermaid: https://github.com/Leward/mermaid-docsify
