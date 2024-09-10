Aquí tienes la traducción al español del texto:

---

# **UNIDAD4 - Manipulación del DOM**

## **1. Modelo de Objetos del Documento (DOM)**

El DOM (Modelo de Objetos del Documento) es un estándar del W3C que define cómo acceder a documentos como HTML y XML. Es una interfaz de programación de aplicaciones (API) de la plataforma W3C que permite a los scripts acceder y actualizar dinámicamente el contenido, la estructura y el estilo de un documento.

- **Estándar**: El DOM es un estándar mantenido por el World Wide Web Consortium (W3C) que proporciona una representación estructurada de un documento.
- **API**: Sirve como una interfaz para la programación, permitiendo a los desarrolladores manipular la estructura, el estilo y el contenido del documento a través de lenguajes de scripting como JavaScript.
- **Actualizaciones Dinámicas**: Con el DOM, los scripts pueden modificar dinámicamente el contenido, la estructura y el estilo del documento, permitiendo aplicaciones web interactivas y reactivas.

Aquí tienes un ejemplo simple de cómo podrías usar el DOM para cambiar dinámicamente el contenido de un elemento HTML:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ejemplo de DOM</title>
</head>
<body>
    <h1 id="title">¡Hola, Mundo!</h1>
    <button onclick="changeTitle()">Cambiar Título</button>

    <script>
        function changeTitle() {
            // Accede al elemento DOM con el id 'title'
            const titleElement = document.getElementById('title');
            // Cambia el contenido del elemento
            titleElement.textContent = '¡Hola, DOM!';
        }
    </script>
</body>
</html>
```

### **1.1 Historia del DOM**

- **Web Temprana (1990s)**: La web comenzó con páginas HTML estáticas simples. No había una manera estándar de manipular el contenido o la estructura de estas páginas de manera dinámica.

- **Guerras Netscape e IE**: Netscape Navigator e Internet Explorer (IE) fueron los dos navegadores dominantes. Cada uno desarrolló sus propios métodos para manipular documentos HTML, lo que llevó a problemas de compatibilidad.

- **Introducción de JavaScript (1995)**: Brendan Eich creó JavaScript para Netscape, permitiendo interacciones dinámicas básicas. Sin embargo, el enfoque de Netscape era diferente del de IE. Netscape Navigator 2.0 fue el primer navegador en implementar el denominado **DOM Nivel 0**.

- **Participación del W3C (1998)**: El [World Wide Web Consortium (W3C)](https://www.w3.org) intervino para estandarizar cómo se deberían acceder y manipular los documentos, resultando en la creación del Modelo de Objetos del Documento **(DOM) Nivel 1**.

- **DOM Nivel 1 (1998)**: Se lanzó la primera versión del DOM, proporcionando una manera estandarizada de manipular la estructura y el contenido del documento **a través de diferentes navegadores**.

- **DOM Nivel 2 (2000)**: Introdujo características más avanzadas como **soporte para CSS**, **eventos** y manipulación de documentos XML.

- **DOM Nivel 3 (2004)**: Expansión adicional de la API para incluir más características para la manipulación y navegación de documentos.

- **HTML5 y la Web Moderna (2010s)**: HTML5 trajo actualizaciones significativas al DOM, haciéndolo más robusto y permitiendo aplicaciones web más complejas. Los navegadores modernos han adoptado e implementado estos estándares de manera consistente.

El desarrollo y la estandarización del DOM han sido cruciales para crear la web dinámica e interactiva que conocemos hoy, proporcionando una manera consistente para que los scripts interactúen y modifiquen documentos web a través de diferentes navegadores.

[--> Estándar DOM Nivel 3 por el W3C](https://www.w3.org/DOM/DOMTR)

## **2. Estructura del Árbol DOM**

Un árbol DOM es una estructura de árbol cuyos nodos representan el contenido de un documento HTML o XML. Cada documento HTML o XML tiene una representación en árbol DOM. Por ejemplo, considera el siguiente documento:

```html
<html lang="es">
  <head>
    <title>Mi Título</title>
  </head>
  <body>
    <a href="http://alink.com">Mi Enlace</a>
    <h1>Mi Encabezado</h1>
  </body>
