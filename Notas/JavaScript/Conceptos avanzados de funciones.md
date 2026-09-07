---
orden: 15
tags:
  - Funciones
Comentario:
estado: true
---

## Funciones Autoejecutables (IIFE)

Una **IIFE** (_Immediately Invoked Function Expression_) es una función que se **define y ejecuta inmediatamente** después de su creación.

- Se envuelve entre paréntesis para convertirla en una **expresión**.
- Se ejecuta automáticamente con los paréntesis finales `()`.
- Crea un **ámbito privado** que evita la **contaminación del ámbito global**.
- Útil para **patrones de módulo**, **inicialización inmediata** o **protección de variables**.

Sintaxis:

```js
(function() {
  // Código privado
})();
```

Ejemplo:

```js
(function(a, b) {
  console.log('Executing the function: ' + (a + b));
})(3, 4);

// Executing the function: 7
```

## Funciones como Objetos (Ciudadanos de Primera Clase)

En JavaScript, las funciones son **objetos** y se consideran **"ciudadanos de primera clase"**, lo que significa que:

- Se pueden **asignar a variables**.
- Se pueden **pasar como argumentos**.
- Se pueden **retornar desde otras funciones**.
- Tienen **propiedades y métodos** como:
    - `name`: nombre de la función.
    - `length`: número de parámetros definidos.
    - `toString()`: devuelve el código fuente completo.

```js
function myFunction(a, b) {
  console.log(arguments.length);
  return a + b;
}

console.log(typeof myFunction);        // "function"
console.log(myFunction.name);          // "myFunction"
console.log(myFunction.length);        // 2
console.log(myFunction.toString());    // (Código fuente de la función)
```

> Estas propiedades son útiles en **meta-programación**, depuración y manipulación dinámica de funciones.

## Objeto `arguments`

`arguments` es un objeto **similar a un arreglo** que contiene **todos los argumentos pasados** a una función, independientemente de cuántos sean.

- Tiene la propiedad `length`.
- **No es un arreglo real** (no tiene métodos como `map` o `reduce`).
- Solo existe en **funciones tradicionales** (no en arrow functions).
- Permite trabajar con un **número variable de argumentos**.

```js
function sumAll() {
  let total = 0;
  for (let i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}

console.log(sumAll(5, 4, 13, 10, 9, 10, 11, 3)); // 65
```

## Parámetros Rest (`...`)

El operador **rest** permite agrupar un número indefinido de argumentos en un **arreglo real**.

- Es la **alternativa moderna** a `arguments`.
- Los parámetros rest **deben ir al final** de la lista de parámetros.
- Ideal para funciones que procesan listas de datos o argumentos variables.

```js
function sumAll(...numbers) {
  return numbers.reduce((acc, num) => acc + num, 0);
}

console.log(sumAll(1, 2, 3, 4)); // 10
```

## Scope (Ámbito)

El **scope** determina dónde son accesibles las variables.

### Scope Global

Variables declaradas fuera de cualquier función o bloque. Accesibles desde cualquier parte del programa.

```js
let globalVar = "I am global";

function show() {
  console.log(globalVar); // "I am global"
}
```

### Scope de Función

Variables declaradas dentro de una función solo existen dentro de ella. `var` tiene alcance de función.

```js
function example() {
  var localVar = "I am local";
  console.log(localVar); // "I am local"
}
// console.log(localVar); // Error: localVar no está definida
```

### Scope de Bloque

`let` y `const` tienen alcance de bloque `{}`.

```js
if (true) {
  let blockVar = "Within the block";
}
// console.log(blockVar); // Error: blockVar no está definida
```

## Closures

Un **closure** es una función que **recuerda el entorno léxico** donde fue creada, incluso después de que la función externa haya terminado su ejecución.

- Permite **mantener estado** entre llamadas.
- Útil para crear **variables privadas** y **encapsulación**.
- Ideal para **fábricas de funciones** y **contadores**.

```js
function createCounter() {
  let count = 0;
  return function() {
    count++;
    return count;
  };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

## Paso por Valor vs. Paso por Referencia

### Paso por Valor (Tipos Primitivos)

Los tipos primitivos (`number`, `string`, `boolean`, etc.) se copian **por valor**. Las modificaciones dentro de la función **no afectan la variable original**.

```js
let x = 10;

function changeValue(a) {
  a = 20;
}

changeValue(x);
console.log(x); // 10 (no cambia)
```

### Paso por Referencia (Objetos y Arreglos)

Los objetos y arreglos se pasan **por referencia**. Las modificaciones dentro de la función **sí afectan al objeto original**.

```js
const person = { name: 'Juan', lastName: 'Perez' };

function changeObjectValue(p) {
  p.name = 'Carlos';
}

changeObjectValue(person);
console.log(person.name); // "Carlos"
```

## Funciones Recursivas

Una función **recursiva** es aquella que **se llama a sí misma** hasta cumplir una condición de salida.

- Requiere un **caso base** para detener la recursión.
- Tiene un **caso recursivo** que modifica el valor en cada llamada.
- Un mal manejo puede generar **Stack Overflow**.

```js
function factorial(n) {
  if (n <= 1) return 1;        // Caso base
  return n * factorial(n - 1); // Caso recursivo
}

console.log(factorial(5)); // 120
```

### Stack Overflow (Desbordamiento de Pila)

Ocurre cuando una función se llama a sí misma indefinidamente sin llegar al caso base, llenando la pila de ejecución hasta que el programa lanza un error.

```js
function infiniteRecursion() {
  console.log("Calling the function...");
  infiniteRecursion(); // Sin caso base → Stack Overflow
}

// infiniteRecursion(); // ¡Error! (no ejecutar)
```

## Buenas Prácticas con conceptos avanzados de funciones

- Usa **IIFE** para aislar código y evitar contaminar el scope global.
- Prefiere **parámetros rest** en lugar de `arguments` para código más legible y moderno.
- Aprovecha **closures** para crear estado privado y encapsulación.
- Comprende la diferencia entre **paso por valor y por referencia** para evitar efectos colaterales no deseados.
- En recursión, **siempre define un caso base** y asegúrate de que la función progrese hacia él.
- Usa `let` y `const` en lugar de `var` para un control más preciso del scope.
