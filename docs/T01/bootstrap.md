# **Bootstrap — Pinceladas fundamentales**

## **1. ¿Qué es Bootstrap?**

**Bootstrap** es un framework CSS/JS que proporciona:

- Un sistema de **grid responsive**.
- Clases CSS ya preparadas.
- Componentes visuales: botones, cards, navbar, modales, alertas...
- Utilidades para espaciado, colores, tamaños, display, flexbox, etc.
- Componentes interactivos mediante JavaScript.

La idea fundamental:

> En lugar de escribir todo el CSS desde cero, utilizamos clases que Bootstrap ya proporciona.

Por ejemplo, en CSS tradicional:

```html
<button class="boton">Guardar</button>
```

```css
.boton {
  background-color: #0d6efd;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
}
```

Con Bootstrap:

```html
<button class="btn btn-primary">Guardar</button>
```

Bootstrap ya se encarga de gran parte del estilo.

---

## **2. Incluir Bootstrap**

La forma más sencilla para empezar es mediante CDN.

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Mi página</title>
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
  </head>
  <body>
    <h1>Hola Bootstrap</h1>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

### **Idea importante**

Bootstrap tiene dos partes principales:

- **CSS** → estilos, grid, utilidades, componentes visuales.
- **JavaScript** → componentes interactivos.

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

## **3. El sistema de Grid**

Probablemente sea uno de los conceptos más importantes de Bootstrap.

Bootstrap utiliza un sistema de **12 columnas virtuales** para dividir los contenedores. Nuestras columnas reales ocuparán esas columnas virtuales.

La estructura habitual es:

```html
<div class="container">
  <div class="row">
    <div class="col">Columna 1</div>
    <div class="col">Columna 2</div>
    <div class="col">Columna 3</div>
  </div>
</div>
```

Visualmente:

```html
<div class="container border border-primary p-3">
  <div class="row border border-primary p-3">
    <div class="col border border-danger p-3">Columna 1</div>
    <div class="col border border-danger p-3">Columna 2</div>
    <div class="col border border-danger p-3">Columna 3</div>
  </div>
</div>
```

También podemos especificar el número de columnas:

```html
<div class="row">
  <div class="col-4 border-danger p-3">4 columnas</div>
  <div class="col-8 border-danger p-3">8 columnas</div>
</div>
```

Como 4 + 8 = 12 la columna de la derecha ocupará el doble que la de la izquierda:

```html
<div class="container border border-primary p-3">
  <div class="row border border-primary p-3">
    <div class="col-4 border border-danger p-3">4 columnas</div>
    <div class="col-8 border border-danger p-3">8 columnas</div>
  </div>
</div>
```

---

## **4. Responsive Design**

Aquí aparece una de las grandes ventajas de Bootstrap. Podemos indicar diferentes tamaños dependiendo del dispositivo.

```html
<div class="row">
  <div class="col-12 col-md-6 col-lg-4">Producto</div>
  <div class="col-12 col-md-6 col-lg-4">Producto</div>
  <div class="col-12 col-md-6 col-lg-4">Producto</div>
</div>
```

Esto significa:

- **Móvil o pantalla estrecha:** se verá como una pila de elementos (12 lumnas).
- **Tablet o pantalla mediana:** los elementos aparecerán emparejados de dos en dos ($6$ columnas).
- **Desktop:** los productos aparecerán en tres columnas (4 columnas).

---

## **5. Breakpoints**

Bootstrap define diferentes puntos de ruptura (_breakpoints_):

| Breakpoint  | Prefijo | Uso aproximado        |
| :---------- | :------ | :-------------------- |
| Extra small | `col-`  | Móvil                 |
| Small       | `sm`    | Móvil grande          |
| Medium      | `md`    | Tablet                |
| Large       | `lg`    | Desktop               |
| Extra large | `xl`    | Pantallas grandes     |
| XXL         | `xxl`   | Pantallas muy grandes |

