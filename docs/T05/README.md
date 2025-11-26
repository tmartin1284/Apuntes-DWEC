# **UNIDAD 5 - Gestión de Eventos y Validación de Formularios**

En esta unidad, exploraremos cómo manejar interacciones de los usuarios y validar formularios en una página web.

- **Los eventos** son fundamentales para crear aplicaciones web dinámicas e interactivas. Nos permiten responder a acciones del usuario, como clics, pulsaciones de teclas y envíos de formularios.
- **La validación de formularios** es esencial para asegurar que los datos ingresados por los usuarios cumplan con los criterios requeridos antes de enviarlos al servidor.

Al dominar la gestión de eventos y la validación de formularios, mejorarás la experiencia del usuario y la fiabilidad de tus aplicaciones web.

## **1. Modelos de Gestión de Eventos en JavaScript**

- Los eventos son mecanismos que se activan cuando el usuario realiza un cambio en una página web.
- La entidad responsable de crear la jerarquía de objetos que compone una página web es el DOM (Modelo de Objeto de Documento).
- Por lo tanto, es el DOM el que gestiona los eventos.

### **1.1 Asignar un Manejador de Eventos**

En JavaScript, la gestión de eventos te permite responder a acciones de los usuarios u otros eventos activados en el navegador. Existen diferentes modelos para gestionar eventos, cada uno ofreciendo distintas maneras de adjuntar oyentes de eventos y gestionar la propagación de eventos.

1. **Modelo Tradicional de Eventos (`onclick`, `onmouseover`, etc.)**
     - **Descripción:** Este modelo implica asignar directamente atributos de manejador de eventos a elementos HTML.
     - **Uso:** Adjuntar eventos dentro de etiquetas HTML o configurarlos mediante JavaScript utilizando propiedades de los elementos (`element.onclick = function() {...}`).
     - **Ejemplo:**
     ```html
     <button onclick="alert('¡Botón clicado!')">Haz clic aquí</button>
     ```

2. **Modelo de Eventos Nivel 2 del DOM (método `addEventListener()`)**
     - **Descripción:** Introducido en el Nivel 2 del DOM, este modelo ofrece un enfoque más flexible para la gestión de eventos.
     - **Uso:** Adjuntar eventos utilizando `addEventListener(event, handler, useCapture)`, donde `event` es el tipo de evento (por ejemplo, `'click'`), `handler` es la función a ejecutar, y `useCapture` (opcional) especifica el flujo del evento.
     - **Ejemplo:**
     ```javascript
     const boton = document.querySelector('button');
     boton.addEventListener('click', function() {
       alert('¡Botón clicado usando addEventListener!');
     });
     ```

3. **Delegación de Eventos**
     - **Descripción:** En lugar de adjuntar oyentes de eventos a elementos individuales, esta técnica implica adjuntar un solo oyente de eventos a un elemento padre.
     - **Uso:** Utilizar la burbuja de eventos colocando oyentes de eventos en elementos padres y delegar el manejo en función del elemento objetivo (`event.target`).
     - **Ejemplo:**
     ```html
     <ul id="lista">
       <li>Elemento 1</li>
       <li>Elemento 2</li>
       <li>Elemento 3</li>
     </ul>

     <script>
       const lista = document.getElementById('lista');
       lista.addEventListener('click', function(evento) {
         if (evento.target.tagName === 'LI') {
           console.log('Clic en:', evento.target.textContent);
         }
       });
     </script>
     ```

## **2. Tipos de Eventos en JavaScript**

JavaScript ofrece una gran variedad de eventos que se pueden utilizar para interactuar con las páginas web. Estos eventos se pueden clasificar en diferentes categorías según su naturaleza y los elementos a los que están asociados.

#### Categorías de Eventos
1. Eventos de Ratón
2. Eventos de Teclado
3. Eventos de Formularios
4. Eventos del Documento
5. Eventos del Portapapeles
6. Eventos de Arrastrar y Soltar
7. Eventos de Pantalla Táctil

### 2.1 **Eventos de Ratón**
Los eventos de ratón se activan por acciones del usuario con el ratón.

- **click**: Se dispara cuando el usuario hace clic en un elemento.
- **dblclick**: Se dispara cuando el usuario hace doble clic en un elemento.
- **mousedown**: Se dispara cuando el usuario presiona un botón del ratón sobre un elemento.
- **mouseup**: Se dispara cuando el usuario suelta un botón del ratón sobre un elemento.
- **mousemove**: Se dispara cuando el usuario mueve el puntero del ratón sobre un elemento.
- **mouseover**: Se dispara cuando el usuario mueve el puntero del ratón sobre un elemento.
- **mouseout**: Se dispara cuando el usuario mueve el puntero del ratón fuera de un elemento.

