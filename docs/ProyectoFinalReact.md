# P9.2 - **Asignación Final de Práctica con React**

## Objetivo

El objetivo de esta asignación es desarrollar una **Aplicación de Página Única (SPA) utilizando React** con múltiples rutas. Esto se logrará mediante el uso de **React Router** y **TypeScript**. La aplicación deberá recuperar datos a través de **solicitudes AJAX**, ya sea desde una API personalizada, una API de terceros o ambas.

## Requisitos del Proyecto

Cada equipo (compuesto por dos estudiantes) debe definir los requisitos de su aplicación, incluyendo el tipo de datos que manejará y si utilizará una API de terceros. Los equipos deben enviar la especificación de su aplicación en un panel proporcionado por el instructor en **Google Classroom**.

## Especificaciones Técnicas

### Estructura del Proyecto

El proyecto debe estar estructurado de la siguiente manera:

- **routes/** – Contiene todos los componentes de ruta.
- **layout/** – Almacena los diferentes componentes de diseño.
- **components/** – Incluye componentes atómicos, moleculares y organismos, organizados por **tipo** o **característica**.
- **services/** – Contiene bibliotecas para solicitudes a la API.
- **types/** – Almacena interfaces TypeScript que definen los formatos de datos utilizados en la aplicación.

### Organización de Componentes

El proyecto debe incluir una variedad de tipos de componentes:

- **Componentes Atómicos** – Elementos de UI más pequeños (botones, entradas de texto, etc.).
- **Componentes Moleculares** – Combinaciones de componentes atómicos que forman elementos reutilizables de la interfaz.
- **Componentes Organismo** – Secciones de UI más complejas compuestas por múltiples componentes moleculares.
- **Componentes de Diseño (Layout Components)** – Definen la estructura general de la aplicación.
- **Componentes de Ruta** – Páginas que definen diferentes vistas dentro de la aplicación.

### Requisitos de Rutas y API

- El proyecto debe incluir un **uso suficientemente complejo de rutas e integraciones de API**.
- Debe haber **al menos dos rutas distintas** para diferentes tipos de búsquedas dentro de la API.
- La aplicación debe incluir **funcionalidades de filtrado de datos**.
- El proyecto debe implementar **una ruta con un parámetro dinámico** (por ejemplo, `/ruta/:id`).

### Guías de Estilo

- Se permite cualquier método de estilización (CSS, SASS, Bootstrap, Tailwind CSS).
- Los estilos **deben estar ubicados dentro de la carpeta del componente**.
- No se deben usar archivos de estilos globales.
- Si se usa **CSS puro (vanilla CSS)**, se debe seguir la metodología **BEM (Block-Element-Modifier)** para la nomenclatura de clases.

## Entrega del Proyecto

Cada equipo debe entregar lo siguiente:

- Un enlace al **repositorio de GitHub** que contenga el proyecto completo.
- El repositorio de GitHub debe reflejar un **desarrollo progresivo** (no se aceptarán repositorios con pocos commits masivos).

## Archivo README

El repositorio debe incluir un archivo **README.md** que sirva como documentación del proyecto y debe contener:

1. **Objetivos** – Descripción de los principales objetivos del proyecto.
2. **Características** – Lista de las funcionalidades principales de la aplicación.
3. **Prototipo UI** – Boceto de cómo deben combinarse los componentes en pantalla.
4. **Tecnologías Utilizadas** – Lista de frameworks, bibliotecas y APIs empleadas.
5. **Instrucciones de Instalación** – Explicación sobre cómo configurar y ejecutar el proyecto localmente.
6. **Guía de Uso** – Descripción general de cómo funciona la aplicación.
7. **Documentación de la API** – Si aplica, documentación de los endpoints de la API utilizados en el proyecto.
8. **Notas de Implementación** – Explicación de los diferentes componentes que conforman la aplicación, las rutas y los diseños utilizados.
9. **Aplicación Desplegada** – Enlace a la versión en producción del proyecto (ej. GitHub Pages, Vercel).

## Criterios de Evaluación (Rúbrica)

El proyecto será evaluado con base en los siguientes aspectos:

| Criterio                    | Descripción                                                                    | Puntos  |
| --------------------------- | ------------------------------------------------------------------------------ | ------- |
| **Estructura del Proyecto** | Organización adecuada de carpetas y modularidad                                | 10      |
| **Diseño de Componentes**   | Uso de componentes atómicos, moleculares, organismos, layout y rutas           | 15      |
| **Rutas y Navegación**      | Implementación de React Router para SPA, incluyendo rutas dinámicas            | 10      |
| **Integración de API**      | Uso correcto de solicitudes AJAX, múltiples búsquedas en API y filtrado        | 10      |
| **Estilos**                 | Aplicación adecuada de metodologías CSS y estilos dentro de componentes        | 10      |
| **Documentación**           | README completo con todas las secciones requeridas, incluyendo UI y despliegue | 15      |
| **Calidad del Código**      | Código limpio, legible y mantenible                                            | 10      |
| **Presentación y Q&A**      | Claridad y profundidad en la presentación oral y respuestas a preguntas        | 20      |
| **Total**                   | **Puntaje final sobre 100**                                                    | **100** |

Cada miembro del equipo recibirá una **calificación individual** basada en su participación en la presentación y sus respuestas durante la sesión de preguntas y respuestas.

Este proyecto final servirá como una **demostración práctica** de la capacidad de los estudiantes para trabajar con **React, TypeScript, React Router, integración de API, arquitectura de componentes y metodologías de estilización**.