Por ejemplo:

```html
<div class="col-12 col-sm-6 col-lg-3"></div>
```

Se puede interpretar como:

- `xs` (por defecto) → **12 columnas:** En pantallas pequeñas, se verán los elementos apilados.
- `sm` → **6 columnas:** En pantallas medianas, ocupará la mitad, mostrando dos elementos en paralelo.
- `lg` → **3 columnas:** En pantallas grandes, ocupará un cuarto de la pantalla, cabiendo 4 elementos por fila.

---

## **6. Container**

Normalmente trabajaremos dentro de un _container_.

```html
<div class="container">
  <h1>Mi página</h1>
</div>
```

Bootstrap centra el contenido y controla su anchura máxima.

También existe:

```html
<div class="container-fluid">Contenido a todo el ancho</div>
```

### **Diferencia:**

- `.container`

```text
┌──────────────────────────────┐
│                              │
│      CONTENIDO CENTRADO      │
│                              │
└──────────────────────────────┘
```

- `.container-fluid`

```text
┌────────────────────────────────────────────┐
│         CONTENIDO A TODO EL ANCHO          │
└────────────────────────────────────────────┘
```

Mientras que el `.container` se centra en la página y muestra márgenes a los lados, el `.container-fluid` se adapta al ancho total de la pantalla.

---

## **7. Gutters**

Las filas y columnas tienen separación interna entre ellas (márgenes/espaciado). Podemos modificarla mediante las clases `g-*`.

```html
<div class="row g-4">
  <div class="col-md-6">
    <div class="p-3 border">Bloque 1</div>
  </div>
  <div class="col-md-6">
    <div class="p-3 border">Bloque 2</div>
  </div>
</div>
```

---

## **8. Botones**

Bootstrap proporciona diferentes estilos de botones:

```html
<button class="btn btn-primary">Principal</button>
<button class="btn btn-secondary">Secundario</button>
<button class="btn btn-success">Éxito</button>
<button class="btn btn-danger">Eliminar</button>
<button class="btn btn-warning">Advertencia</button>
<button class="btn btn-info">Información</button>
```

Botones con borde (_outline_):

```html
<button class="btn btn-outline-primary">Ver detalles</button>
```

Tamaños:

```html
<button class="btn btn-primary btn-lg">Grande</button>
<button class="btn btn-primary btn-sm">Pequeño</button>
```

---

## **9. Colores**

Bootstrap proporciona una paleta semántica. Algunas clases importantes:

- `primary`
- `secondary`
- `success`
- `danger`
- `warning`
- `info`
- `light`
- `dark`

Ejemplo de uso:

```html
<p class="text-primary">Texto importante</p>
<p class="text-danger">Ha ocurrido un error</p>
<div class="bg-dark text-white p-3">Fondo oscuro</div>
```

Nomenclatura común:

- `text-*` → Color del texto
- `bg-*` → Color de fondo
- `btn-*` → Estilo de botón
- `border-*` → Color del borde

---

## **10. Spacing: margin y padding**

Una de las utilidades más usadas de Bootstrap son las clases de espaciado.

```html
<div class="p-3">Padding</div>
<div class="m-3">Margin</div>
```

**Nomenclatura:**

- `m` → margin
- `p` → padding

**Direcciones:**

- `t` → top
- `b` → bottom
- `s` → start (izquierda en LTR)
- `e` → end (derecha en LTR)
- `x` → horizontal (start + end)
- `y` → vertical (top + bottom)

**Ejemplos:**

```html
<div class="mt-3">margin-top</div>
<div class="mb-4">margin-bottom</div>
<div class="px-5">padding horizontal</div>
<div class="py-2">padding vertical</div>
```

Niveles de espaciado (del `0` al `5`):