### 2.2 **Eventos de Teclado**
Los eventos de teclado se activan por acciones del usuario con el teclado.

- **keydown**: Se dispara cuando el usuario presiona una tecla.
- **keyup**: Se dispara cuando el usuario suelta una tecla.
- <strike>**keypress**</strike>: Se disparaba cuando el usuario presionaba una tecla (obsoleto, usar `keydown` en su lugar).

Cuando una tecla se presiona y se mantiene pulsada, comienza a repetirse automáticamente: `keydown` se dispara repetidamente, y cuando la tecla finalmente se suelta, se desencadena un solo evento `keyup`. Por lo tanto, es normal tener muchos eventos `keydown` y solo uno `keyup`.

<div class="exercise-box">
    <h3><i class="fas fa-laptop-code"></i> Ejercicio Práctico: Gestión de Eventos de Teclado</h3>
    <p>Crea una página HTML simple con JavaScript que permita al usuario controlar un personaje usando las teclas de flecha.</p>
    <ol>
        <li><strong>Estructura HTML:</strong> Crea un archivo HTML (`index.html`) con un elemento `div` para representar el personaje.</li>
        <li><strong>Estilo CSS:</strong> Estiliza el personaje (`#personaje`) para que sea visible y esté posicionado en la pantalla.</li>
        <li><strong>Funcionalidad JavaScript:</strong> Implementa código JavaScript para manejar eventos `keydown` de las teclas de flecha y mover el personaje en consecuencia.</li>
        <li><strong>Gestión de Eventos:</strong> Adjunta un oyente de eventos al objeto `document` para capturar las pulsaciones de las teclas de flecha y actualizar la posición del personaje.</li>
    </ol>
    <p><strong>Objetivo:</strong> Mover el personaje suavemente en la pantalla usando las teclas de flecha.</p>
    <p><strong>Instrucciones:</strong></p>
    <ul>
        <li>Abre `index.html` en un navegador web.</li>
        <li>Usa las teclas de flecha (`arriba`, `abajo`, `izquierda`, `derecha`) para controlar el movimiento del personaje.</li>
        <li>Observa cómo el personaje actualiza su posición en respuesta a cada pulsación de tecla.</li>
    </ul>
    <p><strong>Explicación:</strong> Este ejercicio demuestra los fundamentos de la gestión de eventos de teclado en JavaScript para crear aplicaciones web interactivas.</p>
</div>

Ejemplo de HTML para el ejercicio:

```js
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ejercicio Simple de Eventos de Teclado</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
    }
    #personaje {
      position: relative;
      width: 50px;
      height: 50px;
      background-color: blue;
      margin-top: 20px;
      transition: 0.2s ease-out;
    }
  </style>
</head>
<body>
  <h2>Mueve el Personaje con las Teclas de Flecha</h2>
  <div id="personaje"></div>

  <script>
    // Código JavaScript irá aquí
    const personaje = document.getElementById('personaje');
    let posX = 0;
    let posY = 0;
  </script>
</body>
</html>
```

### 2.3 **Eventos de Formularios**
Los eventos de formularios están relacionados con los elementos del formulario.

- **submit**: Se dispara cuando se envía un formulario.
- **reset**: Se dispara cuando se restablece un formulario.
- **change**: Se dispara cuando cambia el valor de un elemento (para `<input>`, `<textarea>`, `<select>`).
- **focus**: Se dispara cuando un elemento gana el foco.
- **blur**: Se dispara cuando un elemento pierde el foco.
- **input**: Se dispara cuando el usuario introduce texto en un elemento.

### 2.4 **Eventos del Documento**
Los eventos del documento se activan por acciones que afectan al documento en su totalidad.

- **DOMContentLoaded**: Se dispara cuando el documento HTML inicial ha sido completamente cargado y analizado.
```js
document.addEventListener('DOMContentLoaded', (event) => {
    console.log('El DOM está completamente cargado y analizado');
});
```
- **DOMSubtreeModified**: Se activa cuando se agregan o eliminan nodos del subárbol de un elemento o del documento.
- **DOMNodeInserted**: Ocurre cuando un nuevo nodo hijo es agregado a un nodo padre.
- **DOMNodeRemoved**: Ocurre cuando un nodo con un nodo padre es eliminado.

### 2.5 **Eventos de la Ventana**
- **load**: Se dispara cuando toda la página (ventana) y todos los recursos dependientes han terminado de cargarse.
```js
window.addEventListener('load', (event) => {
    console.log('La página está completamente cargada');
});
```

