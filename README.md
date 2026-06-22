# Luna Go - prototipo web documentado

Este paquete contiene la versión documentada del prototipo estático para la página web de Luna Go. La documentación está escrita directamente dentro de los archivos mediante comentarios HTML, CSS y JavaScript, y también en este README para explicar la función de cada archivo.

## Cómo abrir el proyecto

Abre `index.html` en un navegador. No necesita servidor, instalación ni dependencias externas porque es un prototipo estático construido con HTML, CSS y JavaScript puro.

## Estructura completa de archivos

```text
luna-go-web/
├── index.html
├── pintura.html
├── mural.html
├── ilustracion.html
├── sobre-mi.html
├── bitacora.html
├── tienda.html
├── README.md
├── assets/
│   ├── README.md
│   ├── luna-go-pintura-2026.jpg
│   ├── luna-go-mural-2026.jpg
│   ├── luna-go-ilustracion-2026.jpg
│   └── luna-go-pintura-detalle-2026.jpg
├── css/
│   └── styles.css
└── js/
    └── main.js
```

## Para qué sirve cada archivo

| Archivo | Función |
|---|---|
| `index.html` | Página principal. Contiene el header y el slider de obras destacadas con tipo de obra y año. |
| `pintura.html` | Página base para la galería de pintura, preparada para organizar obras por año. |
| `mural.html` | Página base para la galería de murales, preparada para organizar proyectos por año. |
| `ilustracion.html` | Página base para la galería de ilustración, preparada para organizar piezas por año. |
| `sobre-mi.html` | Página para biografía, statement, trayectoria y presentación de Luna Go. |
| `bitacora.html` | Página para textos, notas de proceso, diario de obra y publicaciones. |
| `tienda.html` | Página base para catálogo, prints, piezas disponibles, comisiones o productos. |
| `css/styles.css` | Controla colores, tipografía, layout, header, menú de años, slider, páginas interiores y responsive. |
| `js/main.js` | Controla interacciones: menú móvil, submenús de años, slider, autoplay, flechas, dots y teclado. |
| `assets/README.md` | Documenta las imágenes, su uso actual y cómo reemplazarlas. |
| `assets/*.jpg` | Imágenes usadas actualmente en el slider de portada. Son archivos binarios; por eso su documentación está en `assets/README.md`. |

## Paleta aplicada

Los cuatro colores principales están definidos como variables CSS al inicio de `css/styles.css`:

| Variable CSS | RGB | Uso principal |
|---|---:|---|
| `--malva` | `rgb(177, 146, 186)` | Acentos, dots activos, detalles del menú. |
| `--gris-lila` | `rgb(157, 162, 184)` | Bordes suaves y separadores. |
| `--azul-noche` | `rgb(38, 36, 72)` | Texto principal, fondos oscuros y overlays. |
| `--azul-acero` | `rgb(110, 132, 172)` | Matices secundarios y fondos suaves. |

Además existe `--paper`, un tono claro de fondo que sirve como base neutra para que la paleta respire.

## Dónde cambiar la tipografía

La tipografía está centralizada en `css/styles.css`, dentro de la variable:

```css
--font-sans: "Helvetica Neue", Arial, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
```

Cambiar esa línea modifica el logo textual, el menú y los títulos porque todos usan la misma familia sans-serif sencilla.

## Cómo cambiar las obras del slider

En `index.html`, cada obra del slider está dentro de un bloque con clase `slide` y atributo `data-slide`:

```html
<section class="slide" aria-label="Obra 5 de 5" data-slide>
  <img src="assets/nombre-de-la-imagen.jpg" alt="Descripción breve de la obra." draggable="false">
  <div class="slide-caption">
    <span class="work-type">Pintura</span>
    <span class="work-year">2026</span>
  </div>
</section>
```

Para agregar una obra:

1. Copia una imagen nueva dentro de `assets/`.
2. Duplica un bloque `<section class="slide" ...>` en `index.html`.
3. Cambia el `src`, el `alt`, el tipo de obra y el año.
4. Actualiza los textos `aria-label="Obra X de Y"` para que coincidan con el total real.
5. Agrega un botón dentro de `.slider-dots`.

Ejemplo de nuevo dot:

```html
<button class="dot" type="button" role="tab" aria-label="Mostrar obra 5" aria-selected="false" data-dot="4"></button>
```

Importante: `data-dot` empieza en cero. La obra 1 usa `data-dot="0"`, la obra 2 usa `data-dot="1"`, etc.

## Cómo cambiar los años del menú

Las pestañas `Pintura`, `Mural` e `Ilustración` tienen un panel llamado `.years-panel`. Cada año es un enlace:

```html
<a href="pintura.html#2026" role="menuitem">2026</a>
```

Para agregar 2027 en pintura, agrega:

```html
<a href="pintura.html#2027" role="menuitem">2027</a>
```

Como el prototipo es HTML estático, el header está repetido en todas las páginas. Si se cambia el menú, hay que copiar el mismo cambio en:

- `index.html`
- `pintura.html`
- `mural.html`
- `ilustracion.html`
- `sobre-mi.html`
- `bitacora.html`
- `tienda.html`

## Atributos `data-*` usados por JavaScript

| Atributo | Dónde está | Para qué sirve |
|---|---|---|
| `data-menu-toggle` | Botón hamburguesa | Permite abrir/cerrar el menú móvil. |
| `data-site-nav` | `<nav>` principal | Identifica el menú que se abre/cierra en móvil. |
| `data-years-menu` | Pestañas con años | Permite abrir/cerrar submenús con click. |
| `data-slider` | `<main>` de portada | Identifica el slider principal. |
| `data-slide` | Cada slide | Permite que JS sepa qué elementos son obras del slider. |
| `data-prev` | Botón anterior | Retrocede al slide anterior. |
| `data-next` | Botón siguiente | Avanza al slide siguiente. |
| `data-current` | Contador | Muestra el número de slide activo. |
| `data-total` | Contador | Muestra el total de slides. |
| `data-dot` | Dots del slider | Salta al slide con el índice indicado. |

No conviene borrar estos atributos si se quiere conservar la interactividad.

## Qué está documentado dentro de cada archivo

- Los `.html` tienen comentarios sobre el propósito de cada página, el header, el menú, los submenús de años, el contenido principal y, en el caso de `index.html`, cada parte del slider.
- `css/styles.css` está dividido por secciones comentadas: variables, base, header, slider, páginas interiores, responsive y accesibilidad.
- `js/main.js` explica qué hace cada constante, cada función y cada evento.
- `assets/README.md` explica la función de cada imagen porque los JPG no pueden llevar comentarios visibles en código.

## Recomendación para la siguiente fase

Cuando se incorporen las obras reales, conviene crear secciones con ids por año en las páginas de galería. Ejemplo en `pintura.html`:

```html
<section id="2026">
  <h2>2026</h2>
  <!-- Obras de pintura creadas en 2026 -->
</section>
```

Así los enlaces del menú como `pintura.html#2026` llevarán directamente a la sección correcta.
