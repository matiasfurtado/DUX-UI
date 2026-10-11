# Coffea — Landing page (TP4)

Landing page estática de una sola página para la cafetería ficticia **Coffea**, construida solo con **HTML5 semántico y CSS3**. Sin JavaScript, frameworks, Tailwind, Sass, bundlers, CMS ni backend.

## Estructura

```
coffea-landing/
├── index.html            # landing de 9 secciones
├── 404.html              # página de error (mismo header y footer)
├── netlify.toml          # publicación, headers de seguridad y caché
├── css/
│   ├── main.css          # declara las capas y hace @import en orden
│   ├── tokens.css        # custom properties (colores, tipografías, radios, espaciados)
│   ├── base.css          # reset, tipografía base, :focus-visible, skip link, reduced motion
│   ├── layout.css        # .container, títulos de sección, franjas
│   ├── components/       # header, hero, categories, product-card, carousel, promo,
│   │                     # testimonial-card, newsletter, footer
│   └── utilities.css     # .visually-hidden / .sr-only
└── assets/
    ├── img/              # AVIF + WebP + JPG de fallback
    └── icons/            # SVG (categorías, búsqueda, corazón, flecha, chevron, estrella, sobre, redes)
```

Capas de la cascada: `tokens → base → layout → components → utilities`. Clases con metodología BEM. Mobile-first con breakpoints en 768, 1024 y 1440 px.

## Cómo abrirlo en local

Opción simple: abrir `index.html` en el navegador. Recomendado, para que el logo (`href="/"`) y la 404 funcionen igual que en producción:

```bash
cd coffea-landing
python3 -m http.server 8080   # y abrir http://localhost:8080
```

## Cómo comprobarlo

- Validadores: https://validator.w3.org (HTML) y https://jigsaw.w3.org/css-validator (CSS).
- Lighthouse (Chrome DevTools) sobre la **URL de producción** de Netlify (RNF-D7).
- Responsive: DevTools de 360 a 1920 px, verificando que no haya scroll horizontal de página.
- Teclado: Tab recorre skip link, navegación, botones, favoritos, carruseles y formulario con foco visible.

## Cómo publicarlo en Netlify

1. Subir el proyecto a un repositorio de GitHub o GitLab (rama `main`).
2. En Netlify: *Add new site → Import an existing project* y elegir el repositorio.
3. Build command: vacío. Publish directory: `.` (ya está en `netlify.toml`).
4. Activar *Deploy Previews* para Pull/Merge Requests. HTTPS es automático.

Como `css/` y `assets/` tienen caché `immutable`, si se modifica un archivo hay que renombrarlo con versión (por ejemplo `main.v2.css`) y actualizar la referencia.

## Notas importantes

- **Imágenes:** no se tuvo acceso al Figma, así que las 15 imágenes son **ilustraciones de reemplazo generadas** con las medidas y nombres del PRD. Hay que sustituirlas por las exportadas del Figma (o imágenes propias con licencia) manteniendo los nombres de `assets/img/`.
- **Hero:** el PRD indica `hero.avif`; se sirve AVIF + WebP + JPG con `<picture>`.
- **Textos placeholder** (no definidos en el PRD): párrafo del hero, descripciones y nombres de postres, subtítulo del newsletter, enlaces del footer, texto del botón del CTA ("Shop now") y testimonios (lorem ipsum, "James Smith"). Los precios mantienen "Rs. 200" del diseño (pendiente confirmar moneda). Typos del Figma corregidos: "Join in and get 15% off!", "Explore Our Products", "Our story", "Plans & pricing", "Sell your products", "INFORMATION".
- **Idioma:** `lang="en"` (copy en inglés, como el diseño); confirmar idioma final.
- **Carruseles:** con 4 cards por carrusel, desde 1024 px se ven todas. Las flechas (anclas a la primera/última card) solo aparecen desde 1800 px, donde caben fuera del carrusel sin generar scroll horizontal. En mobile/tablet se desliza con swipe y scroll-snap.
- **Paginador de testimonios:** anclas a `#t-1`, `#t-2`, `#t-3`.
- **Funcionalidad simulada:** "Order Now", Login, redes y buscador no hacen nada real; el newsletter usa `action="#"` con validación nativa y no envía datos.
- **Fuentes:** se cargan desde Google Fonts (con `preconnect` y `display=swap`). Autohospedarlas queda como mejora.
- **Open Graph:** sin `og:image` porque requiere una URL absoluta (agregarla tras el deploy).
