# **UNIDAD 7 - Almacenamiento del Lado del Cliente**

## 1. **Introducción**

El almacenamiento del lado del cliente se refiere a los diversos métodos que permiten a las aplicaciones web almacenar datos en el lado del cliente, dentro del navegador del usuario. Esto permite a las aplicaciones web guardar y recuperar datos sin requerir comunicación constante con el servidor. El almacenamiento del lado del cliente mejora la experiencia del usuario al proporcionar acceso más rápido a los datos y reducir la carga del servidor.

### 1.1 **Usos**

El almacenamiento del lado del cliente se puede utilizar para una variedad de propósitos, incluyendo:

- **Almacenamiento de Preferencias del Usuario**: Guardar configuraciones y preferencias para una experiencia personalizada.
- **Seguimiento**: Registrar y analizar el comportamiento del usuario.
- **Acceso Offline**: Permitir a los usuarios acceder e interactuar con aplicaciones web incluso cuando están desconectados.
- **Gestión de Sesiones**: Mantener información de sesión del usuario para mantener a los usuarios conectados o recordar su progreso en una tarea.
- **Caché de Datos**: Almacenar datos a los que se accede frecuentemente para mejorar el rendimiento y reducir las solicitudes al servidor.
- **Almacenamiento Temporal de Datos**: Mantener datos temporalmente durante la interacción de un usuario con la aplicación web, como entradas de formularios o archivos temporales.

### 1.2 **Métodos**

- **Cookies (método antiguo)**: Pequeñas piezas de datos almacenadas en el navegador y enviadas al servidor con cada solicitud HTTP. Comúnmente utilizadas para la gestión de sesiones y preferencias del usuario.

- **Almacenamiento Local**: Almacenamiento de clave-valor que permite que los datos se almacenen de forma persistente en el navegador sin una fecha de expiración. Ideal para guardar configuraciones y datos de aplicación que no necesitan ser enviados al servidor.

- **Almacenamiento de Sesión**: Similar al Almacenamiento Local, pero los datos solo se almacenan durante la duración de la sesión de la página. Útil para datos temporales que solo necesitan ser accesibles mientras la página está abierta.

- **IndexedDB**: Una base de datos NoSQL que permite almacenar grandes cantidades de datos estructurados. Adecuada para aplicaciones complejas que requieren un almacenamiento local significativo y capacidades offline.

![Comparación de Almacenamiento](img/comparison-table.png)