>El evento `load` de `window` y el evento `DOMContentLoaded` de `document` se pueden utilizar para fines similares, actuando como un "método principal" en el que podemos asegurarnos de que el código dentro de ellos se ejecute una vez que la página esté cargada, con algunas diferencias:
>
> - **DOMContentLoaded**: Se dispara una vez que el árbol del DOM está completamente construido.
> - **load**: Se dispara una vez que todos los recursos de la página, incluyendo multimedia, están completamente cargados.
> Es una buena práctica colocar el código que queremos ejecutar dentro de una función controladora para uno de estos eventos. Sin embargo, si el script se carga al final del `body`, al menos podemos asegurar que todo el DOM esté cargado.

- **unload**: Se dispara cuando toda la página (ventana) o un recurso hijo está siendo descargado.
- **resize**: Se dispara cuando la vista del documento (ventana) es redimensionada.
- **scroll**: Se dispara cuando la vista del documento (ventana) es desplazada.

### 2.6 **Eventos de Arrastrar y Soltar**
Los eventos de arrastrar y soltar se utilizan para mover elementos arrastrándolos.

- **drag**: Se dispara cuando un elemento está siendo arrastrado.
- **dragstart**: Se dispara cuando el usuario comienza a arrastrar un elemento.
- **dragend**: Se dispara cuando el usuario termina de arrastrar un elemento.
- **dragenter**: Se dispara cuando un elemento arrastrado entra en un objetivo de colocación válido.
- **dragover**: Se dispara cuando un elemento es arrastrado sobre un objetivo de colocación válido.
- **dragleave**: Se dispara cuando un elemento arrastrado sale de un objetivo de colocación válido.
- **drop**: Se dispara cuando un elemento arrastrado es soltado sobre un objetivo de colocación válido.

## 3. **Formularios HTML**

- Un formulario web se utiliza para enviar, procesar y recuperar datos que se envían y reciben entre un cliente y un servidor web.
- Cada elemento del formulario almacena un tipo de dato o activa alguna de sus funcionalidades.
- Los formularios tienen una arquitectura definida dentro del contexto del lenguaje HTML.

### 3.1 **Estructura del Formulario**

