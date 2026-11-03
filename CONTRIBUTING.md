# Guía de colaboración — Maison Vérane

Prototipo e-commerce en **HTML + Tailwind CSS únicamente** (sin JavaScript ni otros frameworks).

## Reparto de vistas

| Vista | Archivo | Rama |
|-------|---------|------|
| Home | `index.html` | `feature/home` |
| Catálogo | `catalogo.html` | `feature/catalogo` |
| Producto | `producto/<nombre>.html` (una ficha por producto) | `feature/producto` |
| Carrito | `carrito.html` | `feature/carrito` |
| Checkout | `checkout.html` | `feature/checkout` |

El navbar ya enlaza a `catalogo.html`, `carrito.html` y el footer a `catalogo.html?categoria=…`. Los archivos de cada vista los crea quien la desarrolla.

## Cómo empezar una vista

1. `git checkout main && git pull origin main`
2. `git checkout -b feature/<vista>`
3. Copia `components/page-template.html` al archivo de tu vista.
4. Pega `components/navbar.html` y `components/footer.html` donde indican los comentarios, **sin modificarlos**. Si tu página está dentro de `producto/`, usa en su lugar `components/navbar-producto.html` y `components/footer-producto.html`: son idénticos, pero con los enlaces en `../` para que no den 404 desde la subcarpeta. Si hace falta un cambio, abre un PR contra `main` con la rama `feature/base-<cambio>` y regenera las variantes.
5. Prueba en local: `python3 -m http.server 8000` y abre `http://localhost:8000/index.html`.

## Sistema de diseño

| Token | Valor Tailwind |
|-------|----------------|
| Fondo página | `bg-stone-50` |
| Texto | `text-stone-900` (secundario `text-stone-600`) |
| Acento | `orange-800` (hover/focus) |
| Titulares | `font-serif font-semibold` |
| Cuerpo | `font-sans` |
| Contenedor | `mx-auto max-w-7xl px-4 sm:px-6 lg:px-8` |
| Botón primario | `rounded-full bg-stone-900 px-6 py-3 text-sm font-medium text-white hover:bg-orange-800` |
| Card de producto | `<article>` con imagen `aspect-[3/4] object-cover`, nombre, precio en `€` |

Breakpoints: móvil por defecto, `md:` tablet, `lg:` escritorio. Sin scroll horizontal de página en móvil.

## HTML y SEO

- Un solo `<h1>` por página; jerarquía de `<h2>`/`<h3>` sin saltos.
- Landmarks: `<header>`, `<nav>`, un `<main id="contenido">`, `<footer>`.
- `<title>` y `meta description` únicos; `alt` descriptivo en imágenes; `width`/`height` en `<img>`; `loading="lazy"` salvo la imagen principal.
- Tailwind: usa el `<script>` de `components/page-template.html` (versión fija con `integrity`); no lo cambies a `@4`.
- Schema.org en JSON-LD donde aplique (`Product` en producto, `ItemList` en listados).

## Git

- Nunca commits directos a `main`. Una rama por vista o funcionalidad.
- `git pull origin main` antes de abrir el PR. Sin `push --force`; los conflictos se resuelven en equipo.
- Commits pequeños, un cambio lógico por commit, en [Conventional Commits](https://www.conventionalcommits.org/): `feat(carrito): add order summary box`.
- Cada PR describe qué incluye y cómo probarlo.

## Si tu rama se queda atrás

Cuando otra persona mergea su PR, `main` avanza y tu rama queda desactualizada. GitHub lo avisa en tu PR con "This branch is out-of-date".

1. En tu PR, pulsa **Update branch**. GitHub trae los cambios de `main` a tu rama con un commit de unión; no reescribe tu trabajo.
2. En tu ordenador, antes de seguir trabajando: `git checkout <tu-rama>` y `git pull`.
   Si prefieres no usar el botón, desde la terminal: `git checkout <tu-rama>`, `git pull origin main` y `git push`.
3. Si `git push` responde "rejected" o "non-fast-forward", haz `git pull` y vuelve a hacer `git push`. No uses `--force`.
4. Si `git pull` muestra `CONFLICT`, no borres nada: avisa al equipo y se resuelve entre todos.