```html
<div class="m-0">
  <div class="m-1">
    <div class="m-2">
      <div class="m-3">
        <div class="m-4">
          <div class="m-5"></div>
        </div>
      </div>
    </div>
  </div>
</div>
```

---

## **11. Flexbox mediante clases**

Bootstrap tiene muchas utilidades para Flexbox.

```html
<div class="d-flex">
  <div>Uno</div>
  <div>Dos</div>
  <div>Tres</div>
</div>
```

- **Centrar horizontalmente:**

```html
<div class="d-flex justify-content-center">
  <button class="btn btn-primary">Centrar</button>
</div>
```

- **Centrar verticalmente:**

```html
<div class="d-flex align-items-center">
  <button class="btn btn-primary">Centrar vertical</button>
</div>
```

- **Separar elementos:**

```html
<div class="d-flex justify-content-between">
  <span>Logo</span>
  <span>Usuario</span>
</div>
```

- **Cambiar orientación a columna:**

```html
<div class="d-flex flex-column">
  <div>Uno</div>
  <div>Dos</div>
  <div>Tres</div>
</div>
```

---

## **12. Tipografía**

Bootstrap proporciona clases para controlar el texto:

```html
<h1 class="display-1">Título enorme</h1>
<p class="lead">Este es un texto destacado.</p>
```

**Alineación:**

```html
<p class="text-center">Texto centrado</p>
<p class="text-end">Texto a la derecha</p>
```

**Peso y estilo:**

```html
<p class="fw-bold">Negrita</p>
<p class="fw-normal">Normal</p>
<p class="fst-italic">Cursiva</p>
```

---

## **13. Cards**

Las _cards_ son un componente muy habitual.

```html
<div class="card" style="width: 18rem;">
  <img src="imagen.jpg" class="card-img-top" alt="Producto" />
  <div class="card-body">
    <h5 class="card-title">Producto</h5>
    <p class="card-text">Descripción del producto.</p>
    <a href="#" class="btn btn-primary">Comprar</a>
  </div>
</div>
```

Combinadas con el sistema de Grid:

```html
<div class="row g-4">
  <div class="col-md-4">
    <div class="card">
      <div class="card-body">Producto 1</div>
    </div>
  </div>
  <div class="col-md-4">
    <div class="card">
      <div class="card-body">Producto 2</div>
    </div>
  </div>
  <div class="col-md-4">
    <div class="card">
      <div class="card-body">Producto 3</div>
    </div>
  </div>
</div>
```

---

## **14. Formularios**

Bootstrap facilita el aspecto de los formularios mediante `.form-label` y `.form-control`.

```html
<form>
  <div class="mb-3">
    <label for="email" class="form-label">Email</label>
    <input
      type="email"
      class="form-control"
      id="email"
      placeholder="nombre@ejemplo.com"
    />
  </div>
  <div class="mb-3">
    <label for="password" class="form-label">Contraseña</label>
    <input type="password" class="form-control" id="password" />
  </div>
  <button class="btn btn-primary">Entrar</button>
</form>
```

Ejemplo de formulario centrado en pantalla:

```html
<div class="container">
  <div class="row justify-content-center">
    <div class="col-12 col-md-6">
      <h1 class="mb-4">Iniciar sesión</h1>
      <form>
        <div class="mb-3">
          <label class="form-label">Email</label>
          <input type="email" class="form-control" />
        </div>
        <div class="mb-3">
          <label class="form-label">Contraseña</label>
          <input type="password" class="form-control" />
        </div>
        <button class="btn btn-primary w-100">Entrar</button>
      </form>
    </div>
  </div>
</div>
```

---

## **15. Navbar**

