---
orden: 14
tags:
  - Funciones
Comentario:
estado: true
---

## ¿Qué es un Callback?

Un **callback** es una **función que se pasa como argumento** a otra función, con la intención de que sea **ejecutada más tarde**, ya sea al finalizar una tarea, cuando ocurra un **evento específico** o en un momento determinado.

Los callbacks son fundamentales para manejar la **asincronía**, la **ejecución secuencial de tareas** y los **eventos del navegador**.

## Concepto clave

Un callback es simplemente una función que se **entrega** a otra función para que esta la **ejecute cuando sea necesario**, sin necesidad de saber cuándo o cómo se invocará.

```js
function mainTask(callback) {
  console.log("Executing main task...");
  callback();
}

mainTask(() => {
  console.log("Callback executed after the main task");
});

// Executing main task...
// Callback executed after the main task
```

### Características principales

- Es una función pasada como argumento a otra.
- Puede ser **anónima** o **nombrada**.
- Permite manejar **acciones asíncronas**: temporizadores, eventos, peticiones HTTP, etc.
- Es la **base** de mecanismos modernos como **Promesas** y **`async/await`**.
- Permite **separar responsabilidades** y hacer el código más modular.

## Ejemplo síncrono

El callback se ejecuta inmediatamente después de la tarea principal, sin esperar nada.

```js
function greet(name, callback) {
  console.log(`Hello ${name}!`);
  callback();
}

greet("Juan", () => console.log("Bye!"));

// Hello Juan!
// Bye!
```

## Ejemplo asíncrono

El callback se ejecuta después de un tiempo determinado, gracias a `setTimeout`.

```js
function doSomething(callback) {
  setTimeout(() => {
    console.log("Operation completed");
    callback();
  }, 2000);
}

doSomething(() => {
  console.log("Callback executed after 2 seconds");
});

// (espera ~2 segundos)
// Operation completed
// Callback executed after 2 seconds
```

>📌 `setTimeout` es una función global que recibe un callback y un tiempo en milisegundos para ejecutarlo.

## Ventajas y desventajas de los callbacks

|**Ventajas**|**Desventajas**|
|---|---|
|Simples y compatibles con todos los navegadores.|Pueden generar **Callback Hell** (anidación excesiva).|
|Base para Promesas y `async/await`.|Manejo de errores más complejo si no se controla cada callback.|
|Flexibles y fáciles de integrar con eventos o temporizadores.|Código menos legible en flujos complejos.|
|Permiten separar lógica y mejorar la modularidad.|Dificultan el seguimiento del flujo de ejecución.|

## Usos comunes de callbacks

### Temporizadores (`setTimeout`, `setInterval`)

```js
setTimeout(() => {
  console.log("This executes after 1 second");
}, 1000);
```

### Eventos del DOM

```js
document.getElementById("button").addEventListener("click", function() {
  console.log("Button clicked");
});
```

### Métodos de arreglos (`forEach`, `map`, `filter`, etc.)

```js
const numbers = [1, 2, 3];

numbers.forEach(number => {
  console.log(number * 2);
});

// 2
// 4
// 6
```

## Callbacks como parámetros de función

Puedes pasar tanto **funciones anónimas** como **funciones con nombre** como callbacks.

```js
function executeOperation(operation) {
  const result = operation(10, 5);
  console.log(`Result: ${result}`);
}

// Callback anónimo (arrow function)
executeOperation((a, b) => a * b);

// Callback nombrado
function add(a, b) {
  return a + b;
}
executeOperation(add);

// Result: 50
// Result: 15
```

>La función `executeOperation` recibe un parámetro que es una función, lo que permite pasar lógica personalizada en el momento de la llamada.

## Callback Hell (Infierno de Callbacks)

El **Callback Hell** (o _Pirámide de la Perdición_) ocurre cuando se anidan múltiples callbacks uno dentro de otro, generando una estructura difícil de leer y mantener, lo cual trae los siguientes problemas:

- Código visualmente en forma de pirámide.
- Dificultad para manejar errores.
- Complejidad para modificar o agregar pasos intermedios.
- Baja legibilidad y mantenibilidad.

```js
doTask1(() => {
  doTask2(() => {
    doTask3(() => {
      doTask4(() => {
        console.log("Excessive callback nesting");
      });
    });
  });
});
```

> 📌 **Solución moderna:** Usar **Promesas** o **`async/await`** para aplanar la estructura y mejorar el flujo.

## Buenas prácticas con callbacks

- **Nombra los callbacks** cuando sea posible para mejorar la depuración.
- **Maneja errores** explícitamente (por ejemplo, con el patrón de error-first callback).
- **Evita el anidamiento profundo**; si ves más de 2 o 3 niveles, considera usar Promesas.
- **Documenta** qué parámetros recibe el callback y qué debe retornar.
- **Usa arrow functions** para callbacks cortos y con `this` léxico.
