**Markdown** es un lenguaje de marcado ligero creado por John Gruber y Aaron Swartz en 2004. Su objetivo es ofrecer máxima legibilidad y facilidad de escritura, permitiendo convertir texto plano en HTML válido y otros formatos visuales.

---

## 1. Instalación y Herramientas

Markdown en sí no requiere una "instalación" como un programa ejecutable, ya que es una sintaxis de texto plano. Sin embargo, para escribirlo, visualizarlo y exportarlo se utilizan editores e intérpretes.

### Editores recomendados

- **VS Code (Visual Studio Code):** Incluye previsualización nativa. Soporta extensiones como _Markdown All in One_ o _Markdown Preview Enhanced_.
- **Typora:** Editor WYSIWYG ("lo que ves es lo que obtienes") con previsualización en tiempo real.
- **Obsidian / Logseq:** Herramientas para gestión del conocimiento orientadas al formato Markdown.
- **MarkText:** Editor de código abierto centrado en una experiencia limpia y sin distracciones.

### Herramientas de compilación por línea de comandos

- **Pandoc:** El conversor universal de documentos más potente (requiere instalación independiente).
- **Node.js (CLI tools):** Herramientas como `marked-cli` o `markdown-it`.
- **Python:** Biblioteca `markdown` accesible vía terminal.

### tecnologías concretas

Se usan las siguientes tecnologías:

- [MkDocs](https://www.mkdocs.org/)
- [Material para MkDocs](https://squidfunk.github.io/mkdocs-material/)

### Para ejecutar la web en local:

1. Tienes que instalar dos herramientas si no las tienes. Si las tienes, ve al siguiente paso (como en los libros de [Dragones y Mazmorras](https://www.ddo.com/home)).

- Necesitas instalar [`python`](https://www.python.org/) y `pip` (que normalmente se instala con python).
- Instalas `pip`:

```
pip install mkdocs
pip install mkdocs-material
```

2. Descargas este repositorio, lo descomprimes, y abres un terminal (ventana de comandos) en la carpeta raiz que acabas de descomprimir, y ejecutas:

```
mkdocs build //para construir el proyecto
mkdocs serve //para servirlo en el servidor local
```

Con esto, tendrás la página de documentación lista para acceder en modo local (127.0.0.1/8000). Aunque también puedes

3. Desplegar tu página en **github.pages**. Entendemos que tendrás tu proyecto de **markdown** en tu repositorio de github, tendrás que configurar el despliegue en **Settings** del repositorio, y en la ventana de comandos de tu proyecto

```
mkdocs build //para construir el proyecto
mkdocs gh-deploy //para servirlo en el servidor de github pages
```

---

## 2. Sintaxis y Formatos Principales

### Encabezados

\```markdown

# Encabezado 1 (H1)

## Encabezado 2 (H2)

### Encabezado 3 (H3)

#### Encabezado 4 (H4)

\```

Estos encabezados pueden o no llevar numeración

### Formato de Texto

\```markdown
_Texto en cursiva_ o _Texto en cursiva_
**Texto en negrita** o **Texto en negrita**
**_Negrita y cursiva_**
~~Texto tachado~~
\```

### Listas

**Listas no ordenadas:**
\```markdown

- Elemento 1
- Elemento 2
  - Subelemento 2.1

* Elemento alternativo
  \```

Markdown considera un nuevo nivel a partir de 4 espacios.

**Listas ordenadas:**
\```markdown

1. Primer paso
2. Segundo paso
3. Tercer paso
   \```

### Enlaces e Imágenes

\```markdown

<!-- Enlace -->

[Texto del enlace](https://www.ejemplo.com)

<!-- Imagen -->

![Texto alternativo](https://via.placeholder.com/150 "Título opcional")
\```

### Citas (Blockquotes)

\```markdown

> La simplicidad es la clave de la verdadera elegancia.
>
> > Cita anidada
> > \```

### Código

\```markdown
Código en línea: Utiliza `npm start` para ejecutar la aplicación.

Bloque de código con resaltado de sintaxis:

````javascript
function saludar(nombre) {
  console.log(`Hola, ${nombre}`);
}
saludar("Mundo");
```


````

### Tablas

| Nombre |  Rol  |   Estado |
| :----- | :---: | -------: |
| Ana    | Admin |   Activo |
| Carlos | User  | Inactivo |

_(Los puntos `:` determinan la alineación: izquierda `:---`, centro `:---:`, derecha `---:`)_

---

### Separadores Horizontales

```markdown
---
---

---
```