```html
<nav class="navbar navbar-expand-lg bg-body-tertiary">
  <div class="container">
    <a class="navbar-brand" href="#">Mi Web</a>
    <button
      class="navbar-toggler"
      type="button"
      data-bs-toggle="collapse"
      data-bs-target="#menu"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="menu">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link" href="#">Inicio</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Productos</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Contacto</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

Los atributos `data-bs-toggle="collapse"` y `data-bs-target="#menu"` conectan los elementos HTML con el JavaScript de Bootstrap para activar la interactividad.

---

## **16. Alertas**

```html
<div class="alert alert-success">¡Usuario creado correctamente!</div>
<div class="alert alert-danger">Se ha producido un error.</div>
<div class="alert alert-warning">Ten cuidado.</div>
<div class="alert alert-info">Información importante.</div>
```

---

## **17. Modal**

Un modal es una ventana superpuesta sobre la página.

**Botón activador:**

```html
<button
  class="btn btn-primary"
  data-bs-toggle="modal"
  data-bs-target="#miModal"
>
  Abrir modal
</button>
```

**Estructura del Modal:**

```html
<div class="modal fade" id="miModal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Confirmación</h5>
        <button
          type="button"
          class="btn-close"
          data-bs-dismiss="modal"
        ></button>
      </div>
      <div class="modal-body">¿Quieres eliminar este elemento?</div>
      <div class="modal-footer">
        <button class="btn btn-secondary" data-bs-dismiss="modal">
          Cancelar
        </button>
        <button class="btn btn-danger">Eliminar</button>
      </div>
    </div>
  </div>
</div>
```

---

## **18. Utilidades de display**

Bootstrap permite controlar la propiedad CSS `display`:

```html
<div class="d-none">No se muestra</div>
<div class="d-block">Elemento bloque</div>
```

Con soporte responsive:

```html
<div class="d-none d-md-block">Visible únicamente a partir de tamaño md</div>
```

---

## **19. Width y Height**

Utilidades para dimensiones relativas:

```html
<div class="w-25">25%</div>
<div class="w-50">50%</div>
<div class="w-75">75%</div>
<div class="w-100">100%</div>

<button class="btn btn-primary w-100">Continuar</button>
```

---

## **20. Bordes y Sombras**

```html
<div class="border">Con borde</div>
<div class="rounded">Bordes redondeados</div>
<div class="shadow">Con sombra</div>
<div class="shadow-sm">Sombra pequeña</div>
<div class="shadow-lg">Sombra grande</div>
```

---

## **21. Un ejemplo completo**

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Tienda</title>
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
      rel="stylesheet"
    />
  </head>
  <body>
    <!-- NAVBAR -->
    <nav class="navbar navbar-expand-lg bg-dark">
      <div class="container">
        <a class="navbar-brand text-white" href="#">Mi tienda</a>
        <a class="btn btn-primary" href="#">Carrito</a>
      </div>
    </nav>

    <!-- CONTENIDO -->
    <main class="container py-5">
      <div class="text-center mb-5">
        <h1 class="display-4">Nuestros productos</h1>
        <p class="lead">Los mejores productos al mejor precio.</p>
      </div>

      <!-- GRID -->
      <div class="row g-4">
        <div class="col-12 col-md-6 col-lg-4">
          <div class="card h-100 shadow-sm">
            <div class="card-body">
              <h5 class="card-title">Producto 1</h5>
              <p class="card-text">Descripción del producto.</p>
              <button class="btn btn-primary">Comprar</button>
            </div>
          </div>
        </div>

        <div class="col-12 col-md-6 col-lg-4">
          <div class="card h-100 shadow-sm">
            <div class="card-body">
              <h5 class="card-title">Producto 2</h5>
              <p class="card-text">Descripción del producto.</p>
              <button class="btn btn-primary">Comprar</button>
            </div>
          </div>
        </div>

        <div class="col-12 col-md-6 col-lg-4">
          <div class="card h-100 shadow-sm">
            <div class="card-body">
              <h5 class="card-title">Producto 3</h5>
              <p class="card-text">Descripción del producto.</p>
              <button class="btn btn-primary">Comprar</button>
            </div>
          </div>
        </div>
      </div>
    </main>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

---

## **22. La "chuleta mental" de Bootstrap**

Aprender a reconocer patrones:

### **Layout**

`container` \rightarrow `row` \rightarrow `col`

```html
<div class="container">
  <div class="row">
    <div class="col-md-6">...</div>
  </div>
