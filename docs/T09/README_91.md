### **5.1 NPM**

De esto, comentar que `npm` es el gestor de paquetes de Node.js (recordemos que esto se basa en Node). Se usa para instalar y administrar dependencias.

Abrimos el terminal y procedemos con el comando:

```bash
npm init react-app ruta y nombre de la aplicación
```

`init` es el comando de npm para iniciar un nuevo proyecto. `react-app` es el paquete preconfigurado que se usa para crear una aplicacion de React con la estructura de directorios y archivos recomendada. `ruta y nombre de la aplicación` pues la ruta y el nombre del proyecto.

Es muy probable que dé error por problemas con dependencias, para solucionarlo, añadimos al comando:

```bash
--legacy-peer-dep
```

con esto le estamos diciendo que resuelva los problemas de dependencias que se encuentre. En general, esta opción nos será bastante útil cada vez que tengamos problemas con las dependencias

Ya tenemos el proyecto creado. Ahora hay que meterle cosillas. Bueno, ya le meteremos cosillas luego. Ahora lo importante es arrancar la app que acabamos de crear.

En primer lugar, nos movemos al directorio de la aplicación `cd ruta completa del directorio`. Después arrancamos React en ese directorio

```bash
npm start
```

El resultado nos debe mostrar las direcciones tanto local como de red desde las que son visible nuestra web.

![esto furula](img/direcciones.jpg)

Y si no ha habido ningún fallo de última hora, ya debería funcionar. Puede dar fallos. si los da, ejecutamos

```bash
npm install ajv@latest ajv-keywords@latest --legacy-peer-dep
```

y volvemos a lanzar `npm start`. Y ahora si se debe abrir el navegador con nuestra página (en blanco).

![ay mi react que bonito es](img/quebonito.jpg)
