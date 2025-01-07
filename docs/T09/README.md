# **UNIDAD 9 - React**

## 1. **Introducción**

[React](https://es.react.dev/) es una libreria para el desarrollo de aplicaciones web. Concretamente una librería javascript para construir interfactes web.  
React se basa en el uso de **componentes**, una fusión  `html` con `javascript`, escritos en **JSX (JavaScript XML)**. A través de JSX, se crea una copia de DOM (Modelo de Objetos del Documento) llamada **DOM virtual**. Si un componente cambia su estado, React compara el **DOM virtual** con el DOM real (de la página web) y aplica este cambio solamente al elemento que ha sido actualizado, sin necesidad de volver a renderizar toda la página.

### ¿Por qué usar **React**?
De hecho, JavaScript ya se encarga "por detrás", de cagar los datos que la página web necesita en función de la interacción del usuario (ir a una nueva pestaña, por ejemplo), diseñar la nueva página web, y presentarla al usuario de forma transparente a este. Y esto ha convertido a JS en un lenguaje demandado para la programación web.

Sin embargo, usar **sólo Javascript** en esencia no es una buena opción para proyectos realistas (recordemos que estamos evolucionando hacia SPA - Single Page Application, es decir, webs dónde sólo hay una página -vacia- que se va cargando con JS):

  - Crear **páginas complejas** (realistas), se puede convertir en algo **tortuoso**. Sobretodo en un proyecto real dónde los requisitos van cambiando.
  - JS (de verdad) es propenso a errores. No que la página no haga lo que debe, si no **que haga lo que no debe**.
  - Los proyectos de JS (de verdad) son **dificiles de entender** (benditos comentarios), y por tanto **mantener o editar**.
  

React ofrece una manera más lógica e intuitiva de estructurar una página web con las que ofrece soluciones a esas desventajas de JS:

  - Los componentes de React **agilizan la creación de una interfaz sensible a cualquier cambio** en un sitio web o una aplicación de cualquier complejidad.
  - Gracias al DOM virtual, la biblioteca **ahorra recursos y tráfico**.
  - El código de React tiene una **lógica clara**, es fácil de leer, entender y depurar, lo que ayuda a reducir errores.
  - Las interfaces interactivas creadas con React garantizan una **mejor experiencia de usuario**.
  - React es fácil de aprender, tiene una **documentación accesible** y muchos recursos gratuitos online.
  
Todo esto, hace que React sea una de las librerias/habilidades más demandadas para conseguir el trabajo de desarrollo Front End. Aunque también tiene algunos puntos en contra:

  - Necesidad de un conocimiento sólido de **HTML** y **JavaScript** para aprender la sintaxis de JXS.
  - La biblioteca puede **aumentar el tamaño de tu aplicación**.
  - React solo visualiza la interfaz, pero para crear un proyecto completo, se necesita una **pila de tecnología**.


## 2. **Código React y Código JS**

Vamos a ver una [página simple en Javascript (con vainilla)](https://codesandbox.io/p/devbox/hg2rkw), y después veremos una [página similar usando React](https://codesandbox.io/p/devbox/88hszh). Sus estructuras etc, y las analizamos.

![Web sencillita](/docs/T09/img/websimple.JPG)

En una web JS, tenemos la página HTML, y el archivo JS, que se encarga de obtener los botones, configurar los listeners, y definir la funcionalidad cada vez que se pulsa un botón (cambiando el fondo de todos los botones, generando el texto, etc...). 


![React sencillita](/docs/T09/img/reactsimple.JPG)


Si echamos un vistazo, en la carpeta /Public tenemos un archivo html, que está casi vacio. Tiene un `<div>` que  es la carcasa de la web (SPA).
El archivo JS, de hecho también está bastante vacío, y su función es solo para vincular el html con React, esto es, usar React para **renderizar** la pagina web. De hecho la función `render` es un componente de React que está devolviendo etiquetas html **marcadas** (distinguirás estas etiquetas porque aparecen en mayúscula). 
El archivo `App.js` tiene toda la "chicha". Tiene la función `app` que devuelve un código html muy parecido al html del ejemplo en la versión sin React. Por otra parte, no tenemos las instrucciones JavaScrpt pero si que tenemos algunas sentencias JS mezcladas en el codigo html. 
Si aparecen unos elementos que nos hablan del estado (o de los estados) de una página web. Estos estados los controla React, y se aplican a todos los elementos que integran la web.

Importante: En React se programa o configura el estado en el que tiene que estar todos los componentes de la página, no los pasos para llegar a ese estado. Por tanto la web va a estar siempre en un estado válido.


![Declarativo vs Imperativo](/docs/T09/img/decvsimp.png)