</div>
```

### **Espaciado**

- Propiedades: `m` (margin), `p` (padding)
- Direcciones: `t` (top), `b` (bottom), `s` (start), `e` (end), `x` (horizontal), `y` (vertical)

```html
<div class="mt-3 px-4 mb-5"></div>
```

### **Flexbox**

`d-flex`, `justify-content-*`, `align-items-*`, `flex-column`

```html
<div class="d-flex justify-content-between align-items-center">...</div>
```

### **Texto**

- Alineación: `text-center`, `text-start`, `text-end`
- Formato: `fw-bold`, `fst-italic`, `lead`

### **Colores**

`primary`, `secondary`, `success`, `danger`, `warning`, `info`, `dark`, `light`

### **Responsive**

Breakpoints: `sm`, `md`, `lg`, `xl`, `xxl`

```html
<div class="col-12 col-md-6 col-lg-4"></div>
```

---

## **23. Algo importante: Bootstrap no sustituye a CSS**

Bootstrap no pretende eliminar CSS. Lo habitual es combinar:

$$\text{Bootstrap} + \text{CSS propio} + \text{JavaScript propio}$$

**HTML:**

```html
<div class="card mi-producto">...</div>
```

**CSS:**

```css
/* Estilo propio sobre la base de Bootstrap */
.mi-producto {
  transition: transform 0.2s;
}

.mi-producto:hover {
  transform: translateY(-5px);
}
```

---

## **24. Regla práctica para aprender Bootstrap**

Ante un problema de diseño:

```text
¿Bootstrap tiene una clase para esto?
│
├── Sí ──> Utilizar la clase
│
└── No ──> Escribir CSS propio
```

---

## **25. Conceptos a priorizar en una clase**

1. **Concepto de framework:** Qué es y por qué utilizarlo.
2. **CDN:** Inclusión de hojas de estilo y scripts.
3. **Container + Row + Col:**
   ```html
   <div class="container">
     <div class="row">
       <div class="col-md-6"></div>
     </div>
   </div>
   ```
4. **Responsive:** Uso de combinaciones como `col-12 col-md-6 col-lg-4`.
5. **Utilidades:** Espaciado (`m-*`, `p-*`), display (`d-*`), colores (`text-*`, `bg-*`) y dimensiones (`w-*`).
6. **Flexbox:** `d-flex`, `justify-content-*`, `align-items-*`.
7. **Componentes:** `btn`, `card`, `alert`, `navbar`, `modal`.
8. **Personalización:** Integración con CSS propio.

---

## **26. Ejercicio final para los alumnos**

Crear una página de productos responsive utilizando Bootstrap.

### **Requisitos**

1. **Navbar.**
2. **Título y descripción.**
3. **Grid de productos:** 6 cards.
   - Móvil $\rightarrow$ 1 producto por fila (`col-12`).
   - Tablet $\rightarrow$ 2 productos por fila (`col-md-6`).
   - Escritorio $\rightarrow$ 3 productos por fila (`col-lg-4`).
4. **Estructura de cada card:**
   - Imagen.
   - Nombre.
   - Precio.
   - Descripción.
   - Botón "Comprar".
5. **Utilizar clases de Bootstrap para:** Espaciado, Colores, Botones, Grid, Responsive y Flexbox.

### **Fase 2 (Opcional):**

_"Personaliza el diseño utilizando CSS propio sin modificar la estructura HTML de Bootstrap."_

---

## **Resumen**

> Bootstrap es un conjunto de clases y componentes que nos permite construir interfaces responsive rápidamente sin tener que implementar desde cero todo el CSS habitual.
