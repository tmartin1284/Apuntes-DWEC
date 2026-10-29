# **UNIDAD 8 - NODE JS>**

## 1. **Introducción**

### Presentación de Node

Node.js es una plataforma para el desarrollo de aplicaciones en JavaScript que se ejecutan fundamentalmente en un equipo servidor. Node.js se basa en el lenguaje JavaScript v8 y nos permite entre otras hacer las siguientes funcionalidades:

- Generar páginas dinámicas en un servidor web.
- Acceder a bases de datos relacionales (MySQL, SqlServer etc.) y no relacionales (MongoDB, CouchDB, Cassandra etc.)
- Crear, leer y escribir archivos.
- Recuperar datos de formularios HTML.
- Procesar y almacenar archivos enviados desde una página web.
- Generar y enviar a aplicaciones cliente (navegador web, aplicación móvil etc.) archivos JSON
- Interactuar con sitios de una sola página (SPA) creados en Angular, React, Vue etc.

### Bibliografía

En [programación ya](https://www.tutorialesprogramacionya.com/javascriptya/nodejsya/) podeis encontrar un tutorial pasito a pasito de la instalación de node. Explicando con detalle cada uno de los puntos.

Todo el código que vaya desarrollando estará en [este repo de github](https://github.com/tmartin1284/node)

## 1 - Instalación de Node.js

1. Descargarlo del sitio oficial: [https://nodejs.org](https://nodejs.org). La versión recomendada para la mayoría de los usuarios es (**LTS**).
2. Seguir las instrucciones del instalador en su sistema operativo (Windows -si, aceptar, si, siguiente, finalizar-, macOS o Linux).
3. Abra una ventana de la consola o terminal y verifique que Node.js y `npm` estén correctamente instalados ejecutando:

```bash
node -v
npm -v
```

---

## 2 - Módulos en Node.js (2 sistemas de módulos)

Para organizar aplicaciones en Node.js dividimos el código en archivos llamados **módulos**. Existen dos sistemas principales de módulos:

1. **CommonJS** (Sistema tradicional de Node.js mediante `require` y `module.exports`).
2. **ES Modules** (Estándar moderno de JavaScript mediante `import` y `export`).

### Problema

Crear un módulo que contenga funciones matemáticas (sumar, restar) y consumirlo desde un archivo principal utilizando ambos sistemas.

#### Opción A: CommonJS

##### `matematica.js`

```javascript
const PI = 3.1416;

function sumar(x1, x2) {
  return x1 + x2;
}

function restar(x1, x2) {
  return x1 - x2;
}

module.exports = {
  sumar,
  restar,
  PI,
};
```

##### `ejercicio1.js`

```javascript
const mat = require("./matematica");

console.log("La suma de 2+2 es " + mat.sumar(2, 2));
console.log("La resta de 10-4 es " + mat.restar(10, 4));
console.log("El valor de PI es " + mat.PI);
```

Para ejecutarlo, lanzar en la ventana de comandos `node ejercicio1.js`, o la ruta correspondiente al archivo `ejercicio1.js`.

#### Opción B: ES Modules (ESM)

Para habilitar este sistema en Node.js se debe agregar `"type": "module"` en el archivo `package.json` o nombrar los archivos con extensión `.mjs`.

##### `matematica.mjs`

```javascript
export const PI = 3.1416;

export function sumar(x1, x2) {
  return x1 + x2;
}

export function restar(x1, x2) {
  return x1 - x2;
}
```

##### `ejercicio1.mjs`

```javascript
import { sumar, restar, PI } from "./matematica.mjs";

console.log("La suma de 5+3 es " + sumar(5, 3));
console.log("La resta de 8-2 es " + restar(8, 2));
console.log("Valor de PI: " + PI);
```

## La ejecución es similar al punto anterior: `node ejercicio1.mjs`,

## 3 - Consumir módulo del núcleo de Node.js

Node.js incluye módulos por defecto (llamados _módulos del núcleo_ o _core modules_) que no requieren instalación adicional mediante `npm`. Algunos ejemplos son `os` (sistema operativo), `fs` (archivos) y `http` (servidor web).

### Problema

Desarrollar un programa que solicite información al sistema operativo donde se ejecuta el servidor (memoria disponible, sistema operativo, CPU) y la imprima por consola.

##### `ejercicio2.js`

```javascript
const os = require("node:os");

console.log("Sistema operativo: " + os.platform());
console.log("Versión del SO: " + os.release());
console.log("Memoria total: " + os.totalmem() + " bytes");
console.log("Memoria libre: " + os.freemem() + " bytes");
console.log("Número de procesadores (CPUs): " + os.cpus().length);
```

---

## 4 - Módulos para administrar el sistema de archivos: 'fs' y 'fs/promises'

El módulo `fs` (File System) nos permite crear, leer, modificar y borrar archivos en el disco duro del servidor.

### Problema

Crear un archivo de texto `.txt`, escribir información en él y posteriormente leer su contenido utilizando tanto llamadas con _callbacks_ como con _promesas_.

#### Usando `fs` con Callbacks

##### `ejercicio3a.js`

```javascript
const fs = require("node:fs");

// Crear y escribir en un archivo
fs.writeFile(
  "./archivo1.txt",
  "Línea 1 creada con Node.js\nLínea 2",
  (error) => {
    if (error) {
      console.log(error);
    } else {
      console.log("El archivo fue creado con éxito.");
    }
  },
);

// Leer el archivo
fs.readFile("./archivo1.txt", "utf-8", (error, datos) => {
  if (error) {
    console.log(error);
  } else {
    console.log("Contenido del archivo:");
    console.log(datos);
  }
});
```

#### Usando `fs/promises` (Promesas)

##### `ejercicio3b.js`

```javascript
const fs = require("node:fs/promises");

async function administrarArchivos() {
  try {
    await fs.writeFile("./archivo2.txt", "Texto escrito usando fs/promises.");
    console.log("Archivo creado correctamente.");

    const contenido = await fs.readFile("./archivo2.txt", "utf-8");
    console.log("Lectura del archivo:");
    console.log(contenido);
  } catch (error) {
    console.log("Error en la operación de archivo:", error);
  }
}

administrarArchivos();
```

---

## 5 - Módulo http

El módulo `http` de Node.js permite crear un servidor web capaz de escuchar peticiones en un puerto determinado y responder a los clientes (navegadores).

### Problema

Crear un servidor web que escuche en el puerto 8888 y devuelva un mensaje de bienvenida en formato HTML simple.

##### `ejercicio4.js`

```javascript
const http = require("node:http");

const servidor = http.createServer((pedido, respuesta) => {
  respuesta.writeHead(200, { "Content-Type": "text/html; charset=utf-8" });
  respuesta.write(
    "<!doctype html><html><head></head><body><h1>Bienvenido a mi sitio con Node.js</h1></body></html>",
  );
  respuesta.end();
});

servidor.listen(8888);

console.log("Servidor web iniciado en http://localhost:8888/");
```

### Explicación

- `http.createServer`: Crea una instancia del servidor web.
- `pedido` (`req`): Objeto de tipo `http.IncomingMessage` con los datos enviados por el navegador.
- `respuesta` (`res`): Objeto de tipo `http.ServerResponse` utilizado para responder al cliente.
- `respuesta.writeHead(...)`: Define el código de estado HTTP (200 OK) y las cabeceras (_headers_).
- `servidor.listen(8888)`: Pone al servidor a escuchar peticiones en el puerto 8888. El servidor, y el programa se quedará escuchando hasta que lo paremos con `ctrl+C`.

---

## 6 - Módulo http: datos que envía el navegador

Cuando el navegador solicita una página, envía datos como la ruta (URL), el método (GET, POST), y cabeceras con detalles del navegador.

### Problema

Crear un servidor web que inspeccione la URL y el método HTTP solicitado por el navegador y le responda mostrándole dicha información.

##### `ejercicio5.js`

```javascript
const http = require("node:http");

const servidor = http.createServer((pedido, respuesta) => {
  const url = new URL("http://localhost:8888" + pedido.url);

  respuesta.writeHead(200, { "Content-Type": "text/html; charset=utf-8" });
  respuesta.write("<!doctype html><html><head></head><body>");
  respuesta.write("<h2>Información de la petición:</h2>");
  respuesta.write("<p>URL completa: " + pedido.url + "</p>");
  respuesta.write("<p>Ruta (pathname): " + url.pathname + "</p>");
  respuesta.write("<p>Método HTTP: " + pedido.method + "</p>");
  respuesta.write("</body></html>");
  respuesta.end();
});

servidor.listen(8888);
console.log("Servidor iniciado...");
```

---

## 7 - Servidor web con Node.js que sirve páginas estáticas HTML

### Problema

Crear un servidor web que lea archivos HTML desde el disco duro y los envíe al navegador. Si se solicita la raíz `/` debe servir `index.html`. Si la página no existe, retornar un error 404.

#### Estructura de archivos

```text
ejercicio6/
├── ejercicio6.js
└── public/
    ├── index.html
    └── pagina2.html
```

##### `public/index.html`

```html
<!doctype html>
<html>
  <head>
    <title>Página principal</title>
  </head>
  <body>
    <h1>Página Principal</h1>
    <a href="pagina2.html">Ir a página 2</a>
  </body>
</html>
```

##### `public/pagina2.html`

```html
<!doctype html>
<html>
  <head>
    <title>Página 2</title>
  </head>
  <body>
    <h1>Página 2</h1>
    <a href="index.html">Volver</a>
  </body>
</html>
```

##### `ejercicio6.js`

```javascript
const http = require("node:http");
const fs = require("node:fs");

const servidor = http.createServer((pedido, respuesta) => {
  const url = new URL("http://localhost:8888" + pedido.url);
  let camino = "public" + url.pathname;
  if (camino === "public/") {
    camino = "public/index.html";
  }

  fs.stat(camino, (error) => {
    if (!error) {
      fs.readFile(camino, (error, contenido) => {
        if (error) {
          respuesta.writeHead(500, { "Content-Type": "text/plain" });
          respuesta.write("Error interno del servidor");
          respuesta.end();
        } else {
          respuesta.writeHead(200, {
            "Content-Type": "text/html; charset=utf-8",
          });
          respuesta.write(contenido);
          respuesta.end();
        }
      });
    } else {
      respuesta.writeHead(404, { "Content-Type": "text/html; charset=utf-8" });
      respuesta.write(
        "<!doctype html><html><head></head><body>Recurso inexistente</body></html>",
      );
      respuesta.end();
    }
  });
});

servidor.listen(8888);
console.log("Servidor iniciado en http://localhost:8888/");
```

---

## 8 - Servidor web de archivos estáticos (html, css, jpg, mp3, mp4, ico, etc.)

Para que un servidor web sirva correctamente imágenes, archivos CSS o recursos multimedia, debe incluir la cabecera `Content-Type` correspondiente (_MIME type_).

### Problema

Crear un servidor capaz de retornar archivos con extensión `.html`, `.css`, `.jpg`, `.ico`, `.mp3` y `.mp4`.

##### `ejercicio7.js`

```javascript
const http = require("node:http");
const fs = require("node:fs");

const mime = {
  html: "text/html",
  css: "text/css",
  jpg: "image/jpg",
  ico: "image/x-icon",
  mp3: "audio/mpeg3",
  mp4: "video/mp4",
};

const servidor = http.createServer((pedido, respuesta) => {
  const url = new URL("http://localhost:8888" + pedido.url);
  let camino = "public" + url.pathname;
  if (camino === "public/") {
    camino = "public/index.html";
  }

  fs.stat(camino, (error) => {
    if (!error) {
      fs.readFile(camino, (error, contenido) => {
        if (error) {
          respuesta.writeHead(500, { "Content-Type": "text/plain" });
          respuesta.write("Error interno");
          respuesta.end();
        } else {
          const vec = camino.split(".");
          const extension = vec[vec.length - 1];
          const mimearchivo = mime[extension] || "text/plain";

          respuesta.writeHead(200, { "Content-Type": mimearchivo });
          respuesta.write(contenido);
          respuesta.end();
        }
      });
    } else {
      respuesta.writeHead(404, { "Content-Type": "text/html" });
      respuesta.write(
        "<!doctype html><html><head></head><body>404: Recurso no encontrado</body></html>",
      );
      respuesta.end();
    }
  });
});

servidor.listen(8888);
console.log("Servidor multirrecurse iniciado en http://localhost:8888/");
```

---

## 9 - Servidor web de archivos y creación de una caché

Leer constantemente archivos desde el disco es una operación costosa. Podemos guardar los recursos leídos en memoria RAM (objeto o Map) para servirlos con mayor velocidad en posteriores peticiones.

### Problema

Implementar un diccionario que almacene en caché los contenidos de los archivos leídos previamente.

##### `ejercicio8.js`

```javascript
const http = require("node:http");
const fs = require("node:fs");

const cache = {};

const mime = {
  html: "text/html",
  css: "text/css",
  jpg: "image/jpg",
  ico: "image/x-icon",
};

const servidor = http.createServer((pedido, respuesta) => {
  const url = new URL("http://localhost:8888" + pedido.url);
  let camino = "public" + url.pathname;
  if (camino === "public/") {
    camino = "public/index.html";
  }

  // Comprobar si ya existe en la caché de memoria
  if (cache[camino]) {
    console.log("Sirviendo desde la memoria RAM (Caché): " + camino);
    const vec = camino.split(".");
    const extension = vec[vec.length - 1];
    const mimearchivo = mime[extension];
    respuesta.writeHead(200, { "Content-Type": mimearchivo });
    respuesta.write(cache[camino]);
    respuesta.end();
  } else {
    fs.stat(camino, (error) => {
      if (!error) {
        fs.readFile(camino, (error, contenido) => {
          if (error) {
            respuesta.writeHead(500, { "Content-Type": "text/plain" });
            respuesta.write("Error interno");
            respuesta.end();
          } else {
            cache[camino] = contenido; // Almacenamos en caché
            console.log("Leído desde el disco por primera vez: " + camino);
            const vec = camino.split(".");
            const extension = vec[vec.length - 1];
            const mimearchivo = mime[extension];
            respuesta.writeHead(200, { "Content-Type": mimearchivo });
            respuesta.write(contenido);
            respuesta.end();
          }
        });
      } else {
        respuesta.writeHead(404, { "Content-Type": "text/html" });
        respuesta.write(
          "<!doctype html><html><head></head><body>404: No existe</body></html>",
        );
        respuesta.end();
      }
    });
  }
});

servidor.listen(8888);
console.log("Servidor con caché iniciado");
```

---

## 10 - Recuperar datos de un formulario HTML mediante Node.js (POST)

Los datos de un formulario enviado con el método POST se transmiten en el cuerpo (_body_) de la petición HTTP divididos en fragmentos (_chunks_).

### Problema

Crear un formulario donde el usuario ingrese un nombre y su correo. Al enviar, el servidor en Node.js recuperará los datos con eventos de flujo (`data` y `end`) y mostrará una página HTML dinámica con la información recibida.

#### Estructura

```text
ejercicio9/
├── ejercicio9.js
└── public/
    └── formulario.html
```

##### `public/formulario.html`

```html
<!doctype html>
<html>
  <head>
    <title>Formulario POST</title>
  </head>
  <body>
    <form action="ingresar" method="post">
      Ingrese nombre: <input type="text" name="nombre" /><br />
      Ingrese clave: <input type="password" name="clave" /><br />
      <input type="submit" value="Enviar" />
    </form>
  </body>
</html>
```

##### `ejercicio9.js`

```javascript
const http = require("node:http");
const fs = require("node:fs");

const servidor = http.createServer((pedido, respuesta) => {
  const url = new URL("http://localhost:8888" + pedido.url);
  let camino = "public" + url.pathname;
  if (camino === "public/") {
    camino = "public/formulario.html";
  }

  if (camino === "public/ingresar") {
    procesarFormulario(pedido, respuesta);
  } else {
    fs.stat(camino, (error) => {
      if (!error) {
        fs.readFile(camino, (error, contenido) => {
          if (!error) {
            respuesta.writeHead(200, { "Content-Type": "text/html" });
            respuesta.write(contenido);
            respuesta.end();
          }
        });
      } else {
        respuesta.writeHead(404, { "Content-Type": "text/html" });
        respuesta.write("Recurso no encontrado");
        respuesta.end();
      }
    });
  }
});

function procesarFormulario(pedido, respuesta) {
  let datos = "";

  // Evento que se dispara cada vez que llega un fragmento de datos
  pedido.on("data", (datosparciales) => {
    datos += datosparciales;
  });

  // Evento que se dispara cuando termina la transmisión de datos
  pedido.on("end", () => {
    const formulario = new URLSearchParams(datos);

    respuesta.writeHead(200, { "Content-Type": "text/html; charset=utf-8" });
    respuesta.write("<!doctype html><html><head></head><body>");
    respuesta.write("Nombre ingresado: " + formulario.get("nombre") + "<br>");
    respuesta.write("Clave ingresada: " + formulario.get("clave") + "<br>");
    respuesta.write('<a href="formulario.html">Volver</a>');
    respuesta.write("</body></html>");
    respuesta.end();
  });
}

servidor.listen(8888);
console.log("Servidor POST listo en puerto 8888");
```

---

## 11 - Implementación de un libro de visitas mediante un archivo de texto

### Problema

Desarrollar una aplicación completa que permita ingresar comentarios en un libro de visitas mediante un formulario HTML. Los datos deben almacenarse permanentemente en un archivo de texto `visitas.txt` mediante `fs.appendFile` y poder ser leídos posteriormente para visualizarlos en pantalla.

#### Estructura

```text
ejercicio10/
├── ejercicio10.js
└── public/
    ├── index.html
    └── cargarcomentario.html
```

##### `public/index.html`

```html
<!doctype html>
<html>
  <head>
    <title>Libro de Visitas</title>
  </head>
  <body>
    <h1>Libro de Visitas</h1>
    <p>
      <a href="cargarcomentario.html"
        >Cargar comentario en el libro de visitas</a
      >
    </p>
    <p>
      <a href="leercomentarios"
        >Ver todos los comentarios del libro de visitas</a
      >
    </p>
  </body>
</html>
```

##### `public/cargarcomentario.html`

```html
<!doctype html>
<html>
  <head>
    <title>Cargar comentario</title>
  </head>
  <body>
    <h2>Ingrese su comentario</h2>
    <form action="cargar" method="post">
      Ingrese su nombre:<br />
      <input type="text" name="nombre" size="30" /><br /><br />
      Comentarios:<br />
      <textarea name="comentarios" rows="5" cols="50"></textarea><br /><br />
      <input type="submit" value="Enviar" />
    </form>
  </body>
</html>
```

##### `ejercicio10.js`

```javascript
const http = require("node:http");
const fs = require("node:fs");

const mime = {
  html: "text/html",
  css: "text/css",
};

const servidor = http.createServer((pedido, respuesta) => {
  const url = new URL("http://localhost:8888" + pedido.url);
  let camino = "public" + url.pathname;
  if (camino === "public/") {
    camino = "public/index.html";
  }
  encaminar(pedido, respuesta, camino);
});

servidor.listen(8888);

function encaminar(pedido, respuesta, camino) {
  switch (camino) {
    case "public/cargar": {
      grabarComentarios(pedido, respuesta);
      break;
    }
    case "public/leercomentarios": {
      leerComentarios(respuesta);
      break;
    }
    default: {
      fs.stat(camino, (error) => {
        if (!error) {
          fs.readFile(camino, (error, contenido) => {
            if (error) {
              respuesta.writeHead(500, { "Content-Type": "text/plain" });
              respuesta.write("Error interno");
              respuesta.end();
            } else {
              const vec = camino.split(".");
              const extension = vec[vec.length - 1];
              const mimearchivo = mime[extension] || "text/html";
              respuesta.writeHead(200, { "Content-Type": mimearchivo });
              respuesta.write(contenido);
              respuesta.end();
            }
          });
        } else {
          respuesta.writeHead(404, { "Content-Type": "text/html" });
          respuesta.write("Recurso no encontrado");
          respuesta.end();
        }
      });
    }
  }
}

function grabarComentarios(pedido, respuesta) {
  let info = "";
  pedido.on("data", (datosparciales) => {
    info += datosparciales;
  });
  pedido.on("end", () => {
    const formulario = new URLSearchParams(info);
    respuesta.writeHead(200, { "Content-Type": "text/html; charset=utf-8" });
    const pagina = `<!doctype html><html><head></head><body>
      Gracias ${formulario.get("nombre")} por dejar su comentario.<br><br>
      <a href="index.html">Retornar</a>
    </body></html>`;
    respuesta.end(pagina);
    grabarEnArchivo(formulario);
  });
}

function grabarEnArchivo(formulario) {
  const datos = `Nombre: ${formulario.get("nombre")}<br>Comentario: ${formulario.get("comentarios")}<hr>`;
  fs.appendFile("public/visitas.txt", datos, (error) => {
    if (error) console.log(error);
  });
}

function leerComentarios(respuesta) {
  fs.readFile("public/visitas.txt", (error, datos) => {
    respuesta.writeHead(200, { "Content-Type": "text/html; charset=utf-8" });
    respuesta.write(
      "<!doctype html><html><head></head><body><h1>Listado de Visitas</h1>",
    );
    if (error) {
      respuesta.write("Aún no hay visitas registradas.");
    } else {
      respuesta.write(datos);
    }
    respuesta.write('<br><br><a href="index.html">Retornar</a></body></html>');
    respuesta.end();
  });
}

console.log("Servidor del Libro de Visitas listo en puerto 8888");
```

---

## 12 - Recuperar datos de los parámetros de una URL (GET)

En las peticiones mediante el método GET, los parámetros viajan en la propia URL tras el signo `?` (por ejemplo: `http://localhost:8888/consultar?num1=10&num2=5`).

### Problema

Crear una aplicación donde el usuario especifique mediante un formulario GET dos números y se le muestre la suma de ambos leyendo los parámetros desde la URL.

##### `ejercicio11.js`

```javascript
const http = require("node:http");

const servidor = http.createServer((pedido, respuesta) => {
  const url = new URL("http://localhost:8888" + pedido.url);

  if (url.pathname === "/sumar") {
    const v1 = parseInt(url.searchParams.get("v1"));
    const v2 = parseInt(url.searchParams.get("v2"));
    const suma = v1 + v2;

    respuesta.writeHead(200, { "Content-Type": "text/html; charset=utf-8" });
    respuesta.write(
      `<!doctype html><html><body>La suma de ${v1} y ${v2} es: ${suma}</body></html>`,
    );
    respuesta.end();
  } else {
    respuesta.writeHead(200, { "Content-Type": "text/html; charset=utf-8" });
    respuesta.write(`
      <!doctype html>
      <html>
      <body>
        <form action="/sumar" method="get">
          Ingrese primer valor: <input type="number" name="v1"><br>
          Ingrese segundo valor: <input type="number" name="v2"><br>
          <input type="submit" value="Sumar">
        </form>
      </body>
      </html>
    `);
    respuesta.end();
  }
});

servidor.listen(8888);
console.log("Servidor GET listo en puerto 8888");
```

---

## 13 - npm (Node Package Manager)

`npm` es el administrador de paquetes por excelencia para el ecosistema de JavaScript. Nos permite inicializar proyectos y descargar módulos externos creados por la comunidad.

### Pasos básicos de trabajo

1. **Inicializar un proyecto Node.js:**  
   Crea el archivo de configuración `package.json`.
   ```bash
   npm init -y
   ```
2. **Instalar una librería/dependencia de producción:**  
   Descarga e instala el módulo dentro de la carpeta `node_modules/` y lo registra en `package.json`.
   ```bash
   npm install express
   ```
3. **Instalar dependencias de desarrollo:**  
   Para herramientas requeridas solo durante el desarrollo (por ejemplo `nodemon`).
   ```bash
   npm install --save-dev nodemon
   ```

---

## 14 - Upload de archivos al servidor con Node.js y el módulo 'formidable'

El módulo de terceros `formidable` simplifica el procesamiento de datos enviados por un formulario con codificación `multipart/form-data` (utilizada para subir imágenes o archivos).

### Instalación previa

```bash
npm install formidable
```

### Problema

Crear un formulario HTML para seleccionar y subir una imagen o archivo al servidor y almacenarlo en un directorio local llamado `uploads/`.

##### `ejercicio12.js`

```javascript
const http = require("node:http");
const formidable = require("formidable");
const fs = require("node:fs");

const servidor = http.createServer((pedido, respuesta) => {
  const url = new URL("http://localhost:8888" + pedido.url);

  if (url.pathname === "/subir" && pedido.method.toLowerCase() === "post") {
    const form = new formidable.IncomingForm({
      uploadDir: "./uploads",
      keepExtensions: true,
    });

    form.parse(pedido, (error, campos, archivos) => {
      if (error) {
        respuesta.writeHead(500, { "Content-Type": "text/plain" });
        respuesta.write("Error al subir el archivo");
        respuesta.end();
      } else {
        respuesta.writeHead(200, {
          "Content-Type": "text/html; charset=utf-8",
        });
        respuesta.write("<!doctype html><html><body>");
        respuesta.write("<h1>Archivo subido correctamente al servidor</h1>");
        respuesta.write('<a href="/">Subir otro archivo</a>');
        respuesta.write("</body></html>");
        respuesta.end();
      }
    });
  } else {
    respuesta.writeHead(200, { "Content-Type": "text/html; charset=utf-8" });
    respuesta.write(`
      <!doctype html>
      <html>
      <body>
        <h2>Subida de archivos</h2>
        <form action="/subir" method="post" enctype="multipart/form-data">
          Seleccione archivo: <input type="file" name="archivo"><br><br>
          <input type="submit" value="Subir Archivo">
        </form>
      </body>
      </html>
    `);
    respuesta.end();
  }
});

servidor.listen(8888);
console.log("Servidor para subida de archivos listo en http://localhost:8888/");
```

---

## 15 - Comunicación con el gestor de base de datos MySQL empleando el módulo 'mysql2'

Para conectar aplicaciones Node.js con bases de datos MySQL utilizaremos el controlador oficial de alto rendimiento `mysql2`.

### Instalación previa

```bash
npm install mysql2
```

### Problema

Crear una tabla `articulos` en MySQL, insertar un nuevo registro empleando parámetros para evitar _SQL Injection_, y finalmente realizar una consulta de todos los registros para listarlos en la consola.

##### `ejercicio13.js`

```javascript
const mysql = require("mysql2/promise");

async function administrarBaseDatos() {
  try {
    // 1. Establecer conexión con MySQL
    const conexion = await mysql.createConnection({
      host: "localhost",
      user: "root",
      password: "",
      database: "base1",
    });

    console.log("Conexión exitosa a la base de datos MySQL.");

    // 2. Insertar un artículo
    const sqlInsert =
      "INSERT INTO articulos (descripcion, precio) VALUES (?, ?)";
    const [resultadoInsert] = await conexion.execute(sqlInsert, [
      "Teclado Mecánico",
      4500.5,
    ]);
    console.log(
      "Artículo insertado con el ID generado: " + resultadoInsert.insertId,
    );

    // 3. Consultar todos los artículos
    const sqlSelect = "SELECT codigo, descripcion, precio FROM articulos";
    const [filas] = await conexion.execute(sqlSelect);

    console.log("\n--- Listado de artículos ---");
    filas.forEach((fila) => {
      console.log(
        `Código: ${fila.codigo} | Descripción: ${fila.descripcion} | Precio: $${fila.precio}`,
      );
    });

    // 4. Cerrar conexión
    await conexion.end();
  } catch (error) {
    console.log("Error de conexión o consulta:", error.message);
  }
}

administrarBaseDatos();
```
