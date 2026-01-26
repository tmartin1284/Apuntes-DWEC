# **UNIDAD 09 - React**

## **1. Introducción**

[React](https://es.react.dev/) es una libreria para el desarrollo de aplicaciones web. Concretamente una librería javascript para construir interfactes web.  
React se basa en el uso de **componentes**, una fusión `html` con `javascript`, escritos en **JSX (JavaScript XML)**. A través de JSX, se crea una copia de DOM (Modelo de Objetos del Documento) llamada **DOM virtual**. Si un componente cambia su estado, React compara el **DOM virtual** con el DOM real (de la página web) y aplica este cambio solamente al elemento que ha sido actualizado, sin necesidad de volver a renderizar toda la página.

### **¿Por qué usar _React_?**

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

## **2. Fundamentos de React**

La parte de Fundamentos de React, así como la evolución desde el punto de vista del desarrollo del código que implica React, está más o menos explicada en estas transparencias.

[Fundamentos de React](slides/1._Fundamentals.pdf)

## **3. Características Modernas de JavaScript para el Desarrollo en React**

###**3.1 Módulos de JavaScript**

¿Qué son los Módulos?

Importar y exportar funciones, objetos o valores de un archivo a otro.

**Sintaxis**

```javascript
// Exportando
export const greet = () => {
  console.log("¡Hola!");
};

// Importando
import { greet } from "./greetModule.js";
greet();
```

### **3.2 Asignación por Desestructuración**

¿Qué es la Desestructuración?

Una sintaxis para desempaquetar valores de arrays o propiedades de objetos en variables distintas.

**Ejemplos**

```javascript
// Desestructuración de Array
const [first, second] = [1, 2, 3];
console.log(first, second); // Salida: 1, 2

// Desestructuración de Objetos
const user = { name: "Alice", age: 25 };
const { name, age } = user;
console.log(name, age); // Salida: Alice, 25
```

### **3.3. Operadores Spread y Rest (...)**

#### **Operador Spread**

Se utiliza para expandir elementos de un array u objeto.

```javascript
const arr = [1, 2, 3];
const newArr = [...arr, 4, 5];
console.log(newArr); // Salida: [1, 2, 3, 4, 5]

const user = { name: "Alice", age: 25 };
const updatedUser = { ...user, location: "NY" };
console.log(updatedUser); // Salida: { name: 'Alice', age: 25, location: 'NY' }
```

#### **Operador Rest**

Se utiliza para recolectar argumentos en un array o las propiedades restantes en un objeto.

```javascript
const sum = (...numbers) => numbers.reduce((total, num) => total + num, 0);
console.log(sum(1, 2, 3)); // Salida: 6

const { name, ...rest } = { name: "Alice", age: 25, location: "NY" };
console.log(rest); // Salida: { age: 25, location: 'NY' }
```

### **3.4 Funciones de Flecha**

¿Qué son las Funciones de Flecha?

Una sintaxis concisa para escribir funciones. También manejan el contexto de `this` de manera diferente a las funciones normales.

**Sintaxis**

```javascript
const add = (a, b) => a + b;
console.log(add(2, 3)); // Salida: 5
```

### **3.5 Literales de Plantilla**

¿Qué son los Literales de Plantilla?

Una sintaxis para crear cadenas con expresiones incrustadas usando comillas invertidas.

**Ejemplos**

```javascript
const name = "Alice";
console.log(`¡Hola, ${name}!`); // Salida: ¡Hola, Alice!
```

### **3.6 Parámetros por Defecto**

¿Qué son los Parámetros por Defecto?

Asignar valores predeterminados a los parámetros de una función.

**Ejemplos**

```javascript
const greet = (name = "Invitado") => `¡Hola, ${name}!`;
console.log(greet()); // Salida: ¡Hola, Invitado!
```

## **4. Comparación entre Código React y Código JS**

Vamos a ver una [página simple en Javascript (con vainilla)](https://codesandbox.io/p/devbox/hg2rkw), y después veremos una [página similar usando React](https://codesandbox.io/p/devbox/88hszh).
Ambas están en mi repositorio.

### **4.1 JavaScript [y ya]**

![Web sencillita](img/websimple.jpg)

En una web basada en JS tenemos tres elementos principales:

- el archivo `html`, que es la página en si;
- el archivo `css` ~que sirve para cosas raras que vereis con Jose Enrique~ para dar formato a la web;
- y el archivo `.js` que se encarga de obtener los botones, configurar los listeners, gestionar el DOM y definir la funcionalidad cada vez que se pulsa un botón (cambiando el fondo de todos los botones, generando el texto, etc...).

Todo esto es lo que hemos visto hasta ahora en el módulo.

### **4.2 Librería React**

Una aplicación de **React** es un poco más compleja. Empezando porque se basa en una estructura de archivos y directorios muy bien definida. Más adelante la veremos en detalle.

![React sencillita](img/reactsimple.jpg)

Si echamos un vistazo, en la carpeta `/Public` tenemos

- Un archivo `.html`, que está casi vacio: tiene un `<div>` que es la carcasa de la web (SPA).
- El resto de elementos están en la carpeta `/src`, aunque hay más carpetas propias de la estructura de un proyecto **React**.
- El archivo`.js`, de hecho también está bastante vacío, y su función es solo para vincular el `html` con **React**, esto es, _a través del achivo `.js` se va a usar **React** para **renderizar** la pagina web_. De hecho la función `render` es un componente de React que está devolviendo etiquetas html **marcadas** (distinguirás estas etiquetas porque aparecen en mayúscula, aparte que el editor las marca con otro color).

El archivo `App.js` tiene toda la "chicha": Tiene la función `app` que devuelve un código html muy parecido al html del ejemplo anterior **_¡¡¡¡Se está mezclando html con js!!!! ¡¡ay dios mio!!_**. Por otra parte, no tenemos las instrucciones JavaScript pero si que tenemos algunas sentencias JS mezcladas en el codigo html **_to junto! que estres!!_**.

Si aparecen unos elementos que nos hablan del **_estado (o de los estados)_** de una página web. Estos estados los controla React, y se aplican a todos los elementos que integran la web.

Para arrancar el proyecto, nos situamos con el terminal en la carpeta _react_ y ejecuta el comando `npm start`.

### **4.3 _Programaciòn declarativa_ vs _imperativa_**

En React se programa o configura el estado en el que tiene que estar todos los componentes de la página, no los pasos para llegar a ese estado. Por tanto la web va a estar siempre en un estado válido. Es lo que se denomina **Programación Declarativa** que basicamente consiste en decir como tiene que estar todo configurado, pero sin decir los pasos para configurarlo, que sería **Programación imperativa**.

![Declarativo vs Imperativo](img/decvsimp.png)

La programación declarativa se basa en una máquina de estados, y las transiciones entre estados.

<div class="exercise-box">
    <h3><i class="fas fa-laptop-code"></i> Ejercicio Práctico: React o solo JS</h3>
    <p>1. Editemos ambas versiones de la web para añadir un cuarto botón, llamadlo como queráis. 
    NOta: Los arrais ya están preparados para ese botón</p>
    <p><u>Deberíamos cronometrarnos para ver lo que nos cuesta hacerlo con una y otra tecnología.</u></p>
</div>

## **5. Creando un proyecto React en Code**

Hay varias versiones a la hora de crear un proyecto en React:

- "A pelo". Usando el gestor de paquetes [**npm**](https://www.npmjs.com/) que ya comentamos en el primer tema.
- O con el bundler de [**vite**](https://vite.dev/).

Por la simplicidad que ofrece Vite, nos centramos por esa opción. Aún así, si queréis echarle un ojo a cómo crearlo con npm, está en [este enlace](./README_91.md).

### **5.1 React con Vite**

Si queremos usar React con Vite, simplemente debemos seguir los siguientes pasos, tanto desde una localización en VSCode, como desde una carpeta en nuestro sistema de archivos (Ojo, al terminar el proceso nos creará una carpeta con todo el proyecto):

- Abrir una terminal (como siempre, os acordáis de cuánto odiabais los comandos en SiSi... quién nos iba a decir...), y escribimos

```bash
npm create vite@latest
```

con esto creamos un proyecto de Vite, pero OJO, que nos va a pedir cosillas (recuerda que estas opciones pueden ser ligeramente diferentes conforme actualicen vite):

- En primer lugar, nos va a pedir permiso para crear los paquetes. Decimos que `y`es.

* Después nos pide un _nombre_ para el proyecto. Recordad que creará una carpeta con el nombre del proyecto en el directorio actual, y dentro creará toda la estrucura del proyecto. Si forzamos la creación de directorios intermedios, asumirá que le hemos dado la _ruta_ y nos volverá a pedir _nombre_ del proyecto. ![nombre](img/nombre.jpg)
* El _framework_ que vamos a utilizar ![tecnologia](img/tecnologia.jpg) y podremos desplazarnos con las flechas.
* El _lenguaje_, ![lenguaje](img/lenguaje.jpg)

* Con esto, ya tendremos creado el proyecto Vite. Si todo ha ido bien nos mostrará una imagen con más info: ![vite](img/vitecreado.jpg)
* El último paso de vite nos pregunta si queremos que instale y ejecute el proyecto. Si le decimos que **yes** nos saltamos los siguientes tres pasos, y nos vamos directamente a la ejecución del proyecto.
  - Si le decimos que **no** tenemos que ejecutar los tres comandos que nos dice Vite (Recordad usar la carpeta que hayais puesto en vuestro proyecto):

```bash
#nos vamos a la carpea del proyecto
cd Tema9\ProyectoViteReact

# instalamos npm
npm install

# actualizamos paquetes de react y reactDOM por si acaso
npm install  react@latest react-dom@latest
```

- Ejecutamos la aplicación

```bash
npm run dev
```

- Y obtenemos este resultado:

![inicio vite](img/vite.jpg)

Aqui podemos ver la dirección en localhost dónde se está mostrando la página, y cómo podemos acceder a los archivos de código. Por otra parte, se habrá creado el proyecto React con la estructura de directorios y ficheros vista.

![proyecto](img/proyectoreact.JPG)

Y por supuesto, en el navegador, podemos ver nuestra primera página

![vitereact](img/vitereact.jpg).

### **5.2 Configuración del entorno de desarrollo para trabajar con React**

Esta parte se basa en las transparencias [setup React](slides/2._Setup.pdf), pero las adapta a una distribución en VSCode.

Para recapitular, en el desarrollo de un proyecto con React vamos a necesitar algunos elementos:

- Las librerías de _React_ y _React-DOM_, que se han instalado al crear el proyecto de React en la sección anterior
- Un gestor de contenido, que sería `npm` o `yarn`, aunque el primero ya lo tenenos puesto.
- Si hemos hecho la instalación con Vite, él se va a encargar de empaquetar el código que generemos.

Ahora es el momento de instalar algunas liberias y paquetes de desarrollo:

#### **Linting**

Cualquier _Lintern_ tiene el objetivo de revisar, analizar y mejorar nuestro código, conforme vamos escribiendo. No sólo detecta errores que provocarían _no compilar_, si no que detecta malas prácticas, inconsistencias y otros fallos en el código fuente.
Por otra parte, sugiere mejoras de estilo y optimizaciones en cuanto a la escritura de código. Aunque debemos recordar que al final cada desarrollador _desarrolla_ su propia forma de programar. También detecta variables o funciones no usadas.
Salvo que sean errores propios del lenguaje (que el compilador detectaría, o que llevaría a un error en el caso de lenguajes interpretados), los errores que detecta un lintern generalmente no impiden que el código se ejecute bien.
Por esto, a veces las líneas rojas que marca el Lintern pueden sacarnos de quicio.

Podemos encontrarnos varios Linterns (algunos incluso están como pluguins de VSCode):

- [**ESLint**](https://eslint.org/) es el más utilizado en proyecto se React. Detecta problemas de código, errores de sintaxis y problemas específicos de React. Además, permite definir reglas personalizables e incorporar estilos predefinidos (Airbnb, Standard, etc.). Las reglas principalmente se usan en grandes equipos de desarrollo, para unificar la manera de programar de todos los integrantes.
- **Style-lint** para mantener un estilo uniforme en las hojas de estilo.

**Eslint** ya viene añadido al proyecto si lo hemos creado con **Vite**.
Sin embargo, también se recomienda instalar [**Airbnb**](https://airbnb.io/javascript/), que son unas reglas creadas por la empresa homónima que se enfocan en (i) Mejorar la **consistencia** para que el código en todo el proyecto, (ii) Garantizar la **legibilidad**, y (iii) prevenier los **errores** más comunes.

Las reglas más comunes de Airbnb implican:

- Uso de comillas simples (') en lugar de dobles (").
- Indentación de 2 espacios.
- Uso de punto y coma (;) al final de cada línea.
- Buenas prácticas:
  - Prohíbe el uso de variables no declaradas.
  - Requiere el uso de const o let en lugar de var.
  - Sugiere usar funciones flecha (=>) siempre que sea posible.
- Específico para React:
  - Requiere propTypes o TypeScript para la validación de propiedades.
  - Promueve el uso de fragmentos (<></>) en lugar de div innecesarios.
  - Obliga a seguir buenas prácticas en los hooks de React.
- Compatibilidad con ES6+:
  - Promueve el uso de destructuración de objetos y arrays.
  - Sugiere usar template literals para la concatenación de cadenas.

#### **Prettier**

[**Prettier**](https://prettier.io/) es una herramienta de formateo de código que se acopla con _Eslint_, nos permite basicamente hacer un formateo automático del código (esto es, añadir ; al final de cada línea de js, si así lo decidimos). Con ello, logramos un estilo consistente.
instalar pretieer

#### **Husky**

[**Husky**]() es una herramienta que permite ejecutar ganchos (llamados hooks, como el capitán Hook) de git en los proyectos.
Los ganchos son scripts que se ejecutan en ciertos momentos clave del proyecto, como la compilación, o la subida al repositiorio de forma automática.

- Automatización de tareas: Puedes configurar Husky para ejecutar tareas automáticamente, como linters, pruebas o formateadores, antes de realizar commits o push.
- Prevención de errores: Garantiza que el código que se sube al repositorio cumpla con los estándares y no contenga errores básicos.
- Flujo de trabajo colaborativo: Asegura que todo el equipo siga las mismas reglas de calidad y estilo.

### **5.3 Instalación de las extensiones en nuestro proyecto**

Una vez creado el proyecto con Vite, según el apartado 5.1, ya nos incluye **Eslint**, pero no las reglas de **Airbnb**, o **prettier** o **Husky**.
Para hacer todo esto, seguimos los siguientes pasos:

1. Comprobamos que tengamos instalado `npm` y `node`, que deberían estar según los pasos del punto 5.1

```bash
npm -v
node -v

```

2. Se configura `eslint` y `prettier` como `formatter` dentro de code. Para ello, en `settings` (`ctrl + ,` o `Archivo > Preferencias > Configuración`) buscamos `formatter` y le indicadmos que es `prettier`; además buscamos la opción de `format on save`, y la activamos. Con esto además, formaterará el texto automáticamente cuando guardemos un archivo (y lo guardará cuando cambiemos de archivo). Todo en uno.

![configuración de vscode](./img/configuración.JPG)

3. Instalamos las reglas Airbnb en eslint, e inicializamos eslint. Airbnb funciona con eslint 8, si tenemos otra versión, va a dar problemas, por tanto, forzaremos su instalación

```bash
# instalamos el eslint 8, forzando la versión
npm install -D eslint@8 --force --legacy-peer-deps

# instalamos el airbnb
npm install -D eslint eslint-config-airbnb eslint-config-airbnb-base eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-jsx-a11y eslint-plugin-import --legacy-peer-deps

# inicializamos eslint
npx eslint --init
```

Para terminar el proceso de instalación, nos va a hacer una serie de preguntas. Aqui os dejo mi respuesta, según un proyecto básico de React con JS.

![instalación de eslint con airbnb](./img/eslint.JPG).

<!--
Al finalizar nos va a crear un archivo _.eslintrc.cjs_ o _.eslintrc.js_. los archivos de conf de eslint.

4. Editamos el archivo .eslintrc.cjs para que quede con esta forma. Ojo, he incluido la parte de prettier

```conf
module.exports = {
  env: {
    browser: true,
    es2021: true,
  },
  extends: [
    "airbnb",
    "airbnb/hooks",
    "plugin:prettier/recommended", //importante
    "eslint:recommended",
    "plugin:react/recommended",
  ],
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 15,
    sourceType: "module",
  },
  plugins: ["react"],
  rules: {
    //reglas que queramos añadir
  },
};

```

5. Instalamos prettier; instalamos y activamos Husky; e instalamos lint-staged (Dejo todos los comandos juntos, para ejecutarlos de una). Con esto nos creará la carpeta .husky/ y un hook pre-commit

```bash
npm install -D prettier eslint-config-prettier eslint-plugin-prettier

# Crea .prettierrc:
echo '{
  "singleQuote": true,
  "semi": true,
  "trailingComma": "all",
  "printWidth": 100
}' > .prettierrc

# Crea .prettierignore:
echo "dist
node_modules " > .prettierignore

# Instalar Husky
npm install -D husky

# Activar Husky:
npx husky init

# Instalar lint-staged
npm install -D lint-staged

```

6. Configurar scripts y lint-staged en package.json

```conf
{
  .....
   "scripts": {
  ...
  "lint": "eslint . --ext js,jsx --fix",
   "format": "prettier . --write"
  ...
   }

....

  "lint-staged": {
    "src/**/*.{js,jsx}": [
      "eslint --fix",
      "prettier --write"
   ]
  }
}

```

7. Configurar Husky para usar lint-staged, y lo lanzamos:

```bash
# Reemplazamos el archivo /Husky/pre-commit
echo '
#!/usr/bin/env sh
. "$(dirname -- "$0")/\_/husky.sh" ' > .husky/pre-commit

npx lint-staged

```
-->

En principio, después de todo esto, el proyecto ya debe estar configurado con todos los plugins.

## **6. Renderizado con React**

[Render react](slides/3._Render.pdf)

## **7. Gestión de _Props_ y _State_**

[props state](slides/4._Props__state.pdf)

- [Learn React from react.dev](https://react.dev/learn)
- [Vite Guide](https://vite.dev/guide/)
