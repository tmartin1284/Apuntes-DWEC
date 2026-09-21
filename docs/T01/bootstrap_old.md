# Manual de Bootstrap 5

> Guía de referencia práctica de Bootstrap 5.3, con ejemplos listos para copiar.

---

## Índice

1. [Introducción](#1-introducción)
2. [Instalación](#2-instalación)
3. [Plantilla base](#3-plantilla-base)
4. [Sistema de rejilla (grid)](#4-sistema-de-rejilla-grid)
5. [Utilidades](#5-utilidades)
6. [Tipografía](#6-tipografía)
7. [Colores y temas](#7-colores-y-temas)
8. [Componentes](#8-componentes)
9. [Formularios](#9-formularios)
10. [JavaScript: API y eventos](#10-javascript-api-y-eventos)
11. [Modo oscuro](#11-modo-oscuro)
12. [Personalización con Sass](#12-personalización-con-sass)
13. [Iconos](#13-iconos)
14. [Buenas prácticas y errores frecuentes](#14-buenas-prácticas-y-errores-frecuentes)
15. [Chuleta rápida](#15-chuleta-rápida)

---

## 1. Introducción

Bootstrap es un framework CSS (y algo de JavaScript) que aporta:

- Un **sistema de rejilla** responsive de 12 columnas basado en Flexbox.
- Componentes visuales: botones, cards, navbar, modales, alertas...
- Utilidades para espaciado, colores, tamaños, display, flexbox, etc.
- Componentes interactivos mediante JavaScript.

La idea fundamental:

> En lugar de escribir todo el CSS desde cero, utilizamos clases que Bootstrap ya proporciona.

Por ejemplo, en CSS tradicional:

```html
<button class="boton">Guardar</button> .boton { background-color: #0d6efd;
color: white; padding: 10px 20px; border: none; border-radius: 5px; }
```

Con Bootstrap:

```html
<button class="btn btn-primary">Guardar</button>
```

Bootstrap ya se encarga de gran parte del estilo.

En este tutorial nos centraremos en una de las partes fundamentales de Bootstrap:

- Contenedores
- Filas
- Columnas
- Sistema de 12 columnas
- Diseño responsive
- Breakpoints
- Separación entre columnas
- Anidación de columnas

La estructura básica que utilizaremos será:

```text
container
   │
   └── row
        │
        ├── col
        ├── col
        └── col
```

---

## 2. Instalación

### Opción A — CDN (la más rápida)

```html
<!-- CSS en el <head> -->
<link
  href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
  rel="stylesheet"
  crossorigin="anonymous"
/>

<!-- JS al final del <body> -->
<script
  src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
  crossorigin="anonymous"
></script>
```

El fichero `bootstrap.bundle.min.js` incluye **Popper**, necesario para tooltips, popovers y dropdowns. Si usas `bootstrap.min.js` a secas, tendrás que cargar Popper por separado.

### Opción B — npm

```bash
npm install bootstrap@5.3.3
npm install @popperjs/core   # si no usas el bundle
```

```js
// main.js
import "bootstrap/dist/css/bootstrap.min.css";
import * as bootstrap from "bootstrap";
```

Importar solo lo necesario reduce el peso final:

```js
import Modal from "bootstrap/js/dist/modal";
import Tooltip from "bootstrap/js/dist/tooltip";
```

### Opción C — Sass (recomendada para proyectos reales)

```scss
// 1. Tus variables antes de importar
$primary: #7952b3;
$enable-shadows: true;

// 2. Bootstrap
@import "bootstrap/scss/bootstrap";

// 3. Tus estilos
```

Ver la sección [Personalización con Sass](#12-personalización-con-sass).

Idea importante

Bootstrap tiene dos partes principales:

- CSS → estilos, grid, utilidades, componentes visuales
- JavaScript → componentes interactivos

Muchísimas cosas funcionan únicamente con CSS:

```html
<button class="btn btn-primary">Botón</button>
```

Pero otras necesitan JavaScript:

- Modal
- Dropdown
- Carousel
- Collapse
- Offcanvas
- Tooltip, etc.

---

## 3. Plantilla base

```html
<!doctype html>
<html lang="es">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Mi página</title>
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
  </head>
  <body>
    <div class="container py-5">
      <h1>Hola, Bootstrap</h1>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

La etiqueta `<meta name="viewport">` es **obligatoria**: sin ella el diseño responsive no funciona en móvil. Esta plantilla se genera automaticamente escribiendo `bs5-$` si tienes los snippets de _boostrap_ instalados (bootstrap 5 quick snippets).

---

## 4. Sistema de rejilla (grid)

### Conceptos

La rejilla tiene tres niveles: **contenedor → fila → columnas**.
Bootsgrap define **12 columnas** que son las que se van a repartir entre las columnas físicas de cada fila del contenedor.
Usa Flexbox por debajo.

```html
<div class="container">
  <div class="row">
    <div class="col">Columna A</div>
    <div class="col">Columna B</div>
  </div>
</div>
```

### Breakpoints

| Nombre            | Infijo      | Ancho mínimo | Uso típico       |
| ----------------- | ----------- | ------------ | ---------------- |
| Extra small       | _(ninguno)_ | \<576px      | Móvil vertical   |
| Small             | `sm`        | ≥576px       | Móvil horizontal |
| Medium            | `md`        | ≥768px       | Tablet           |
| Large             | `lg`        | ≥992px       | Portátil         |
| Extra large       | `xl`        | ≥1200px      | Escritorio       |
| Extra extra large | `xxl`       | ≥1400px      | Pantalla grande  |

**Clave:** Bootstrap es _mobile first_. `col-md-6` significa «6 columnas **a partir de** 768px», no «solo en tablet».

### Tipos de contenedor

```html
<div class="container">…</div>
<!-- ancho fijo por breakpoint dejará margenes a ambos lados-->
<div class="container-fluid">…</div>
<!-- se ajusta al 100% del ancho de la pantalla siempre -->
<div class="container-lg">…</div>
<!-- fluido hasta el tamaño lg, fijo a partir de ahi-->
```

### Columnas

```html
<div class="row">
  <!-- Ancho explícito -->
  <div class="col-12 col-md-8">Contenido principal</div>
  <div class="col-12 col-md-4">Barra lateral</div>
</div>

<div class="row">
  <!-- Reparto automático -->
  <div class="col">Un tercio</div>
  <div class="col">Un tercio</div>
  <div class="col">Un tercio</div>
</div>

<div class="row">
  <!-- Una fija, el resto se reparte -->
  <div class="col-3">Fija</div>
  <div class="col">Flexible</div>
  <div class="col">Flexible</div>
</div>

<div class="row">
  <!-- Ancho por contenido -->
  <div class="col-auto">Solo lo que ocupe</div>
  <div class="col">El resto</div>
</div>
```

### `row-cols`: columnas iguales sin repetir clases

```html
<div class="row row-cols-1 row-cols-sm-2 row-cols-lg-4 g-3">
  <div class="col"><div class="card">…</div></div>
  <div class="col"><div class="card">…</div></div>
  <div class="col"><div class="card">…</div></div>
  <div class="col"><div class="card">…</div></div>
</div>
```

Ideal para rejillas de tarjetas o productos.

### Gutters (separación)

```html
<div class="row g-0">…</div>
<!-- sin separación -->
<div class="row g-3">…</div>
<!-- horizontal + vertical -->
<div class="row gx-5 gy-2">…</div>
<!-- por eje -->
<div class="row g-md-4">…</div>
<!-- responsive -->
```

Escala: `g-0` a `g-5`.

### Alineación

```html
<!-- Vertical de toda la fila -->
<div class="row align-items-start | align-items-center | align-items-end">
  …
</div>

<!-- Vertical de una columna concreta -->
<div class="col align-self-center">…</div>

<!-- Horizontal -->
<div
  class="row justify-content-start | center | end | between | around | evenly"
>
  …
</div>
```

### Offset y orden

```html
<div class="row">
  <div class="col-4">Primera</div>
  <div class="col-4 offset-4">Desplazada 4 columnas</div>
</div>

<div class="row">
  <div class="col order-2 order-md-1">En móvil va segunda</div>
  <div class="col order-1 order-md-2">En móvil va primera</div>
</div>
```

También `order-first` y `order-last`.

### Anidamiento

```html
<div class="row">
  <div class="col-md-8">
    <div class="row">
      <div class="col-6">Anidada</div>
      <div class="col-6">Anidada</div>
    </div>
  </div>
</div>
```

Las filas anidadas vuelven a partir de 12 columnas dentro de su padre.

---

## 5. Utilidades

Las clases de utilidad son el 80% del trabajo diario con Bootstrap.

### Espaciado

Formato: `{propiedad}{lado}-{breakpoint}-{tamaño}`

- **Propiedad:** `m` (margin), `p` (padding)
- **Lado:** `t` top, `b` bottom, `s` start (izq.), `e` end (der.), `x` horizontal, `y` vertical, _(nada)_ todos
- **Tamaño:** `0`–`5`, o `auto`

| Clase | Valor         |
| ----- | ------------- |
| `*-0` | 0             |
| `*-1` | 0.25rem (4px) |
| `*-2` | 0.5rem (8px)  |
| `*-3` | 1rem (16px)   |
| `*-4` | 1.5rem (24px) |
| `*-5` | 3rem (48px)   |

```html
<div class="mt-3 mb-5 px-4 py-2">…</div>
<div class="mx-auto" style="width: 300px">Centrado</div>
<div class="p-2 p-md-5">Padding responsive</div>
<div class="mt-n3">Margen negativo</div>
```

### Display

```html
<div class="d-none d-md-block">Oculto en móvil</div>
<div class="d-block d-md-none">Solo en móvil</div>
<span class="d-inline-block">…</span>
<div class="d-flex">…</div>
<div class="d-grid">…</div>
<div class="d-none d-print-block">Solo al imprimir</div>
```

Valores: `none`, `inline`, `inline-block`, `block`, `grid`, `flex`, `inline-flex`, `table`.

### Flexbox

```html
<div
  class="d-flex flex-column flex-md-row justify-content-between align-items-center gap-3"
>
  <div>Izquierda</div>
  <div>Derecha</div>
</div>
```

| Familia         | Clases                                                               |
| --------------- | -------------------------------------------------------------------- | -------------------- | ---------------- | -------- | --------- | -------- |
| Dirección       | `flex-row`, `flex-column`, `flex-row-reverse`, `flex-column-reverse` |
| Eje principal   | `justify-content-{start                                              | end                  | center           | between  | around    | evenly}` |
| Eje cruzado     | `align-items-{start                                                  | end                  | center           | baseline | stretch}` |
| Varias líneas   | `align-content-*`, `flex-wrap`, `flex-nowrap`                        |
| Ítem individual | `align-self-*`, `flex-grow-{0                                        | 1}`, `flex-shrink-{0 | 1}`, `flex-fill` |
| Separación      | `gap-0` … `gap-5`, `row-gap-*`, `column-gap-*`                       |
| Auto margin     | `ms-auto`, `me-auto`, `ms-auto me-auto`                              |

`ms-auto` dentro de un flex es el truco clásico para empujar un elemento a la derecha.

### Texto

```html
<p class="text-start text-md-center text-lg-end">Alineación responsive</p>
<p class="text-uppercase fw-bold fst-italic">Mayúsculas, negrita, cursiva</p>
<p class="text-truncate" style="max-width:200px">
  Texto muy largo que se corta…
</p>
<p class="text-break">PalabraMuyLargaQueSeRompe</p>
<p class="lh-1 | lh-sm | lh-base | lh-lg">Interlineado</p>
<p class="text-nowrap">Sin saltos de línea</p>
```

Pesos: `fw-light`, `fw-normal`, `fw-medium`, `fw-semibold`, `fw-bold`, `fw-bolder`. Tamaños: `fs-1` a `fs-6` (equivalentes a `h1`–`h6`).

### Colores

```html
<p class="text-primary">Texto primario</p>
<p class="text-body-secondary">Texto secundario</p>
<div class="bg-danger text-white">Fondo rojo</div>
<div class="bg-primary bg-opacity-25">Fondo al 25%</div>
<p class="text-danger text-opacity-75">Texto al 75%</p>
```

Paleta: `primary`, `secondary`, `success`, `danger`, `warning`, `info`, `light`, `dark`. Opacidades: `10`, `25`, `50`, `75`, `100`.

### Bordes

```html
<div class="border">Todos</div>
<div class="border-top border-bottom">Solo arriba y abajo</div>
<div class="border-0 border-end">Quitar y añadir</div>
<div class="border border-primary border-3">Color y grosor</div>
<div class="rounded rounded-3">Esquinas redondeadas</div>
<div class="rounded-circle">Círculo</div>
<div class="rounded-pill">Píldora</div>
<div class="rounded-top-0">Sin redondeo arriba</div>
```

### Tamaño

```html
<div class="w-25 w-50 w-75 w-100 w-auto">Anchos relativos</div>
<div class="h-100">Alto completo</div>
<div class="mw-100 mh-100">Máximos</div>
<div class="vw-100 vh-100">Respecto al viewport</div>
<div class="min-vh-100">Mínimo pantalla completa</div>
```

### Posición

```html
<div class="position-relative">
  <span class="position-absolute top-0 end-0 p-2">Esquina</span>
  <span class="position-absolute top-50 start-50 translate-middle"
    >Centrado</span
  >
</div>

<nav class="sticky-top">Pegado arriba al hacer scroll</nav>
<footer class="fixed-bottom">Siempre visible abajo</footer>
```

### Sombras y otros

```html
<div class="shadow-none | shadow-sm | shadow | shadow-lg">…</div>
<div class="opacity-25 | 50 | 75 | 100">…</div>
<div class="overflow-auto | hidden | scroll">…</div>
<div class="user-select-none">No seleccionable</div>
<a class="link-primary link-offset-2 link-underline-opacity-25">Enlace</a>
<span class="visually-hidden">Solo para lectores de pantalla</span>
<div class="ratio ratio-16x9"><iframe src="…"></iframe></div>
```

---

## 6. Tipografía

```html
<h1 class="display-1">Display 1</h1>
<h1 class="display-4">Display 4</h1>

<p class="lead">Párrafo destacado de entradilla.</p>

<h3>Título <small class="text-body-secondary">con subtítulo</small></h3>

<blockquote class="blockquote">
  <p>Una cita.</p>
</blockquote>
<figcaption class="blockquote-footer">Autor en <cite>Fuente</cite></figcaption>

<ul class="list-unstyled">
  …
</ul>
<ul class="list-inline">
  <li class="list-inline-item">Uno</li>
  <li class="list-inline-item">Dos</li>
</ul>

<p><abbr title="HyperText Markup Language">HTML</abbr></p>
<p>
  <mark>Resaltado</mark> y <code>código</code> y <kbd>Ctrl</kbd>+<kbd>C</kbd>
</p>
```

Clases `h1`–`h6` aplicables a cualquier etiqueta: `<p class="h3">Parece un h3</p>`.

---

## 7. Colores y temas

Bootstrap 5.3 expone variables CSS que puedes sobrescribir sin recompilar Sass:

```css
:root {
  --bs-primary: #7952b3;
  --bs-primary-rgb: 121, 82, 179;
  --bs-body-font-family: "Inter", sans-serif;
  --bs-body-bg: #fafafa;
  --bs-border-radius: 0.5rem;
}
```

> **Cuidado:** cambiar `--bs-primary` no repinta los botones `.btn-primary`, porque estos se compilan en Sass. Para un cambio de marca real, recompila Sass (sección 12) o sobrescribe también las variables del componente:

```css
.btn-primary {
  --bs-btn-bg: #7952b3;
  --bs-btn-border-color: #7952b3;
  --bs-btn-hover-bg: #614092;
  --bs-btn-hover-border-color: #614092;
}
```

Cada componente de 5.3 tiene su propio juego de variables locales (`--bs-btn-*`, `--bs-card-*`, `--bs-nav-*`…), lo que permite variantes sin escribir CSS a mano.

---

## 8. Componentes

### Botones

```html
<button class="btn btn-primary">Primario</button>
<button class="btn btn-outline-secondary">Contorno</button>
<button class="btn btn-link">Enlace</button>

<button class="btn btn-primary btn-sm">Pequeño</button>
<button class="btn btn-primary btn-lg">Grande</button>

<button class="btn btn-primary" disabled>Desactivado</button>
<a href="#" class="btn btn-primary disabled" aria-disabled="true"
  >Enlace desactivado</a
>

<button class="btn btn-primary" type="button" disabled>
  <span class="spinner-border spinner-border-sm" aria-hidden="true"></span>
  Cargando…
</button>

<div class="d-grid gap-2">
  <button class="btn btn-primary">Ancho completo</button>
</div>

<div class="btn-group" role="group" aria-label="Acciones">
  <button class="btn btn-outline-primary">Izquierda</button>
  <button class="btn btn-outline-primary">Centro</button>
  <button class="btn btn-outline-primary">Derecha</button>
</div>

<!-- Toggle -->
<input type="checkbox" class="btn-check" id="btn1" autocomplete="off" />
<label class="btn btn-outline-primary" for="btn1">Alternar</label>
```

### Navbar

```html
<nav class="navbar navbar-expand-lg bg-body-tertiary">
  <div class="container">
    <a class="navbar-brand" href="#">MiSitio</a>

    <button
      class="navbar-toggler"
      type="button"
      data-bs-toggle="collapse"
      data-bs-target="#nav"
      aria-controls="nav"
      aria-expanded="false"
      aria-label="Menú"
    >
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="nav">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <a class="nav-link active" aria-current="page" href="#">Inicio</a>
        </li>
        <li class="nav-item"><a class="nav-link" href="#">Servicios</a></li>
        <li class="nav-item dropdown">
          <a
            class="nav-link dropdown-toggle"
            href="#"
            role="button"
            data-bs-toggle="dropdown"
          >
            Más
          </a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Opción 1</a></li>
            <li><hr class="dropdown-divider" /></li>
            <li><a class="dropdown-item" href="#">Opción 2</a></li>
          </ul>
        </li>
      </ul>
      <form class="d-flex" role="search">
        <input
          class="form-control me-2"
          type="search"
          placeholder="Buscar"
          aria-label="Buscar"
        />
        <button class="btn btn-outline-success" type="submit">Buscar</button>
      </form>
    </div>
  </div>
</nav>
```

- `navbar-expand-{bp}`: a partir de ese breakpoint el menú se despliega horizontal; por debajo, colapsa en hamburguesa.
- Para fondo oscuro: `<nav class="navbar bg-dark" data-bs-theme="dark">`.
- Fijar arriba: añade `fixed-top` y compensa con `padding-top` en el `<body>`.

### Cards

```html
<div class="card" style="width: 18rem;">
  <img src="foto.jpg" class="card-img-top" alt="…" />
  <div class="card-body">
    <h5 class="card-title">Título</h5>
    <h6 class="card-subtitle mb-2 text-body-secondary">Subtítulo</h6>
    <p class="card-text">Descripción breve de la tarjeta.</p>
    <a href="#" class="btn btn-primary">Ir</a>
  </div>
  <ul class="list-group list-group-flush">
    <li class="list-group-item">Dato 1</li>
    <li class="list-group-item">Dato 2</li>
  </ul>
  <div class="card-footer text-body-secondary">Hace 3 días</div>
</div>
```

Tarjetas de igual altura en rejilla:

```html
<div class="row row-cols-1 row-cols-md-3 g-4">
  <div class="col">
    <div class="card h-100">…</div>
  </div>
</div>
```

### Tablas

```html
<div class="table-responsive">
  <table class="table table-striped table-hover table-bordered align-middle">
    <thead class="table-dark">
      <tr>
        <th scope="col">#</th>
        <th scope="col">Nombre</th>
        <th scope="col">Estado</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th scope="row">1</th>
        <td>Ana</td>
        <td><span class="badge text-bg-success">Activa</span></td>
      </tr>
      <tr class="table-warning">
        <th scope="row">2</th>
        <td>Luis</td>
        <td>Pendiente</td>
      </tr>
    </tbody>
  </table>
</div>
```

Variantes: `table-sm`, `table-borderless`, `table-striped-columns`, `table-group-divider`.

### Alertas

```html
<div class="alert alert-success" role="alert">Guardado correctamente.</div>

<div class="alert alert-warning alert-dismissible fade show" role="alert">
  <strong>Atención:</strong> revisa los datos.
  <button
    type="button"
    class="btn-close"
    data-bs-dismiss="alert"
    aria-label="Cerrar"
  ></button>
</div>

<div class="alert alert-danger">
  <h4 class="alert-heading">Error</h4>
  <p>No se pudo conectar.</p>
  <hr />
  <p class="mb-0">Inténtalo más tarde.</p>
</div>
```

### Badges

```html
<span class="badge text-bg-primary">Nuevo</span>
<span class="badge rounded-pill text-bg-danger">9</span>

<button class="btn btn-primary position-relative">
  Mensajes
  <span
    class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger"
  >
    4 <span class="visually-hidden">sin leer</span>
  </span>
</button>
```

### Modales

```html
<button
  class="btn btn-primary"
  data-bs-toggle="modal"
  data-bs-target="#miModal"
>
  Abrir
</button>

<div
  class="modal fade"
  id="miModal"
  tabindex="-1"
  aria-labelledby="miModalLabel"
  aria-hidden="true"
>
  <div
    class="modal-dialog modal-lg modal-dialog-centered modal-dialog-scrollable"
  >
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5" id="miModalLabel">Título</h1>
        <button
          type="button"
          class="btn-close"
          data-bs-dismiss="modal"
          aria-label="Cerrar"
        ></button>
      </div>
      <div class="modal-body">Contenido del modal.</div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
          Cancelar
        </button>
        <button type="button" class="btn btn-primary">Guardar</button>
      </div>
    </div>
  </div>
</div>
```

Tamaños: `modal-sm`, `modal-lg`, `modal-xl`, `modal-fullscreen`, `modal-fullscreen-md-down`.

Control por JS:

```js
const modal = new bootstrap.Modal("#miModal");
modal.show();
modal.hide();
```

### Dropdowns

```html
<div class="dropdown">
  <button
    class="btn btn-secondary dropdown-toggle"
    type="button"
    data-bs-toggle="dropdown"
    aria-expanded="false"
  >
    Acciones
  </button>
  <ul class="dropdown-menu dropdown-menu-end">
    <li><h6 class="dropdown-header">Sección</h6></li>
    <li><a class="dropdown-item" href="#">Editar</a></li>
    <li><a class="dropdown-item active" href="#">Duplicar</a></li>
    <li><hr class="dropdown-divider" /></li>
    <li><a class="dropdown-item disabled" href="#">Borrar</a></li>
  </ul>
</div>
```

Dirección: envuelve en `.dropup`, `.dropend`, `.dropstart`.

### Pestañas (tabs) y pills

```html
<ul class="nav nav-tabs" role="tablist">
  <li class="nav-item" role="presentation">
    <button
      class="nav-link active"
      data-bs-toggle="tab"
      data-bs-target="#t1"
      type="button"
      role="tab"
      aria-selected="true"
    >
      Uno
    </button>
  </li>
  <li class="nav-item" role="presentation">
    <button
      class="nav-link"
      data-bs-toggle="tab"
      data-bs-target="#t2"
      type="button"
      role="tab"
      aria-selected="false"
    >
      Dos
    </button>
  </li>
</ul>

<div class="tab-content pt-3">
  <div class="tab-pane fade show active" id="t1" role="tabpanel">
    Contenido 1
  </div>
  <div class="tab-pane fade" id="t2" role="tabpanel">Contenido 2</div>
</div>
```

Variantes de `nav`: `nav-pills`, `nav-underline`, `nav-fill`, `nav-justified`.

### Acordeón

```html
<div class="accordion" id="acc">
  <div class="accordion-item">
    <h2 class="accordion-header">
      <button
        class="accordion-button"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#c1"
      >
        Primera sección
      </button>
    </h2>
    <div id="c1" class="accordion-collapse collapse show" data-bs-parent="#acc">
      <div class="accordion-body">Contenido de la primera.</div>
    </div>
  </div>

  <div class="accordion-item">
    <h2 class="accordion-header">
      <button
        class="accordion-button collapsed"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#c2"
      >
        Segunda sección
      </button>
    </h2>
    <div id="c2" class="accordion-collapse collapse" data-bs-parent="#acc">
      <div class="accordion-body">Contenido de la segunda.</div>
    </div>
  </div>
</div>
```

Quitar `data-bs-parent` permite varias secciones abiertas a la vez. Con `.accordion-flush` se elimina el borde exterior.

### Collapse suelto

```html
<button
  class="btn btn-primary"
  data-bs-toggle="collapse"
  data-bs-target="#detalle"
  aria-expanded="false"
>
  Ver detalle
</button>
<div class="collapse" id="detalle">
  <div class="card card-body">Contenido plegable.</div>
</div>
```

### Carrusel

```html
<div id="carr" class="carousel slide" data-bs-ride="carousel">
  <div class="carousel-indicators">
    <button
      data-bs-target="#carr"
      data-bs-slide-to="0"
      class="active"
      aria-current="true"
    ></button>
    <button data-bs-target="#carr" data-bs-slide-to="1"></button>
  </div>
  <div class="carousel-inner">
    <div class="carousel-item active" data-bs-interval="5000">
      <img src="1.jpg" class="d-block w-100" alt="…" />
      <div class="carousel-caption d-none d-md-block">
        <h5>Primera</h5>
        <p>Descripción.</p>
      </div>
    </div>
    <div class="carousel-item">
      <img src="2.jpg" class="d-block w-100" alt="…" />
    </div>
  </div>
  <button
    class="carousel-control-prev"
    type="button"
    data-bs-target="#carr"
    data-bs-slide="prev"
  >
    <span class="carousel-control-prev-icon"></span>
    <span class="visually-hidden">Anterior</span>
  </button>
  <button
    class="carousel-control-next"
    type="button"
    data-bs-target="#carr"
    data-bs-slide="next"
  >
    <span class="carousel-control-next-icon"></span>
    <span class="visually-hidden">Siguiente</span>
  </button>
</div>
```

### Offcanvas (panel lateral)

```html
<button
  class="btn btn-primary"
  data-bs-toggle="offcanvas"
  data-bs-target="#panel"
>
  Abrir panel
</button>

<div
  class="offcanvas offcanvas-end"
  tabindex="-1"
  id="panel"
  aria-labelledby="panelLabel"
>
  <div class="offcanvas-header">
    <h5 class="offcanvas-title" id="panelLabel">Filtros</h5>
    <button
      type="button"
      class="btn-close"
      data-bs-dismiss="offcanvas"
      aria-label="Cerrar"
    ></button>
  </div>
  <div class="offcanvas-body">Contenido del panel.</div>
</div>
```

Posiciones: `offcanvas-start`, `offcanvas-end`, `offcanvas-top`, `offcanvas-bottom`. Con `offcanvas-lg` el panel solo se comporta como offcanvas por debajo de `lg`.

### Toasts

```html
<div class="toast-container position-fixed bottom-0 end-0 p-3">
  <div
    id="miToast"
    class="toast"
    role="alert"
    aria-live="assertive"
    aria-atomic="true"
  >
    <div class="toast-header">
      <strong class="me-auto">Notificación</strong>
      <small>ahora</small>
      <button
        type="button"
        class="btn-close"
        data-bs-dismiss="toast"
        aria-label="Cerrar"
      ></button>
    </div>
    <div class="toast-body">Cambios guardados.</div>
  </div>
</div>

<script>
  const toast = new bootstrap.Toast(document.getElementById("miToast"), {
    delay: 4000,
  });
  toast.show();
</script>
```

Los toasts están ocultos por defecto: hay que llamar a `.show()`.

### Tooltips y popovers

Requieren inicialización manual:

```html
<button
  class="btn btn-secondary"
  data-bs-toggle="tooltip"
  data-bs-placement="top"
  data-bs-title="Texto de ayuda"
>
  Pasa el ratón
</button>

<button
  class="btn btn-danger"
  data-bs-toggle="popover"
  data-bs-title="Título"
  data-bs-content="Contenido del popover"
>
  Púlsame
</button>

<script>
  document
    .querySelectorAll('[data-bs-toggle="tooltip"]')
    .forEach((el) => new bootstrap.Tooltip(el));
  document
    .querySelectorAll('[data-bs-toggle="popover"]')
    .forEach((el) => new bootstrap.Popover(el));
</script>
```

### Paginación y breadcrumb

```html
<nav aria-label="Paginación">
  <ul class="pagination justify-content-center">
    <li class="page-item disabled">
      <a class="page-link" href="#">Anterior</a>
    </li>
    <li class="page-item active" aria-current="page">
      <a class="page-link" href="#">1</a>
    </li>
    <li class="page-item"><a class="page-link" href="#">2</a></li>
    <li class="page-item"><a class="page-link" href="#">Siguiente</a></li>
  </ul>
</nav>

<nav aria-label="Migas de pan">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="#">Inicio</a></li>
    <li class="breadcrumb-item"><a href="#">Catálogo</a></li>
    <li class="breadcrumb-item active" aria-current="page">Producto</li>
  </ol>
</nav>
```

### Progreso y spinners

```html
<div
  class="progress"
  role="progressbar"
  aria-valuenow="65"
  aria-valuemin="0"
  aria-valuemax="100"
>
  <div
    class="progress-bar bg-success progress-bar-striped progress-bar-animated"
    style="width: 65%"
  >
    65%
  </div>
</div>

<div class="progress-stacked">
  <div class="progress" role="progressbar" style="width: 30%">
    <div class="progress-bar"></div>
  </div>
  <div class="progress" role="progressbar" style="width: 20%">
    <div class="progress-bar bg-warning"></div>
  </div>
</div>

<div class="spinner-border text-primary" role="status">
  <span class="visually-hidden">Cargando…</span>
</div>
<div class="spinner-grow spinner-grow-sm text-secondary" role="status"></div>
```

### List group

```html
<ul class="list-group">
  <li class="list-group-item active" aria-current="true">Activo</li>
  <li class="list-group-item d-flex justify-content-between align-items-center">
    Mensajes
    <span class="badge text-bg-primary rounded-pill">14</span>
  </li>
  <li class="list-group-item disabled">Desactivado</li>
</ul>

<div class="list-group">
  <a href="#" class="list-group-item list-group-item-action">Enlace pulsable</a>
  <a
    href="#"
    class="list-group-item list-group-item-action list-group-item-danger"
    >Peligro</a
  >
</div>
```

Variantes: `list-group-flush`, `list-group-numbered`, `list-group-horizontal-md`.

---

## 9. Formularios

### Estructura habitual

```html
<form class="needs-validation" novalidate>
  <div class="row g-3">
    <div class="col-md-6">
      <label for="nombre" class="form-label">Nombre</label>
      <input type="text" class="form-control" id="nombre" required />
      <div class="invalid-feedback">Introduce tu nombre.</div>
    </div>

    <div class="col-md-6">
      <label for="email" class="form-label">Correo</label>
      <input type="email" class="form-control" id="email" required />
      <div class="form-text">No lo compartiremos con nadie.</div>
      <div class="invalid-feedback">Correo no válido.</div>
    </div>

    <div class="col-12">
      <label for="pais" class="form-label">País</label>
      <select class="form-select" id="pais" required>
        <option value="">Elige…</option>
        <option>España</option>
        <option>México</option>
      </select>
      <div class="invalid-feedback">Selecciona un país.</div>
    </div>

    <div class="col-12">
      <label for="comentario" class="form-label">Comentario</label>
      <textarea class="form-control" id="comentario" rows="3"></textarea>
    </div>

    <div class="col-12">
      <div class="form-check">
        <input class="form-check-input" type="checkbox" id="acepto" required />
        <label class="form-check-label" for="acepto"
          >Acepto las condiciones</label
        >
        <div class="invalid-feedback">Debes aceptarlas.</div>
      </div>
    </div>

    <div class="col-12">
      <button class="btn btn-primary" type="submit">Enviar</button>
    </div>
  </div>
</form>
```

### Controles disponibles

```html
<input class="form-control form-control-lg | form-control-sm" />
<input class="form-control" type="file" />
<input class="form-control form-control-color" type="color" value="#563d7c" />
<input class="form-range" type="range" min="0" max="100" step="5" />
<input class="form-control" readonly value="Solo lectura" />
<input class="form-control-plaintext" readonly value="Sin caja" />
<select class="form-select" multiple size="3">
  …
</select>
```

Radios, checks y switches:

```html
<div class="form-check">
  <input class="form-check-input" type="radio" name="op" id="r1" checked />
  <label class="form-check-label" for="r1">Opción A</label>
</div>

<div class="form-check form-check-inline">…</div>

<div class="form-check form-switch">
  <input class="form-check-input" type="checkbox" role="switch" id="sw" />
  <label class="form-check-label" for="sw">Activar notificaciones</label>
</div>
```

### Input groups

```html
<div class="input-group mb-3">
  <span class="input-group-text">@</span>
  <input type="text" class="form-control" placeholder="usuario" />
</div>

<div class="input-group">
  <input type="text" class="form-control" placeholder="Buscar" />
  <button class="btn btn-outline-secondary" type="button">Ir</button>
</div>

<div class="input-group input-group-lg">
  <span class="input-group-text">€</span>
  <input type="number" class="form-control" />
  <span class="input-group-text">,00</span>
</div>
```

### Floating labels

```html
<div class="form-floating mb-3">
  <input
    type="email"
    class="form-control"
    id="fl1"
    placeholder="nombre@ejemplo.com"
  />
  <label for="fl1">Correo electrónico</label>
</div>
```

El atributo `placeholder` es obligatorio aunque no se vea; sin él la animación no funciona.

### Validación

Bootstrap estiliza `:valid` / `:invalid`, pero necesitas activar la validación del navegador:

```js
document.querySelectorAll(".needs-validation").forEach((form) => {
  form.addEventListener(
    "submit",
    (event) => {
      if (!form.checkValidity()) {
        event.preventDefault();
        event.stopPropagation();
      }
      form.classList.add("was-validated");
    },
    false,
  );
});
```

Validación desde servidor: añade a mano `is-valid` o `is-invalid` al control y muestra `.valid-feedback` / `.invalid-feedback`.

### Formularios horizontales

```html
<form>
  <div class="row mb-3">
    <label for="h1" class="col-sm-3 col-form-label">Nombre</label>
    <div class="col-sm-9">
      <input type="text" class="form-control" id="h1" />
    </div>
  </div>
</form>
```

---

## 10. JavaScript: API y eventos

### Dos formas de usar los componentes

**Declarativa** (atributos `data-bs-*`) — no requiere escribir JS:

```html
<button data-bs-toggle="modal" data-bs-target="#m">Abrir</button>
```

**Programática:**

```js
// Crear
const modal = new bootstrap.Modal("#m", {
  backdrop: "static",
  keyboard: false,
});

// Recuperar una instancia ya creada
const existente = bootstrap.Modal.getInstance("#m");

// Recuperar o crear
const inst = bootstrap.Modal.getOrCreateInstance("#m");

// Métodos comunes
modal.show();
modal.hide();
modal.toggle();
modal.dispose(); // libera la instancia
```

### Opciones por atributo

Cualquier opción se puede pasar en HTML en kebab-case:

```html
<div class="modal" data-bs-backdrop="static" data-bs-keyboard="false">…</div>
<div class="toast" data-bs-delay="10000" data-bs-autohide="false">…</div>
<div class="carousel" data-bs-interval="3000" data-bs-pause="hover">…</div>
```

### Eventos

Patrón general: `show.bs.*`, `shown.bs.*`, `hide.bs.*`, `hidden.bs.*`.

```js
const el = document.getElementById("miModal");

el.addEventListener("show.bs.modal", (e) => {
  // e.relatedTarget = el botón que lo abrió
  console.log("abriendo…", e.relatedTarget);
});

el.addEventListener("shown.bs.modal", () => {
  el.querySelector("input")?.focus();
});

el.addEventListener("hidden.bs.modal", () => {
  console.log("cerrado del todo");
});
```

Eventos específicos: `slid.bs.carousel`, `closed.bs.alert`, `inserted.bs.tooltip`, `shown.bs.tab` (con `e.target` y `e.relatedTarget` para la pestaña nueva y la anterior).

### Componentes con JS

`Alert`, `Button`, `Carousel`, `Collapse`, `Dropdown`, `Modal`, `Offcanvas`, `Popover`, `ScrollSpy`, `Tab`, `Toast`, `Tooltip`.

### ScrollSpy

```html
<body
  data-bs-spy="scroll"
  data-bs-target="#navbar"
  data-bs-offset="80"
  tabindex="0"
></body>
```

Resalta automáticamente el enlace de navegación correspondiente a la sección visible.

---

## 11. Modo oscuro

Desde 5.3, con el atributo `data-bs-theme`:

```html
<html lang="es" data-bs-theme="dark"></html>
```

También por secciones:

```html
<div data-bs-theme="dark" class="p-4">
  Esta zona va en oscuro aunque la página esté en claro.
</div>
```

Alternador que respeta la preferencia del sistema y guarda la elección:

```js
const getTheme = () =>
  localStorage.getItem("theme") ||
  (window.matchMedia("(prefers-color-scheme: dark)").matches
    ? "dark"
    : "light");

const setTheme = (theme) => {
  document.documentElement.setAttribute("data-bs-theme", theme);
  localStorage.setItem("theme", theme);
};

setTheme(getTheme());

document.getElementById("toggle")?.addEventListener("click", () => {
  setTheme(getTheme() === "dark" ? "light" : "dark");
});
```

Para que los colores se adapten, usa las utilidades semánticas (`bg-body`, `bg-body-tertiary`, `text-body`, `text-body-secondary`, `border-body`) en lugar de `bg-white` o `text-dark`, que son fijos.

---

## 12. Personalización con Sass

### Estructura recomendada

```
src/
├── scss/
│   ├── _variables.scss
│   ├── _custom.scss
│   └── main.scss
```

```scss
// main.scss

// 1. Funciones (necesarias para manipular colores)
@import "bootstrap/scss/functions";

// 2. Tus variables sobrescritas
$primary:       #7952b3;
$secondary:     #6c757d;
$font-family-sans-serif: "Inter", system-ui, sans-serif;
$border-radius: 0.5rem;
$enable-shadows: true;
$enable-gradients: false;

// 3. Variables base y mapas de Bootstrap
@import "bootstrap/scss/variables";
@import "bootstrap/scss/variables-dark";

// 4. Ampliar mapas (colores propios)
$theme-colors: map-merge($theme-colors, (
  "marca": #ff6b00,
  "neutro": #8e9aaf
));

// 5. El resto
@import "bootstrap/scss/maps";
@import "bootstrap/scss/mixins";
@import "bootstrap/scss/root";
@import "bootstrap/scss/bootstrap";

// 6. Tus estilos propios
.mi-componente { … }
```

Añadir `"marca"` a `$theme-colors` genera automáticamente `.btn-marca`, `.text-marca`, `.bg-marca`, `.border-marca`, etc.

### Importar solo lo necesario

```scss
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
@import "bootstrap/scss/mixins";
@import "bootstrap/scss/root";
@import "bootstrap/scss/reboot";
@import "bootstrap/scss/grid";
@import "bootstrap/scss/buttons";
@import "bootstrap/scss/forms";
@import "bootstrap/scss/utilities";
@import "bootstrap/scss/utilities/api"; // siempre al final
```

### Variables globales útiles

| Variable                  | Efecto                              |
| ------------------------- | ----------------------------------- |
| `$grid-breakpoints`       | Puntos de corte                     |
| `$container-max-widths`   | Anchos máximos del contenedor       |
| `$spacer`                 | Base de toda la escala de espaciado |
| `$grid-gutter-width`      | Separación entre columnas           |
| `$border-radius`          | Redondeo general                    |
| `$enable-rounded`         | Activa/desactiva redondeos          |
| `$enable-shadows`         | Sombras en componentes              |
| `$enable-dark-mode`       | Genera los estilos de modo oscuro   |
| `$body-bg`, `$body-color` | Fondo y texto base                  |

### Crear utilidades propias

```scss
@import "bootstrap/scss/utilities";

$utilities: map-merge(
  $utilities,
  (
    "cursor": (
      property: cursor,
      class: cursor,
      values: pointer grab not-allowed,
    ),
  )
);

@import "bootstrap/scss/utilities/api";
```

Genera `.cursor-pointer`, `.cursor-grab`, `.cursor-not-allowed`.

### Reducir peso en producción

Con PurgeCSS o el `content` de un pipeline moderno puedes eliminar las clases sin usar. Bootstrap completo ronda los 230 KB minificados; un build a medida suele quedarse en 30–60 KB.

---

## 13. Iconos

Bootstrap Icons es un paquete independiente (≈2000 iconos SVG).

```html
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css"
/>

<i class="bi bi-house-door"></i>
<i class="bi bi-trash text-danger fs-4"></i>
<button class="btn btn-primary">
  <i class="bi bi-download me-2"></i>Descargar
</button>
```

Como SVG suelto:

```html
<svg class="bi" width="24" height="24" fill="currentColor">
  <use xlink:href="bootstrap-icons.svg#heart" />
</svg>
```

Añade `aria-hidden="true"` si el icono es decorativo, o `role="img"` con `aria-label` si transmite información.

---

## 14. Buenas prácticas y errores frecuentes

### Errores habituales

1. **Olvidar la meta viewport** → el responsive no funciona en móvil.
2. **Columnas fuera de `.row`** → los gutters producen desbordamiento horizontal.
3. **`.row` fuera de un contenedor** → márgenes negativos sin compensar.
4. **Usar `bootstrap.min.js` y esperar que funcionen dropdowns/tooltips** → falta Popper; usa el bundle.
5. **Cargar el JS antes que el HTML** → scripts al final del `<body>` o con `defer`.
6. **Esperar que tooltips y popovers funcionen solos** → hay que inicializarlos.
7. **IDs duplicados** en modales o acordeones → se abre siempre el primero.
8. **Sobrescribir Bootstrap con `!important`** → mejor variables CSS o Sass.
9. **Pensar que `col-md-6` es «solo en tablet»** → es «de tablet en adelante».
10. **Usar `bg-white` en un sitio con modo oscuro** → usa `bg-body`.

### Recomendaciones

- **Mobile first:** diseña primero la versión estrecha y añade `col-md-*`, `d-lg-*` después.
- **Utilidades antes que CSS propio.** Si repites la misma combinación cinco veces, entonces sí crea una clase.
- **Un solo `container`** por sección, sin anidarlos.
- **Accesibilidad:** `aria-label` en botones sin texto, `scope` en las cabeceras de tabla, contraste suficiente, `visually-hidden` para texto solo de lectores de pantalla.
- **Personaliza con Sass** en cuanto el proyecto pase de una landing.
- **No mezcles versiones** de CSS y JS de Bootstrap.
- **Comprueba el orden de las hojas de estilo:** tu CSS siempre después del de Bootstrap.

---

## 15. Chuleta rápida

```
CONTENEDORES   container · container-fluid · container-{sm|md|lg|xl|xxl}
REJILLA        row · col · col-{1..12} · col-{bp}-{1..12} · col-auto
               row-cols-{1..6} · offset-{n} · order-{n} · g-{0..5} · gx- · gy-

ESPACIADO      m|p + t|b|s|e|x|y + -{bp}- + 0..5|auto      p.ej. mt-md-4
DISPLAY        d-{none|block|inline|inline-block|flex|grid}  · d-{bp}-*
FLEX           flex-{row|column} · justify-content-* · align-items-*
               gap-{0..5} · flex-fill · flex-grow-1 · ms-auto

TEXTO          text-{start|center|end} · text-{uppercase|lowercase|capitalize}
               fw-{light..bolder} · fs-{1..6} · lh-* · text-truncate
COLOR          text-* · bg-* · bg-opacity-{10..100} · text-body-secondary
BORDES         border · border-{top|end|bottom|start} · border-{color} · border-{1..5}
               rounded · rounded-{0..5|circle|pill}
TAMAÑO         w-{25|50|75|100|auto} · h-100 · vh-100 · min-vh-100
POSICIÓN       position-{static|relative|absolute|fixed|sticky}
               top-0 · start-50 · translate-middle · fixed-top · sticky-top
OTRAS          shadow-{sm|""|lg} · opacity-* · overflow-* · visually-hidden
               ratio ratio-16x9

COMPONENTES    btn btn-* · card · navbar · nav-tabs · dropdown · modal
               alert · badge · table · accordion · collapse · carousel
               offcanvas · toast · tooltip · popover · pagination
               breadcrumb · progress · spinner-border · list-group

FORMULARIOS    form-control · form-select · form-check · form-switch
               form-range · form-label · form-text · form-floating
               input-group · is-valid · is-invalid · was-validated

ATRIBUTOS JS   data-bs-toggle · data-bs-target · data-bs-dismiss
               data-bs-parent · data-bs-ride · data-bs-slide · data-bs-theme
```

### Enlaces oficiales

- Documentación: <https://getbootstrap.com/docs/5.3/>
- Bootstrap Icons: <https://icons.getbootstrap.com/>
- Ejemplos y plantillas: <https://getbootstrap.com/docs/5.3/examples/>