Fuente de la imagen: [Local Storage vs. Session Storage vs. Cookies @ LoginRadius](https://www.loginradius.com/blog/engineering/guest-post/local-storage-vs-session-storage-vs-cookies/)

## 2. **Cookies**

- Pequeñas piezas de datos almacenadas en el navegador y enviadas al servidor con cada solicitud HTTP.
- Comúnmente utilizadas para la gestión de sesiones, seguimiento de usuarios y preferencias del usuario.
- Ventajas:
    - Envío automático con solicitudes HTTP.
    - Soporte universal en navegadores.
    - Control del servidor sobre la configuración, modificación y eliminación de cookies.
    - Fecha de expiración y alcance configurables.

![Ejemplo de Cookie](img/cookie-basic-example.png)

**Fuente:** [mdn web docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)

### 2.1 **Tipos de Cookies**

- **Cookies de Sesión**:
    - Estas cookies son temporales y se eliminan una vez que se cierra el navegador.
    - Comúnmente utilizadas para almacenar datos de sesión que solo necesitan persistir durante una única sesión de navegación.

- **Cookies Persistentes**:
    - Estas cookies permanecen en el dispositivo del usuario por un período establecido o hasta que se eliminan manualmente.
    - Se utilizan para almacenar preferencias del usuario, información de inicio de sesión y otras configuraciones que necesitan persistir entre sesiones.

### 2.2 **Escritura de Cookies**

Para escribir cookies utilizando JavaScript, puedes usar la propiedad `document.cookie`. Aquí tienes cómo establecer tanto cookies de sesión como persistentes:

#### Establecer una Cookie de Sesión

Las cookies de sesión no tienen una fecha de expiración, por lo que expiran una vez que se cierra el navegador.

```js
document.cookie = "username=JohnDoe";
```

#### Establecer una Cookie Persistente

Las cookies persistentes tienen una fecha de expiración y permanecen en el dispositivo del usuario hasta la fecha especificada o hasta que se eliminan manualmente.

```js
// Establecer una cookie con una fecha de expiración
const now = new Date();
const time = now.getTime();
const expireTime = time + (7 * 24 * 60 * 60 * 1000); // 7 días a partir de ahora
now.setTime(expireTime);

document.cookie = `username=JohnDoe; expires=${now.toUTCString()}; path=/`;
```

#### Parámetros de Cookie

Al establecer cookies, puedes especificar parámetros adicionales:

- **expires**: Establece la fecha de expiración de la cookie.
- **path**: Define la ruta de URL donde la cookie es accesible.
- **domain**: Especifica el dominio para el cual la cookie es válida.
- **secure**: Asegura que la cookie se envíe solo a través de HTTPS.
- **SameSite**: Controla si las cookies se envían con solicitudes entre sitios.

Ejemplo con todos los parámetros:

```js
const now = new Date();
now.setTime(now.getTime() + (30 * 24 * 60 * 60 * 1000)); // 30 días a partir de ahora

document.cookie = "username=JohnDoe; expires=" + now.toUTCString() + "; path=/; domain=example.com; secure; SameSite=Strict";
```

#### Función JavaScript Genérica para Establecer una Cookie

```js
function setCookie(name, value, days = null, path = "/") {
    let cookieString = `${name}=${value}; path=${path};`;
    
    if (days) {
        const date = new Date();
        date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
        const expires = date.toUTCString();
        cookieString += ` expires=${expires};`;
    }
    
    document.cookie = cookieString;
}

// Ejemplos de uso
setCookie("username", "JohnDoe"); // Cookie de sesión
setCookie("username", "JohnDoe", 7); // Cookie persistente por 7 días
setCookie("username", "JohnDoe", 7, "/user"); // Cookie persistente por 7 días con la ruta /user
```

#### Inspeccionar Valores de Cookie

Para inspeccionar los valores de las cookies en Chrome DevTools, sigue estos pasos:

1. Haz clic derecho en la página web y selecciona `Inspeccionar`.
2. Navega a la pestaña `Aplicación`.
3. En la sección `Almacenamiento`, selecciona `Cookies`.
4. Elige el servidor apropiado de la lista.
5. Visualiza las cookies en la sección principal.

![Inspeccionar Cookies](img/cookie-inspect.png)

### 2.2 **Lectura de Cookies**

Puedes leer cookies accediendo a `document.cookie`, que devuelve una cadena que contiene todas las cookies.

```js
const cookies = document.cookie.split("; ");
cookies.forEach(cookie => {
  const [name, value] = cookie.split("=");
  console.log(`${name}: ${value}`);
});
```

Podemos crear una función para leer una cookie específica según su nombre:

```js
function getCookie(name) {
    // Función auxiliar para decodificar el valor de la cookie
    function decodeCookie(value) {
        return decodeURIComponent(value.replace(/\+/g, ' '));
    }

    // Obtener todas las cookies de document.cookie
    const cookies = document.cookie.split('; ').reduce((acc, cookie) => {
        const [cookieName, cookieValue] = cookie.split('=');
        acc[cookieName] = decodeCookie(cookieValue);
        return acc;
    }, {});

    // Encontrar la cookie con el nombre coincidente
    return cookies[name] || null;
}

// Ejemplo de uso
const cookieValue = getCookie('myCookieName');
console.log(cookieValue);
```

**Puntos clave**

1. `document.cookie`: Contiene todas las cookies como una única cadena en el formato `"name1=value1; name2=value2; ..."`.
2. `split('; ')`: Divide esta cadena en cookies individuales.
3. `reduce`: Transforma las cookies en un objeto donde las claves son los nombres de las cookies y los valores son los valores de las cookies.
4. `decodeURIComponent`: Decodifica cualquier carácter especial en los valores de las cookies.



### 2.4 **Borrado de Cookies**

Para eliminar una cookie, establece su fecha de expiración en una fecha pasada.

```js
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC;";
```

Podemos crear una función genérica para borrar una cookie con un nombre dado. 
Esta función utiliza la función `setCookie` con la propiedad `days = -1`, que se refiere a una fecha pasada.

```js
function eraseCookie(name){
  setCookie(name,"",-1)
}
```

## 3. **API de Almacenamiento Web**

`Local storage` y `session storage` son parte de la `API de Almacenamiento Web`, que proporciona formas para que las aplicaciones web almacenen datos localmente en el navegador del usuario. Aunque tienen algunas similitudes, también tienen diferencias distintas:

- **localStorage**: Los datos persisten incluso después de que se cierra el navegador. Se puede acceder a la propiedad de solo lectura [`localStorage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage).
- **sessionStorage**: Los datos almacenados en session storage se borran cuando termina la sesión de la página. Se puede acceder a la propiedad de solo lectura [`sessionStorage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage).

Los métodos para acceder a los elementos de `localStorage` y `sessionStorage` son exactamente los mismos:

**Métodos de `localStorage`**

```js
// Establecer un elemento en local storage
localStorage.setItem("myCenter", "IES Azarquiel");

// Obtener un elemento de local storage
const center = localStorage.getItem("myCenter");

// Eliminar un elemento de local storage
localStorage.removeItem("myCenter");

// Eliminar todos los datos guardados en localStorage
localStorage.clear();
``` 

**Métodos de `sessionStorage`**

```js
// Establecer un elemento en session storage
sessionStorage.setItem("sessionValue", "My Value");

// Obtener un elemento de session storage
const value = sessionStorage.getItem("sessionValue");

// Eliminar un elemento de session storage
sessionStorage.removeItem("sessionValue");

// Eliminar todos los datos guardados en sessionStorage
sessionStorage.clear();
``` 

### 3.1 **Ejemplos de Uso de Local Storage**

#### Almacenamiento de Preferencias del Usuario

Un sitio web puede recordar la configuración del usuario, como el tema (modo oscuro/claro), preferencias de idioma o tamaño de fuente, sin necesidad de una base de datos en el backend.

```js
// Guardar preferencia
localStorage.setItem('theme', 'dark');

// Recuperar preferencia
const theme = localStorage.getItem('theme');
console.log(theme); // Salida: dark
```

#### Guardar Datos de Formularios:

Local storage se puede usar para guardar datos de formularios temporalmente, permitiendo que los usuarios abandonen la página y regresen sin perder su progreso.

```js
// Guardar datos de formulario
localStorage.setItem('formData', JSON.stringify({ name: 'John', email: 'john@example.com' }));

// Recuperar datos de formulario
const formData = JSON.parse(localStorage.getItem('formData'));
console.log(formData); // Salida: { name: 'John', email: 'john@example.com' }
```

#### Almacenamiento en Caché de Respuestas de API:

Para aplicaciones que obtienen datos de APIs, local storage se puede usar para almacenar respuestas en caché y reducir la cantidad de llamadas a la API, mejorando el rendimiento y la experiencia del usuario.

```js
// Guardar respuesta de API
localStorage.setItem('apiResponse', JSON.stringify(responseData));

// Recuperar respuesta de API
const cachedData = JSON.parse(localStorage.getItem('apiResponse'));
console.log(cachedData); // Salida: responseData
```

#### Mantener el Estado a Través de Cargas de Página:

Las aplicaciones web pueden mantener el estado del usuario, como los artículos en un carrito de compras o la última página vista, a través de cargas de página.

```js
// Guardar estado
let appState = [{ id: 1, name: 'Producto A' }, { id: 2, name: 'Producto B' }];
localStorage.setItem('cartItems', JSON.stringify(appState));

// Recuperar estado
const cartItems = JSON.parse(localStorage.getItem('cartItems'));
console.log(cartItems); // Salida: [{ id: 1, name: 'Producto A' }, { id: 2, name: 'Producto B' }]
```

### 3.2. **Ejemplos de Uso de Session Storage**

**Almacenamiento de Datos Temporales:**

Ideal para datos que solo son relevantes durante la sesión de la página, como un proceso de formulario de varios pasos.

```js
// Guardar datos de paso de formulario
sessionStorage.setItem('currentStep', '2');

// Recuperar datos de paso de formulario
const currentStep = sessionStorage.getItem('currentStep');
console.log(currentStep); // Salida: 2
```

**Mantener el Estado del Usuario Dentro de una Sola Sesión:**

Útil para hacer un seguimiento de las interacciones del usuario en una aplicación de una sola página (SPA) sin afectar otras pestañas o sesiones futuras.

```js
// Guardar estado de interacción del usuario
sessionStorage.setItem('isLoggedIn', 'true');

// Recuperar estado de interacción del usuario
const isLoggedIn = sessionStorage.getItem('isLoggedIn');
console.log(isLoggedIn); // Salida: true
```

**Almacenamiento Temporal del Estado de la Interfaz de Usuario**:

Se puede utilizar para almacenar temporalmente el estado de la interfaz de usuario, como si un modal estaba abierto o cerrado.

```js 
// Guardar estado de UI
sessionStorage.setItem('isModalOpen', 'true');

// Recuperar estado de UI
const isModalOpen = sessionStorage.getItem('isModalOpen');
console.log(isModalOpen); // Salida: true
```

**Guardando texto entre actualizaciones**

El siguiente ejemplo guarda automáticamente el contenido de un campo de texto y, si el navegador se actualiza, restaura el contenido del campo de texto para que no se pierda la escritura.

```js
// Obtener el campo de texto que vamos a rastrear
let field = document.getElementById("field");

// Verificar si tenemos un valor de autoguardado
// (esto solo ocurrirá si la página se actualiza accidentalmente)
if (sessionStorage.getItem("autosave")) {
  // Restaurar el contenido del campo de texto
  field.value = sessionStorage.getItem("autosave");
}

// Escuchar cambios en el campo de texto
field.addEventListener("change", () => {
  // Y guardar los resultados en el objeto de session storage
  sessionStorage.setItem("autosave", field.value);
});
```