- Los formularios se definen utilizando etiquetas.
- La etiqueta principal es [**`<form> </form>`**](https://developer.mozilla.org/es/docs/Web/HTML/Element/form).
- Para ser funcional, la etiqueta `<form>` necesita inicializar dos atributos:
  - `action` – Contiene la URL donde se redirige la información del formulario.
  - `method` – Indica el método por el cual el formulario envía datos. Puede ser POST o GET.

### 3.2 **Etiquetas del Formulario**

#### 1. **[`<input>`](https://developer.mozilla.org/es/docs/Web/HTML/Element/input)**

La etiqueta `<input>` es un elemento fundamental de HTML que se utiliza dentro de los formularios para recopilar entradas del usuario. Es versátil y admite varios tipos (atributo `type`), cada uno diseñado para necesidades específicas de entrada de datos. Los tipos de entrada más comunes incluyen campos de texto, casillas de verificación, botones de opción, controles de carga de archivos y más. La etiqueta `<input>` no tiene una etiqueta de cierre y es autoconclusiva con atributos que controlan su apariencia, comportamiento e interacción con el usuario.

##### Atributos de Entrada:

**type**: Especifica el tipo de elemento que se está definiendo. Este atributo determina los parámetros adicionales. Los valores posibles para el atributo `type` incluyen:

- `text`: Campo de entrada de texto.
- `password`: Campo de entrada de contraseña, donde los caracteres están ocultos (normalmente se muestran como asteriscos).
- `checkbox`: Casilla de verificación para selección múltiple.
- `radio`: Botón de opción para selección exclusiva entre dos o más opciones.
- `submit`: Botón para enviar el formulario.
- `reset`: Botón para restablecer o borrar los campos del formulario.
- `button`: Botón genérico dentro del formulario.
- `file`: Botón para buscar y seleccionar archivos.
- `hidden`: Campo oculto no visible para el usuario en el formulario.
- `image`: Botón de imagen dentro del formulario.

##### Más tipos de entrada en HTML5:

- `email`: Obliga al usuario a introducir una dirección de correo electrónico válida.
- `search`: Estilizado para cajas de búsqueda, proporcionando pistas visuales adecuadas.
- `tel`: Permite la entrada de un número de teléfono (en dispositivos móviles, activa un teclado numérico, pero no restringe la entrada solo a números).
- `url`: Impone restricciones de entrada para garantizar que el texto siga el formato de una URL.
- `number`: Permite la entrada de solo números de punto flotante. Se pueden aplicar restricciones de rango.
- `range`: Crea un control deslizante gráfico para seleccionar un rango numérico.
- `date/time inputs` (Nota: no todos los navegadores los soportan):
  - `datetime-local`
  - `month`
  - `week`
  - `time`
- `color`: Proporciona un control de selección de color.

Consulta --> [https://developer.mozilla.org/es/docs/Learn/Forms/HTML5_input_types](https://developer.mozilla.org/es/docs/Learn/Forms/HTML5_input_types)

##### Más Atributos para Input:

- **name**: Especifica el nombre utilizado para pasar el valor de la variable al servidor.
- **value**: Indica el valor inicial de la entrada en el formulario. Se puede establecer inicialmente y acceder a él para leerlo o validarlo. El tipo de dato depende del tipo de entrada.
- **size**: Especifica el tamaño del elemento en píxeles. Para los campos de texto y contraseña, se refiere al número de caracteres.
- **maxlength**: Especifica el número máximo de caracteres que se pueden introducir en un campo de texto o contraseña.
- **checked**: Exclusivo para elementos de casilla de verificación y botón de opción. Indica qué opción está seleccionada.
- **disabled**: Deshabilita el elemento, impidiendo que su valor se envíe al servidor.
- **readonly**: Hace que el contenido del elemento no sea editable.
- **src**: Especifica la ruta de una imagen utilizada como botón dentro del formulario.
- **alt**: Proporciona texto alternativo para la imagen.
- **placeholder**: Texto que aparece como sugerencia en el campo de entrada antes de que el usuario lo enfoque.
- **autofocus**: Especifica que el elemento debe tener el foco automáticamente cuando la página se carga.

Consulta --> [https://developer.mozilla.org/es/docs/Learn/Forms/Basic_native_form_controls](https://developer.mozilla.org/es/docs/Learn/Forms/Basic_native_form_controls)

#### 2. [**`<label>`**](https://developer.mozilla.org/es/docs/Web/HTML/Element/label): Asocia una etiqueta con un `<input>`, `<select>`, `<textarea>` o `<button>`, proporcionando orientación al usuario. Usa el atributo `for` para coincidir con el `id` del control relacionado.

#### 3. [**`<select>`**](https://developer.mozilla.org/es/docs/Web/HTML/Element/select): Crea una lista desplegable para seleccionar opciones. Usa etiquetas `<option>` anidadas para definir las opciones.

#### 4. [**`<textarea>`**](https://developer.mozilla.org/es/docs/Web/HTML/Element/textarea): Permite la entrada de texto en varias líneas. Útil para respuestas largas como comentarios o mensajes.

#### 5. [**`<button>`**](https://developer.mozilla.org/es/docs/Web/HTML/Element/button): Crea un botón clicable dentro de un formulario. El atributo `type` (`submit`, `reset` o `button`) define el comportamiento.

#### 6. [**`<fieldset>` y `<legend>`**](https://developer.mozilla.org/es/docs/Web/HTML/Element/fieldset): Agrupa controles de formulario relacionados (`<input>`, `<select>`, etc.). `<legend>` proporciona un título para el grupo.

### 3.3 **Estilo de Formularios**

Podemos estilizar manualmente los formularios usando CSS para que se vean mejor. Aquí hay algunos aspectos clave a considerar:

- Cambiar el estilo de los botones (los navegadores diferentes los muestran de manera diferente).
- Usar las fuentes y colores de nuestro sitio web.
- Distribuir adecuadamente los elementos del formulario en la pantalla.
- Usar CSS para distinguir los campos erróneos durante la validación, por ejemplo, cambiando el borde a rojo o mostrando mensajes de error ocultos.

Para agregar o quitar clases CSS usando JavaScript, podemos usar `element.classList.add("clase")`.

También podemos usar bibliotecas como Bootstrap, donde los elementos del formulario ya están definidos.

#### 1. Estilo Manual con CSS

##### Estilo de Botones

Podemos cambiar el estilo de los botones para asegurarnos de que se vean consistentes en todos los navegadores:

```css
button {
    background-color: #4CAF50; /* Verde */
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
    border-radius: 4px;
}

button:hover {
    background-color: #45a049;
}
```

##### Usando Fuentes y Colores del Sitio

Podemos usar fuentes y colores específicos de nuestro sitio web:

```css
body {
    font-family: 'Arial', sans-serif;
    background-color: #f2f2f2;
    color: #333;
}

input, select, textarea {
    font-family: inherit;
    font-size: 16px;
    padding: 10px;
    margin: 10px 0;
    box-sizing: border-box;
}

label {
    font-weight: bold;
}
```

##### Distribuyendo Elementos del Formulario en la Pantalla

Podemos usar un contenedor para centrar el formulario y distribuir sus elementos:

```css
.form-container {
    max-width: 500px;
    margin: auto;
    background: white;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
```

Para organizar los formularios y aplicar estilos de manera efectiva, es una buena idea agrupar elementos usando `fieldset` o `div` con una clase que ayude en el estilo. Por ejemplo, usar una clase como `form-group` puede ayudar a aplicar estilos consistentes a los elementos agrupados.

```html
<div class="form-group">
    <label for="name">Nombre:</label>
    <input type="text" name="name" id="name" autofocus>
</div>
```

```css
.form-group {
  margin-bottom: 1em;
}

.form-group label {
    display: block;
    margin-bottom: 5px;
}

.form-group>input,
.form-group>textarea,
.form-group>select {
  display: block;
  width: 100%;
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #ccc;
  font-family: inherit;
  font-size: 16px;
  box-sizing: border-box;
}

.form-group>input[type="checkbox"] {
  display: inline-block;
  width: auto;
}
```

#### 2. Campos Erróneos

Podemos resaltar los campos erróneos y mostrar mensajes de error:

```css
input.error, select.error, textarea.error {
    border-color: red;
}

.error-message {
    color: red;
    font-size: 12px;
    display: none;
}

.error-message.active {
    display: block;
}
```

Podemos usar JavaScript para agregar o quitar clases CSS:

```js
document.getElementById('myInput').classList.add('error');
document.getElementById('myErrorMessage').classList.add('active');
```

#### 3. Usando Bibliotecas como Bootstrap

Bootstrap proporciona clases predefinidas para formularios:

```html
<form>
  <div class="mb-3">
    <label for="exampleInputEmail1" class="form-label">Dirección de correo electrónico</label>
    <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
    <div id="emailHelp" class="form-text">Nunca compartiremos tu correo electrónico con nadie más.</div>
  </div>
  <div class="mb-3">
    <label for="exampleInputPassword1" class="form-label">Contraseña</label>
    <input type="password" class="form-control" id="exampleInputPassword1">
  </div>
  <div class="mb-3 form-check">
    <input type="checkbox" class="form-check-input" id="exampleCheck1">
    <label class="form-check-label" for="exampleCheck1">Marcarme</label>
  </div>
  <button type="submit" class="btn btn-primary">Enviar</button>
</form>
```

Consulta más información sobre [Formularios de Bootstrap](https://getbootstrap.com/docs/5.0/forms/overview/)

## 4. **Validación de Formularios**

La validación de formularios es crucial para asegurar que las entradas del usuario sean correctas y completas antes de la presentación. Esto se puede lograr a través de varios métodos, incluyendo la validación del lado del cliente con atributos HTML5, validación con JavaScript y validación del lado del servidor.

<div class="important-box">
<h3><i class="fa-solid fa-circle-exclamation"></i>IMPORTANTE</h3>
<p>La validación del lado del cliente mejora la usabilidad de un sitio web, pero no elimina la necesidad de validación del lado del servidor.</p>
</div>

### 4.1 **Validación con JavaScript Vanilla**

La validación se puede realizar de muchas maneras, pero es aconsejable hacerlo de manera organizada usando funciones que podamos reutilizar más tarde. Proponemos esta solución:

##### Formulario a validar

```html
<form id="contactForm" class="needs-validation">
    <div class="form-group">
        <label for="name">Nombre</label>
        <input type="text" class="form-control" id="name" name="name">
        <div class="error-message">El nombre es obligatorio y debe tener al menos 2 caracteres.</div>
    </div>
    <div class="form-group">
        <label for="email">Correo electrónico</label>
        <input type="email" class="form-control" id="email" name="email">
        <div class="error-message">Por favor, proporciona una dirección de correo electrónico válida.</div>
    </div>
    <div class="form-group">
        <label for="password">Contraseña</label>
        <input type="password" class="form-control" id="password" name="password">
        <div class="error-message">La contraseña es obligatoria y debe tener al menos 6 caracteres.</div>
    </div>
    <button type="submit" class="btn btn-primary">Enviar</button>
</form>
```

##### Función de Validación Principal

Se recomienda que todo el código esté dentro del evento `DOMContentLoaded` o `load` de la ventana. Esto asegura que todo el documento esté cargado antes de comenzar a ejecutar el código.


```js
// Es una buena práctica que todo el código esté dentro del evento 'DOMContentLoaded' o 'load' 
document.addEventListener('DOMContentLoaded', function () {
  // Capturar todos los elementos 
  const form = document.getElementById('contactForm');
  const name = document.getElementById('name');
  const email = document.getElementById('email');
  const password = document.getElementById('password');

  // Crear el manejador del evento para el envío del formulario ('submit')
  form.addEventListener('submit', function (event) {
    event.preventDefault(); // Evita que el formulario se envíe automáticamente
    event.stopPropagation(); // Evita que el evento se propague a elementos padre

    // Llamar a la función principal de validación 
    if (validateForm()) {
      console.log("Todos los campos están bien, podemos proceder");
      form.submit();  // Forzar el envío
    } else {
      console.log("Hay algún campo no válido. El usuario debe revisarlos.")
    }
  });

  // Esta función se encarga de validar todos los campos y 
  // devolver un booleano: true si todos los campos están bien, false en caso contrario
  function validateForm() {
    // Esta bandera se inicializa como true.
    // En caso de encontrar un error en un campo, esta variable se convierte en false.
    var isValid = true;

    // Lógica de validación personalizada
    // Ejemplo de validación personalizada solo comprobando la longitud 
    if (name.value.trim().length < 2) {
      markFieldAsNotValid(name);
      isValid = false;
    } else {
      markFieldAsValid(name);
    }

    // Podemos llamar a funciones personalizadas de validación de campos 
    // también podemos comprobar diferentes condiciones y mostrar diferentes mensajes de error
    if (email.value === "") {
      markFieldAsNotValid(email, "El correo electrónico es obligatorio");
      isValid = false;
    } else if (!isValidEmail(email.value)) {
      markFieldAsNotValid(email, "Por favor, proporciona una dirección de correo válida.");
      isValid = false;
    } else {
      markFieldAsValid(email);
    }

    if (!isValidPassword(password.value)) {
      markFieldAsNotValid(password);
      isValid = false;
    } else {
      markFieldAsValid(password);
    }

    // Después de validar todos los campos, devolvemos el valor de la bandera isValid
    return isValid;
  }

  // Definición de las funciones de validación de campos y otras funciones auxiliares
  // ....

}
```

##### Funciones de validación de campos específicos
  Cuando la validación es más compleja, podemos definir funciones que validen ciertos campos.

```js
function isValidEmail(email) {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
}

function isValidPassword(passwd) {
  return (passwd.length >= 6);
}

```
##### Funciones auxiliares para gestionar mensajes de error
 Podemos crear funciones que gestionen los mensajes de error. En este caso, hemos creado una para mostrar el error y otra para ocultarlo. Funcionan sobre el elemento que pasamos a la función. El código navega hacia el elemento padre para agregar o eliminar la clase is-not-valid-field.

```js
// Esta función marca un campo como no válido y añade el mensaje de error
function markFieldAsNotValid(element, message) {
  // Si tenemos un mensaje personalizado, lo mostramos. En caso contrario, mostramos el mensaje de error presente en el HTML
  if (message) {
    element.parentNode.querySelector(".error-message").textContent = message;
  }
  // Añadiendo la clase que muestra el mensaje de error y añade el borde rojo (css)
  element.parentNode.classList.add("is-not-valid-field");
}

// Esta función marca un campo como válido y oculta el mensaje de error
function markFieldAsValid(element) {
  element.parentNode.classList.remove("is-not-valid-field");
}

```
Recordemos la estructura de un elemento form-group:


```js
<div class="form-group">
    <label for="name">Nombre</label>
    <input type="text" class="form-control" id="name" name="name">
    <div class="error-message">El nombre es obligatorio y debe tener al menos 2 caracteres de longitud.</div>
</div>
```


##### CSS para Manejar Errores

Necesitamos algo de CSS para hacer visibles los mensajes de error y el borde rojo cuando la clase `is-not-valid-field` está presente en el elemento `form-group`.

```css
.form-group.is-not-valid-field input,
.form-group.is-not-valid-field select,
.form-group.is-not-valid-field textarea {
  border-color: red;
}

.error-message {
  color: red;
  font-size: 12px;
  display: none;
}

.is-not-valid-field .error-message {
  display: block;
}
```

![Vanilla js Validation](img/vanilla-validation.png)

<div class="exercise-box">
    <h3><i class="fas fa-laptop-code"></i> Ejercicio Práctico</h3>
    <p>Agrega tres nuevos campos al formulario existente:</p>
    <ul>
        <li>Un campo de confirmación de contraseña que debe coincidir con el campo de contraseña original.</li>
        <li>Un campo de fecha de nacimiento. Asegúrate de que el usuario tenga al menos 18 años.</li>
        <li>Una casilla de verificación para aceptar las condiciones. El formulario no debe enviarse a menos que esta casilla esté marcada.</li>
    </ul>
    <p>Implementa la lógica de validación para estos campos usando JavaScript vanilla. Asegúrate de que se muestren mensajes de error apropiados para entradas no válidas.</p>
    <p>Investiga diferentes frameworks y selecciona uno que usarías para construir una Aplicación de Página Única (SPA). Indica las razones que te convencieron.</p>
</div>



### 4.2 **Validación nativa con HTML5**

HTML5 permite la validación nativa de formularios utilizando atributos específicos en elementos de formulario como `<input>`, `<textarea>` y `<select>`. Esta validación integrada asegura que un formulario no se envíe hasta que se cumplan todos los requisitos especificados por estos atributos. Cuando se encuentra un campo inválido, se proporciona retroalimentación sobre el primer problema encontrado.

#### Atributos clave de validación en HTML5

- `required`: Asegura que el campo no quede vacío.
- `minlength` y `maxlength`: Establecen el número mínimo y máximo de caracteres permitidos.
- `min` y `max`: Definen los valores mínimo y máximo para entradas numéricas.
- `pattern`: Valida la entrada contra una expresión regular especificada.
- `type`: Especifica el tipo de dato esperado (por ejemplo, `email`, `number`, `url`).
- `step`: Define los intervalos numéricos legales para entradas numéricas.

Aunque la validación HTML5 es sencilla y no requiere JavaScript, tiene limitaciones. La principal desventaja es la falta de control sobre el proceso de validación y la visualización de retroalimentación. Solo se resalta el primer campo inválido y la personalización de los mensajes de error es limitada.

#### Ejemplos

```html
<form>
    <label for="username">Nombre de usuario:</label>
    <input type="text" id="username" name="username" required minlength="3" maxlength="15">
    
    <label for="email">Correo electrónico:</label>
    <input type="email" id="email" name="email" required>
    
    <label for="age">Edad:</label>
    <input type="number" id="age" name="age" min="18" max="99" required>
    
    <label for="website">Sitio web:</label>
    <input type="url" id="website" name="website" pattern="https?://.+">
    
    <button type="submit">Enviar</button>
</form>
```

### 4.3 **Validación HTML5 con Bootstrap 5**

Bootstrap 5 proporciona estilos y clases que mejoran la validación de formularios HTML5, facilitando la creación de formularios visualmente atractivos y amigables para el usuario. Al combinar los atributos de validación HTML5 con las clases de Bootstrap, podemos ofrecer retroalimentación inmediata a los usuarios de manera más pulida.

#### Clases clave de Bootstrap 5 para validación

- `.needs-validation`: Aplicada al elemento del formulario para habilitar los estilos de validación.
- `.was-validated`: Agregada al formulario después de la presentación para activar la retroalimentación de validación.
- `.is-valid` y `.is-invalid`: Aplicadas a los campos de entrada para mostrar el estado de validación.
- `.valid-feedback` y `.invalid-feedback`: Usadas para mostrar mensajes de validación personalizados.

Consulta el ejemplo en el repositorio de Materiales DWEC. --> [06-html5-bootstrap-validation.html](https://github.com/jeatzr/dwec-materials/blob/main/05-events-forms/forms/06-html5-bootstrap-validation.html)

### 4.4 **Validación híbrida**

Combinar la validación HTML5 con la validación personalizada de JavaScript permite una validación de formularios más flexible y completa. Este enfoque híbrido asegura que las validaciones básicas sean manejadas por HTML5 mientras que los requisitos más complejos o específicos se gestionen con JavaScript.

Echa un vistazo al ejemplo --> [Validación Híbrida con Vanilla JS y Bootstrap](https://github.com/jeatzr/dwec-materials/blob/main/05-events-forms/forms/07-hybrid-validation-bootstrap-vanillajs.html)

### 4.5 **Validación utilizando bibliotecas JS**

## 5. **Expresiones regulares (regex)**

Las expresiones regulares, o regex, son patrones utilizados para coincidir combinaciones de caracteres en cadenas. En JavaScript, el regex se implementa utilizando el objeto [`RegExp`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions) o a través de literales de regex.

#### Creando una expresión regular

1. **Usando literales de regex**:
   ```javascript
   const regex = /patrón/bandera;
   ```
2. **Usando el constructor RegExp**:
   ```js
   const regex = new RegExp('patrón', 'bandera');
   ```

#### Banderas comúnmente utilizadas

- `g`: Búsqueda global (encontrar todas las coincidencias)
- `i`: Búsqueda sin distinguir entre mayúsculas y minúsculas
- `m`: Búsqueda en múltiples líneas

En nuestro caso, la más útil es la bandera `i`.

#### Sintaxis básica

- `^`: Coincide con el comienzo de la cadena.
- `$`: Coincide con el final de la cadena.
- `.`: Coincide con cualquier carácter excepto nueva línea.
- `*`: Coincide con 0 o más repeticiones del elemento anterior.
- `+`: Coincide con 1 o más repeticiones del elemento anterior.
- `?`: Coincide con 0 o 1 repetición del elemento anterior.
- `{n}`: Coincide exactamente con n repeticiones del elemento anterior.
- `{n,}`: Coincide con n o más repeticiones del elemento anterior.
- `{n,m}`: Coincide entre n y m repeticiones del elemento anterior.
- `[abc]`: Coincide con cualquiera de los caracteres a, b o c.
- `[^abc]`: Coincide con cualquier carácter excepto a, b o c.
- `(abc)`: Coincide con la secuencia exacta abc.
- `\d`: Coincide con cualquier dígito (equivalente a `[0-9]`).
- `\D`: Coincide con cualquier carácter que no sea un dígito (equivalente a `[^0-9]`).
- `\w`: Coincide con cualquier carácter alfanumérico incluyendo el guion bajo (equivalente a `[A-Za-z0-9_]`).
- `\W`: Coincide con cualquier carácter no alfanumérico (equivalente a `[^A-Za-z0-9_]`).
- `\s`: Coincide con cualquier carácter de espacio en blanco (espacio, tabulación, nueva línea).
- `\S`: Coincide con cualquier carácter que no sea un espacio en blanco.

#### Ejemplo de uso

1. **Probando un patrón**:
    ```js
    const regex = /hola/i;
    const str = "¡Hola Mundo!";
    console.log(regex.test(str)); // true
    ```

2. **Coincidencia de un patrón**:
    ```js
    const regex = /\d+/g;
    const str = "Hay 123 manzanas y 456 naranjas.";
    console.log(str.match(regex)); // ["123", "456"]
    ```

3. **Reemplazo con un patrón**:
    ```js
    const regex = /manzanas/gi;
    const str = "Las manzanas son dulces. Me gustan las manzanas.";
    const newStr = str.replace(regex, "naranjas");
    console.log(newStr); // "Las naranjas son dulces. Me gustan las naranjas."
    ```

#### Ejemplos de regex

En nuestro caso, lo más típico es hacer que el regex coincida completamente con el campo del formulario, por lo que la mayoría de las veces debemos comenzar con `^` y terminar con `$` en el regex.

```js
// Entero básico
const basicIntRegex = /^\d+$/;
// Entero sin signo (0 no incluido)
const intRegex = /^[1-9]\d*$/;
// Entero con signo
const signIntRegex = /^[-+]?\d+$/;
// Código Postal (España)
const cpRegex  = /^[0-5][0-9]{4}$/;
const cpRegexcompleto =  /^[0[1-9]|[0-4][0-9]|5[0-2]][0-9]{4}$/;
// Correo electrónico 99.9% preciso
const emailRegex = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/

```

#### Recursos

- Crea y prueba regex en varios lenguajes: [https://regex101.com/](https://regex101.com/)
- Regex de direcciones de correo electrónico: [https://emailregex.com/](https://emailregex.com/)
- La IA también es excelente para encontrar regex, ¡pero no olvides probarlos!

![Meme de Regex](img/regex-meme.webp)

#### Cómo validar con regex

Podemos validar campos utilizando las funciones `test` o `match`:

```js

function isValidCP (cp){
  // Código Postal (España)
  const cpRegex  = /^[0-5][0-9]{5}$/;
  // Usando la función test del regex
  if(cpRegex.test(cp)){
    return true;
  }else{
    return false
  }
}

function isValidCP2 (cp){
  // Código Postal

 (España)
  const cpRegex  = /^[0-5][0-9]{5}$/;
  // Usando la función match de la cadena
  if(cp.match(cpRegex)){
    return true;
  }else{
    return false
  }
}

```

Las expresiones regulares son herramientas poderosas para la coincidencia de patrones y la manipulación de texto. Pueden ser complejas, pero con práctica, te resultarán increíblemente útiles para diversas tareas en JavaScript.