</html>
```

Tiene un árbol DOM que se ve así:

![Árbol DOM](img/dom_tree.png)

Aunque el árbol anterior es similar al árbol DOM del documento, no es idéntico, ya que [el árbol DOM real conserva el espacio en blanco](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Whitespace).

Cuando un navegador web analiza un documento HTML, construye un árbol DOM y luego lo usa para mostrar el documento.

FUENTE: [mdn web docs_](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Using_the_Document_Object_Model)

#### Reglas de Estructura del Árbol:

Para organizar la estructura del árbol, hay una serie de reglas:

- En el árbol de nodos, el nodo superior (documento) se llama **raíz**.
- **Cada nodo**, excepto el nodo raíz, **tiene un padre**.
- Un nodo puede tener **cualquier número de hijos**.
- Una **hoja** es un nodo con **sin hijos**.
- Los nodos que **comparten el mismo padre** son **hermanos**.

### **2.1 La Interfaz Node**

Un **Node** es una interfaz abstracta que representa un solo nodo en el árbol. Estos nodos pueden ser un Documento, un Elemento, un DocumentFragment y más.

- **Documento**: El nodo raíz del documento HTML.
- **DocumentType**: Un nodo que representa el DTD (Definición de Tipo de Documento) de la página.
- **Elemento**: Un nodo que representa un elemento HTML.
- **Attr**: Un nodo que representa un atributo de un elemento.
- **Texto**: Un nodo que almacena el texto contenido dentro de un nodo Elemento.
- **Comentario**: Un nodo que almacena un comentario en el documento HTML.

#### Interfaz Node

- Para manipular la información de los nodos, JavaScript crea un objeto llamado `Node`.
- Este objeto define propiedades y métodos para procesar documentos.
- También define un conjunto de constantes que identifican los tipos de nodos. Estos son los valores que la propiedad `nodeType` puede tener:

| **Constante**                      | **Descripción**                           | **Valor** |
| ---------------------------------- | ----------------------------------------- | --------- |
| `Node.ELEMENT_NODE`                | Representa un nodo de elemento.           | 1         |
| `Node.ATTRIBUTE_NODE`              | Representa un nodo de atributo.           | 2         |
| `Node.TEXT_NODE`                   | Representa un nodo de texto.              | 3         |
| `Node.CDATA_SECTION_NODE`          | Representa un nodo de sección CDATA.      | 4         |
| `Node.ENTITY_REFERENCE_NODE`       | Representa un nodo de referencia de entidad. | 5       |
| `Node.ENTITY_NODE`                 | Representa un nodo de entidad.            | 6         |
| `Node.PROCESSING_INSTRUCTION_NODE` | Representa un nodo de instrucción de procesamiento. | 7 |
| `Node.COMMENT_NODE`                | Representa un nodo de comentario.         | 8         |
| `Node.DOCUMENT_NODE`               | Representa el nodo del documento.         | 9         |
| `Node.DOCUMENT_TYPE_NODE`          | Representa el nodo de tipo de documento.  | 10        |
| `Node.DOCUMENT_FRAGMENT_NODE`      | Representa un nodo de fragmento de documento. | 11    |
| `Node.NOTATION_NODE`               | Representa un nodo de notación.           | 12        |

#### Propiedades y Métodos del Nodo

| **Propiedad/Método**               | **Descripción**                                                                               |
| ---------------------------------- | --------------------------------------------------------------------------------------------- |
| `nodeName`                         | Devuelve el nombre del nodo.                                                                  |
| `nodeType`                         | Devuelve un código entero que representa el tipo de nodo.                                      |
| `nodeValue`                        | Establece o devuelve el valor del nodo. Para nodos de elementos, esto es `null`.               |
| `parentNode`                       | Devuelve el nodo padre del nodo especificado.                                                  |
| `childNodes`                       | Devuelve una NodeList de los nodos hijos del nodo especificado.                                |
| `firstChild`                       | Devuelve el primer nodo hijo del nodo especificado.                                            |
| `lastChild`                        | Devuelve el último nodo hijo del nodo especificado.                                           |
| `previousSibling`                  | Devuelve el nodo hermano anterior del nodo especificado.                                       |
| `nextSibling`                      | Devuelve el nodo hermano siguiente del nodo especificado.                                     |
| `textContent`                      | Establece o devuelve el contenido de texto del nodo y sus descendientes.                      |
| `appendChild(node)`                | Agrega un nuevo nodo hijo al final de la lista de hijos de un nodo padre especificado.          |
| `removeChild(node)`                | Elimina un nodo hijo del

 nodo padre especificado.                                              |
| `replaceChild(newNode, oldNode)`   | Reemplaza un nodo hijo por otro en el nodo padre especificado.                                |
| `cloneNode(deep)`                  | Clona el nodo actual. Si `deep` es `true`, también clona todos los nodos descendientes.      |

Estos métodos y propiedades proporcionan una variedad de maneras para manipular los nodos dentro del árbol DOM, permitiendo una amplia gama de operaciones en la estructura del documento.

