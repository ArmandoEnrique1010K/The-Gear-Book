---
orden: 4
tags:
  - Datos
estado: true
---

## Declaración de variables y constantes

En JavaScript, las variables y constantes se declaran utilizando tres palabras clave: `var`, `let` y `const`. Cada una tiene características distintas en cuanto a **alcance (scope)**, **mutabilidad** y **comportamiento durante el hoisting**. Elegir la adecuada es fundamental para escribir código predecible y libre de errores.

### `var` (obsoleto, solo para código legacy)

**No se recomienda su uso en código moderno.** Está presente principalmente en código antiguo (legacy) o en entornos que requieren compatibilidad con versiones muy viejas de JavaScript.

- **Alcance**: de **función** (function-scoped).
- **Redeclaración**: permitida.
- **Reasignación**: permitida.
- **Hoisting**: la declaración se eleva, pero la inicialización no; su valor es `undefined` hasta que se asigne.

```javascript
var userName = "Ana";
var userName = "Pedro"; // Redeclaración permitida
userName = "Juan";      // Reasignación permitida

function exampleVar() {
  var x = 10;
  if (true) {
    var x = 20; // Sobrescribe la variable del mismo scope
  }
  console.log(x); // 20
}
```

>⚠️ El comportamiento permisivo de `var` puede provocar errores difíciles de depurar. Por eso, **siempre prefiere `let` o `const`**.

### `let` (para valores mutables)

**Es la opción recomendada cuando necesitas reasignar un valor.** No permite redeclarar en el mismo ámbito, pero sí reasignar.

- **Alcance**: de **bloque** (block-scoped, delimitado por `{}`).
- **Redeclaración**: no permitida en el mismo scope.
- **Reasignación**: permitida.
- **Hoisting**: la declaración se eleva, pero no se puede acceder antes de la inicialización (zona muerta temporal).

```javascript
let age = 25;
// let age = 30; // Error: redeclaración no permitida
age = 30;        // Reasignación permitida

if (true) {
  let counter = 5;
  console.log(counter); // 5
}
// console.log(counter); // Error: counter no está definida fuera del bloque
```

### `const` (para valores constantes)

**Es la palabra clave preferida por defecto.** Se usa para valores que no deben reasignarse. Sin embargo, si el valor es un objeto o array, **sus propiedades internas sí pueden modificarse**.

- **Alcance**: de **bloque** (block-scoped).
- **Redeclaración**: no permitida.
- **Reasignación**: no permitida.
- **Inmutabilidad**: la referencia es fija, pero el contenido interno (objetos/arrays) es mutable.

```javascript
const PI = 3.1416;
// PI = 3.14; // Error: reasignación no permitida

const user = { name: "Luis" };
user.name = "Carlos"; // Permitido: mutación interna
// user = { name: "Ana" }; // Error: reasignación no permitida

const colors = ["red", "green"];
colors.push("blue"); // Permitido: mutación del array
// colors = ["yellow"]; // Error: reasignación no permitida
```

## ¿Cuándo usar cada una?

| **Palabra clave** | **Uso recomendado**                                                                       |
| ----------------- | ----------------------------------------------------------------------------------------- |
| **`const`**       | **Por defecto**, para la mayoría de variables que no cambian su referencia.               |
| **`let`**         | Solo cuando necesites reasignar (ej. contadores, acumuladores, bucles).                   |
| **`var`**         | Evitar por completo en código nuevo. Solo para mantener compatibilidad con código legacy. |

```javascript
const API_KEY = "abc123";     // Valor fijo
let counter = 0;              // Variable mutable

for (let i = 0; i < 5; i++) { // `i` solo existe dentro del bucle
  console.log(i);
}
```

## ¿Qué es el Scope (alcance)?

El **scope** define dónde una variable es accesible dentro del código.

- **Global**: visible en todo el programa.
- **Función**: visible solo dentro de la función donde se declara (`var`).
- **Bloque**: visible solo dentro del bloque `{}` donde se declara (`let`, `const`).

```javascript
if (true) {
  let a = 1;  // scope de bloque
  var b = 2;  // scope de función (o global si está fuera de una función)
}

console.log(b); // 2
// console.log(a); // Error: a is not defined
```

## ¿Qué es el Hoisting?

El **hoisting** es el comportamiento del intérprete de JavaScript que **mueve las declaraciones (no las inicializaciones) a la parte superior de su scope** antes de ejecutar el código.

- Con `var`: la declaración se eleva, pero el valor es `undefined` hasta la asignación.
- Con `let` y `const`: la declaración se eleva, pero **no se puede acceder** antes de la inicialización (zona muerta temporal).

```javascript
// Hoisting con var
console.log(score); // undefined (se eleva, pero sin valor)
var score = 10;

// Hoisting con let/const
// console.log(total); // Error: Cannot access 'total' before initialization
let total = 100;
```

## Nombres de variables en inglés

Es una buena práctica utilizar **nombres en inglés** para variables, funciones y constantes, ya que facilita la colaboración y el mantenimiento en equipos internacionales.

```javascript
// Recomendado
const MAX_USERS = 100;
let userCount = 0;
let isActive = true;

// Evitar (nombres en español o poco descriptivos)
const MAX_USUARIOS = 100;
let contadorUsuarios = 0;
let activo = true;
```
