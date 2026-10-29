# Guía de colaboración — Maison Vérane

Prototipo e-commerce en **HTML + Tailwind CSS únicamente** (sin JavaScript ni otros frameworks).

## Reparto de vistas

| Vista | Archivo | Rama |
|-------|---------|------|
| Home | `index.html` | `feature/home` |
| Catálogo | `catalogo.html` | `feature/catalogo` |
| Producto | `producto.html` | `feature/producto` |
| Carrito | `carrito.html` | `feature/carrito` |
| Checkout | `checkout.html` | `feature/checkout` |

El navbar ya enlaza a `catalogo.html`, `carrito.html` y el footer a `catalogo.html?categoria=…`. Los archivos de cada vista los crea quien la desarrolla.

## Cómo empezar una vista

1. `git checkout main && git pull origin main`
2. `git checkout -b feature/<vista>`
3. Copia `components/page-template.html` al archivo de tu vista.
4. Pega `components/navbar.html` y `components/footer.html` donde indican los comentarios, **sin modificarlos**. Si hace falta un cambio, abre un PR contra `main` con la rama `feature/base-<cambio>`.
5. Prueba en local: `pip3 install flask && python3 server.py`.

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
- Schema.org en JSON-LD donde aplique (`Product` en producto, `ItemList` en listados).

## Git

- Nunca commits directos a `main`. Una rama por vista o funcionalidad.
- `git pull origin main` antes de abrir el PR. Sin `push --force`; los conflictos se resuelven en equipo.
- Commits pequeños, un cambio lógico por commit, en [Conventional Commits](https://www.conventionalcommits.org/): `feat(carrito): add order summary box`.
- Cada PR describe qué incluye y cómo probarlo.
