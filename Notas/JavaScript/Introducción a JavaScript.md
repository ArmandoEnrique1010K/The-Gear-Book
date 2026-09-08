---
orden: 1
tags:
  - Introducción
estado: true
Comentario: Agregar una nueva sección sobre Babel para transpilar código en React
---

## ¿Qué es JavaScript?

JavaScript es un **lenguaje de programación interpretado, dinámico, multiparadigma y orientado a objetos basado en prototipos**. Es una de las tecnologías fundamentales en el desarrollo web, junto con HTML (estructura) y CSS (estilo). Su principal función es dotar de interactividad y dinamismo a las páginas web, permitiendo desde animaciones y validaciones de formularios hasta actualizaciones en tiempo real sin necesidad de recargar la página.

![JavaScript Logo|164](../assets/JavaScript%20logo.png)

## Historia de JavaScript

- **1995**: Creado por **Brendan Eich** en **Netscape Communications** en solo 10 días. Pasó por los nombres **Mocha**, **LiveScript** y finalmente **JavaScript** (por una alianza con Sun Microsystems, aunque no tiene relación técnica con Java).
- **1996**: Microsoft lanza **JScript** para Internet Explorer, lo que genera incompatibilidades entre navegadores.
- **1997**: Se estandariza el lenguaje bajo el nombre **ECMAScript (ES1)**, entregado a **ECMA International** y mantenido por el comité **TC39**.
- **2006**: Aparece **jQuery**, que simplifica la manipulación del DOM y unifica el comportamiento entre navegadores, dominando el Frontend durante años.
- **2009**: Llega **ES5**, con mejoras como el modo estricto (`"use strict"`), nuevos métodos de array (`map`, `filter`, etc.) y soporte nativo para JSON. Ese mismo año, **Ryan Dahl** crea **Node.js**, que permite ejecutar JavaScript en el servidor, abriendo la puerta al desarrollo **FullStack**.
- **2015**: Se lanza **ES6 (ES2015)**, una de las actualizaciones más importantes, con características como clases (`class`), módulos (`import`/`export`), funciones flecha (`() => {}`), variables con ámbito (`let`/`const`) y promesas (`Promise`). A partir de aquí, el lenguaje se actualiza anualmente.
- **2017**: **ES2017** introduce `async`/`await`, facilitando la escritura de código asíncrono legible. En esta época, los Frameworks más populares son **Vue**, **React** y **Angular** en Frontend, y **Node.js** con **Express** en Backend.
- **2020**: **ES2020** añade el **operador de encadenamiento opcional** (`obj?.prop`) y el **operador de coalescencia nula** (`??`), mejorando el manejo de valores nulos o indefinidos.

## ECMAScript vs JavaScript

Esta es la confusión más común. La diferencia es sencilla pero clave:

- **ECMAScript (ES):** Es el **estándar** o la **especificación**. Es un documento escrito que define cómo debe funcionar el lenguaje (reglas, sintaxis, tipos, estructuras de control). Piensa en ello como el "manual de instrucciones" o el "contrato" que el lenguaje debe cumplir. Lo gestiona la organización ECMA International (de ahí el nombre). Las versiones más famosas son **ES6/ES2015** (que fue un cambio gigante) y las posteriores (ES2016, ES2017, etc., que ahora son anuales).
- **JavaScript (JS):** Es la **implementación práctica** de ese estándar. Es el lenguaje que realmente usan los navegadores, Node.js, Deno, etc.

## El motor de JavaScript (El "intérprete")

El motor de JavaScript es el programa que **lee, entiende y ejecuta** tu código JavaScript. Es el corazón del navegador (o de Node.js) que convierte tu texto en instrucciones que la computadora puede procesar.

### ¿Cómo funciona a grandes rasgos?

1. **Parsing:** Lee tu código y lo convierte en una estructura de datos llamada Árbol Sintáctico Abstracto (AST).
2. **Compilación Just-In-Time (JIT):** En lugar de interpretar línea por línea (muy lento), los motores modernos compilan tu código a código máquina justo antes de ejecutarlo, optimizándolo sobre la marcha.
3. **Ejecución:** Corre el código máquina resultante.

### Principales motores

Cada motor implementa el estándar ECMAScript, pero a su propio ritmo y con sus propias optimizaciones internas.

- **V8:** De Google, usado en Chrome, Brave y en Node.js (el más famoso).
- **SpiderMonkey:** De Mozilla, usado en Firefox (el primero en crearse).
- **JavaScriptCore (Nitro):** De Apple, usado en Safari.
- **Chakra:** De Microsoft (ya discontinuado en Edge, que ahora usa V8).

## Ámbitos de uso

JavaScript se ejecuta tanto en el **navegador** como en el **servidor**, lo que lo convierte en un lenguaje extremadamente versátil. Algunos de sus usos más destacados son:

- **Desarrollo web Frontend**: Con frameworks como **React**, **Angular** o **Vue.js**, se crean interfaces dinámicas y se manipula el DOM de forma eficiente.
- **Desarrollo web Backend**: Gracias a **Node.js**, se pueden construir servidores, APIs REST, sistemas de autenticación y manejo de bases de datos. **Express.js** es el framework más usado para ello.
- **Aplicaciones móviles**: Herramientas como **React Native** e **Ionic** permiten desarrollar apps nativas o híbridas para iOS y Android usando JavaScript.
- **Videojuegos**: Librerías como **Phaser** (2D) y **Three.js** (3D), junto con **WebGL**, posibilitan la creación de juegos y gráficos interactivos directamente en el navegador.
- **IoT y Robótica**: Plataformas como **Johnny-Five**, basadas en Node.js, permiten programar hardware como **Arduino** o **Raspberry Pi**, controlando sensores, motores y luces LED.

## Compatibilidad entre navegadores al usar JS

**No todos los navegadores implementan la misma versión de ECMAScript al mismo tiempo**. Un navegador antiguo (como Internet Explorer 11) no entiende `arrow functions` (=>) o `let/const`, mientras que Chrome y Firefox sí.

### El desafío en la práctica

- Los navegadores **modernos** (Chrome, Firefox, Safari, Edge) se actualizan automáticamente y suelen soportar las últimas características del estándar en cuestión de semanas.
- Los navegadores **antiguos** o con ciclos de actualización lentos (Internet Explorer, navegadores integrados en TVs o coches, WebViews de Android versiones antiguas) se quedan rezagados durante años.

### ¿Sigue siendo un problema hoy?

**Mucho menos que hace 5 o 10 años**. Todos los navegadores modernos soportan prácticamente todo ES6+ (2015 en adelante). Esto significa que puedes usar `class`, `arrow functions`, `const/let`, `promesas`, `template literals` y `destructuring` sin miedo en la gran mayoría de proyectos.

**El verdadero problema actual** son estos casos específicos:

- **Internet Explorer 11** (aún usado en entornos corporativos).
- **WebViews antiguos** (por ejemplo, Android 4.4 - 6.0, que usan versiones viejas de Chrome).
- **Navegadores integrados** en aplicaciones de escritorio o dispositivos embebidos.
- **Usuarios que no actualizan sus navegadores** (por políticas de empresa o dispositivos obsoletos).
