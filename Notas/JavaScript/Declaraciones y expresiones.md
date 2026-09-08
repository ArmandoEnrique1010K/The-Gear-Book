---
orden: 25
tags:
  - Condiciones
Comentario:
estado: true
---

## Declaraciones (Statements)

Las declaraciones **realizan una acción** o definen una estructura. No siempre producen un valor directo y suelen terminar con punto y coma (`;`).

**Tipos comunes:**

- **Control de flujo:** `if`, `for`, `while`, `switch`
- **Declaración de variables:** `let`, `const`, `var`
- **Asignación:** `x = 5;`

```js
let name = "John";           // declaración de variable
if (x > 5) {                 // declaración de control
  console.log("Greater than 5");
}
for (let i = 0; i < 3; i++) { // declaración de bucle
  console.log(i);
}
```

## Expresiones (Expressions)

Las expresiones **siempre devuelven un valor**. Pueden ser:

- Operaciones aritméticas (`2 + 2`)
- Comparaciones (`age > 18`)
- Llamadas a funciones (`myFunction()`)
- Accesos a propiedades (`object.property`)

Una expresión puede estar **dentro de una declaración** (por ejemplo, en el lado derecho de una asignación).

```js
2 + 2                // devuelve 4
myFunction()         // devuelve lo que retorne la función
age > 18             // devuelve true o false
person.name          // devuelve el valor de la propiedad
```

## Operador Ternario (`? :`)

El operador ternario es una **expresión condicional** que devuelve un valor. Es ideal para condiciones simples en una sola línea.

Sintaxis:

```js
condition ? expressionIfTrue : expressionIfFalse;
```

Ejemplo:

```js
let age = 20;
let message = age >= 18 ? "Adult" : "Minor";
console.log(message); // "Adult"
```

>**Importante:** El ternario devuelve una **expresión**, no un bloque de código. Si necesitas ejecutar múltiples instrucciones, usa `if...else`.

### Anidamiento de Ternarios

Se pueden anidar para simular la estructura de `else if`, manteniendo el código compacto.

```js
const balance = 1000;
const amountToPay = 1200;
const hasCreditCard = false;

const message =
  balance > amountToPay ? "You can pay" :
  hasCreditCard ? "You can pay with credit card" :
  "You cannot pay";

console.log(message); // "You cannot pay"
```

## Evaluación de Cortocircuito (Short-circuit Evaluation)

La evaluación de cortocircuito detiene la ejecución de una expresión lógica cuando el resultado ya puede determinarse. Es útil para:

- Asignar valores por defecto
- Ejecutar funciones solo si se cumple una condición
- Evitar errores (ej. acceder a propiedades de `null`)

### Operador `||` (OR)

Retorna el **primer valor truthy** que encuentra. Si todos son falsy, retorna el último valor.

```js
// Evaluación de cortocircuito
true || console.log("This won't run");   // true, no ejecuta el log
false || console.log("This will run");   // ejecuta el log

// Asignación de valor por defecto
const user = null;
const userName = user || "Guest";        // userName = "Guest"
```

### Operador `&&` (AND)

Retorna el **primer valor falsy** que encuentra. Si todos son truthy, retorna el último valor.

```js
// Evaluación de cortocircuito
false && console.log("This won't run");  // false, no ejecuta
true && console.log("This will run");    // ejecuta el log

// Ejecución condicional
const isLoggedIn = true;
const showPanel = () => console.log("Panel shown");

const result = isLoggedIn && showPanel(); // Ejecuta solo si isLoggedIn es truthy
console.log(result); // undefined (porque console.log devuelve undefined)
```

>**Nota:** `console.log()` devuelve `undefined` (un valor falsy). Por eso, aunque se ejecute dentro de una expresión lógica, el resultado de la expresión completa puede ser `undefined`.
