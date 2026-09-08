---
orden: 24
tags:
  - Condiciones
Comentario:
estado: true
---

## Estructuras Condicionales en JavaScript

Las estructuras condicionales permiten controlar el flujo de ejecución de un programa, tomando decisiones basadas en el valor de una o más condiciones. JavaScript convierte automáticamente cualquier valor a booleano (`true` o `false`) según si es **truthy** o **falsy** (valores falsy: `false`, `0`, `""`, `null`, `undefined`, `NaN`).

## Bloques `if`, `else if` y `else`

Se utilizan para evaluar condiciones secuencialmente. La primera condición que se cumpla ejecutará su bloque y el resto se ignorará.

Sintaxis:

```js
if (condition) {
  // se ejecuta si condition es true
} else if (anotherCondition) {
  // se ejecuta si la anterior es false y esta es true
} else {
  // se ejecuta si ninguna condición anterior es true
}
```

### Solo `if`

Se usa para validar condiciones puntuales. Es común combinarlo con `return` para detener la ejecución en funciones.

```js
let userName = "";

if (!userName) {
  console.log("Name is required");
}

userName = "Enrique";

if (userName) {
  console.log("Valid name:", userName);
}
```

### Bloque `if...else`

Ideal para decisiones binarias (sí/no). Puedes usar operadores lógicos como `&&` (todas las condiciones) y `||` (al menos una).

```js
const balance = 1000;
const amountToPay = 1200;
const hasCreditCard = false;

if (balance >= amountToPay || hasCreditCard) {
  console.log("You can pay");
} else {
  console.log("You cannot pay");
}
```

### Bloque `else if`

Permite encadenar múltiples condiciones. Es útil para rangos o lógica escalonada.

```js
let age = 16;

if (age >= 65) {
  console.log("Senior");
} else if (age >= 18) {
  console.log("Adult");
} else {
  console.log("Minor");
}
```

>**Buenas prácticas:** Coloca las condiciones de **más restrictivas a más generales** para evitar que condiciones amplias bloqueen las más específicas.

## Bloque `switch`

Evalúa una misma expresión contra múltiples valores exactos usando **igualdad estricta (\=\=\=)**. Es más legible que múltiples `if...else` cuando se comparan valores fijos.

Sintaxis:

```js
switch (expression) {
  case value1:
    // código si expression === value1
    break;
  case value2:
    // código si expression === value2
    break;
  default:
    // si ningún caso coincide
}
```

Ejemplo:

```js
let day = 3;
let dayName;

switch (day) {
  case 1:
    dayName = "Monday";
    break;
  case 2:
    dayName = "Tuesday";
    break;
  case 3:
    dayName = "Wednesday";
    break;
  case 6:
  case 7:
    dayName = "Weekend";
    break;
  default:
    dayName = "Invalid day";
}

console.log(dayName); // Wednesday
```

>Puedes agrupar varios `case` que compartan el mismo bloque de código.

## Asignación de valores con condicionales

Tanto `if` como `switch` pueden usarse para asignar valores a variables según una condición.

```js
let temperature = 32;
let weatherStatus;

if (temperature >= 30) {
  weatherStatus = "Hot";
} else if (temperature >= 15) {
  weatherStatus = "Mild";
} else {
  weatherStatus = "Cold";
}

console.log(weatherStatus); // Hot
```

```js
let customerType = "Premium";
let discount;

switch (customerType) {
  case "VIP":
    discount = 20;
    break;
  case "Premium":
    discount = 15;
    break;
  case "Regular":
    discount = 5;
    break;
  default:
    discount = 0;
}

console.log("Discount:", discount + "%");
```

## Patrón Early Return

Consiste en salir de una función tan pronto como se detecta una condición que impide continuar. Esto evita anidaciones profundas y mejora la legibilidad.

```js
function createUser(name, email) {
  if (!name) return "Name is required";
  if (!email) return "Email is required";

  return `User ${name} created with ${email}`;
}

console.log(createUser("Enrique")); // Email is required
```
