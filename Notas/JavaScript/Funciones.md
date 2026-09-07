---
orden: 12
tags:
  - Funciones
Comentario:
estado: true
---

## Funciones

Una **función** en JavaScript es un bloque de código reutilizable diseñado para realizar una tarea específica. Puede **devolver un valor** usando la instrucción `return`. Si no se incluye `return`, la función ejecuta su lógica pero retorna `undefined` (esto se conoce como **función de procedimiento**).

Las funciones pueden recibir **parámetros** (variables internas) y, al ser invocadas, se les pasan **argumentos** (los valores reales que se procesan).

Existen distintas formas de definir funciones, y cada una tiene comportamientos particulares en cuanto a **hoisting**, **contexto (`this`)** y **disponibilidad en tiempo de ejecución**.

## Function Declaration (Declaración de Función)

Es la forma clásica de definir funciones. Se declaran con la palabra clave `function` y siempre tienen un nombre identificable.

- **Tienen hoisting**: pueden ser llamadas antes de su declaración.
- **Crean su propio contexto de `this`**.
- Ideales para funciones reutilizables y de propósito general.

Sintaxis:

```js
function functionName(parameters) {
  // Código a ejecutar
  return value;
}

functionName(arguments);
```

Ejemplo:

```js
console.log(greet("Carlos")); // "Hello Carlos" (funciona por hoisting)

function greet(name) {
  return `Hello ${name}`;
}
```

>**⚠️ Nota:** El hoisting en funciones significa que la declaración completa se eleva al inicio del ámbito durante la compilación, permitiendo su uso antes de la definición.

## Function Expression (Expresión de Función)

Se define como una expresión y se asigna a una variable (generalmente con `const` o `let`).

- **No tienen hoisting**: deben definirse antes de usarlas.
- **Crean su propio contexto de `this`**.
- Pueden ser anónimas o tener un nombre interno (para recursión o depuración).

### Function Expression anónima

La función no tiene nombre; se invoca mediante la variable asignada.

Sintaxis:

```js
const variableName = function(parameters) {
  return value;
};

variableName(arguments);
```

Ejemplo:

```js
// console.log(add(1, 2)); // Error: la función no está inicializada

const add = function(a, b) {
  return a + b;
};

console.log(add(5, 3)); // 8
```

### Function Expression con nombre interno

El nombre interno permite **autorreferencia** (útil para recursión) y mejora la **depuración** (aparece en trazas de pila). Aunque es válido, hoy en día no es un patrón común.

Sintaxis:

```js
const variableName = function internalName(parameters) {
  return value;
};
```

Ejemplo:

```js
const factorial = function calculate(n) {
  return n <= 1 ? 1 : n * calculate(n - 1);
};

console.log(factorial(5)); // 120
```

## Arrow Functions (Funciones de Flecha)

Son una sintaxis más corta y moderna introducida en ES6.

- **No crean su propio `this`**, sino que heredan el `this` del contexto léxico (donde fueron definidas).
- **No tienen hoisting** utilizable.
- **Son anónimas** y se asignan a variables.
- No pueden usarse como **constructores** (`new`).
- No tienen su propio objeto `arguments`, `super` ni `new.target`.

**Sintaxis:**

```js
// Forma básica con bloque
const functionName = (parameters) => {
  return value;
};

// Forma compacta (una sola línea, return implícito)
const add = (a, b) => a + b;

// Con un solo parámetro, los paréntesis son opcionales
const square = n => n * n;
```

Ejemplo:

```js
const multiply = (a, b) => a * b;
console.log(multiply(2, 6)); // 12

const greet = name => `Hello ${name}`;
console.log(greet("Juan")); // "Hello Juan"
```

### `this` léxico en funciones de flecha

En las funciones tradicionales, `this` **depende de cómo se invoca la función**.

En cambio, en las **arrow functions**, `this` **se hereda del contexto donde fueron creadas**, lo que las hace ideales para **callbacks**, **temporizadores** o **eventos** dentro de objetos.

```js
const person = {
  name: "Ana",
  greet: function() {
    setTimeout(() => {
      console.log(`Hi, I'm ${this.name}`);
    }, 1000);
  }
};

person.greet(); // "Hi, I'm Ana"
```

>📌 En objetos, se usa la notación de punto (`.`) para acceder a propiedades y métodos.

## Recomendaciones de uso

- **Function Declaration**: prefíerelas cuando necesites **hoisting**, **legibilidad** o funciones **nombradas** y reutilizables.
- **Function Expression**: úsalas cuando necesites **control de alcance**, **declaraciones condicionales** o **callbacks complejos**.
- **Arrow Functions**: son ideales para **funciones cortas**, **callbacks simples** o cuando quieras **preservar el `this` léxico**.
