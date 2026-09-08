---
orden: 26
tags:
  - Condiciones
Comentario:
estado: true
---

## Bucles en JavaScript

Los bucles permiten ejecutar un bloque de código **repetidamente** mientras se cumpla una condición. JavaScript ofrece varias estructuras adaptadas a diferentes necesidades.

### Bucle `for`

Se utiliza cuando **se conoce la cantidad exacta de iteraciones** (por ejemplo, al recorrer arreglos). Proporciona control preciso sobre el inicio, la condición y el paso.

Sintaxis:

```js
for (initialization; condition; update) {
  // código a ejecutar
}
```

Ejemplo:

```js
const numbers = [1, 2, 3, 4, 5];

for (let i = 0; i < numbers.length; i++) {
  console.log(`Element ${i + 1}: ${numbers[i]}`);
}
// Element 1: 1, Element 2: 2, Element 3: 3, Element 4: 4, Element 5: 5
```

### Bucle `while`

Ejecuta un bloque de código **mientras** la condición sea `true`. La condición se evalúa **antes** de cada iteración, por lo que puede que no se ejecute nunca.

Sintaxis:

```js
while (condition) {
  // código a ejecutar
}
```

Ejemplo:

```js
let counter = 0;
while (counter < 5) {
  console.log(counter); // 0, 1, 2, 3, 4
  counter++;
}
```

> ⚠️ **Importante:** Si la condición nunca se vuelve `false`, se genera un **bucle infinito**.

```js
let counter = 0;
while (counter < 5) {
  console.log(counter); // ¡Infinito! Falta counter++
}
```

### Bucle `do...while`

Similar a `while`, pero **se ejecuta al menos una vez**, ya que la condición se evalúa **al final** de cada iteración.

Sintaxis:

```js
do {
  // código a ejecutar
} while (condition);
```

Ejemplo:

```js
let counter = 0;
do {
  console.log(counter); // 0, 1, 2, 3, 4
  counter++;
} while (counter < 5);
```

>**Uso típico:** Validar entrada de usuario o ejecutar código al menos una vez antes de verificar una condición.

## Control de Bucles: `break` y `continue`

Puedes utilizar las siguientes palabras clave dentro de un bucle:

### `break` – Termina el bucle inmediatamente

```js
for (let i = 0; i < 10; i++) {
  if (i === 5) break; // Sale del bucle cuando i es 5
  console.log(i); // 0, 1, 2, 3, 4
}
```

### `continue` – Salta a la siguiente iteración

```js
for (let i = 0; i < 5; i++) {
  if (i === 2) continue; // Omite la iteración cuando i es 2
  console.log(i); // 0, 1, 3, 4
}
```

>**Recomendación:** Usa `break` y `continue` con moderación, ya que pueden reducir la legibilidad si se abusa de ellos.

## Bucles para Arreglos y Objetos

A partir de la versión ES6 de JavaScript, se tiene en cuenta los siguientes bucles:

### `for...of` – Iterar sobre valores de iterables

Ideal para **arreglos**, **strings** y otros **iterables**. Es más limpio que el `for` tradicional porque no requiere manejar índices.

Sintaxis:

```js
for (const element of iterable) {
  // código a ejecutar
}
```

Ejemplo:

```js
const fruits = ["apple", "banana", "grape"];

for (const fruit of fruits) {
  console.log(fruit); // "apple", "banana", "grape"
}
```

> ❌ `for...of` **no funciona** con objetos literales (no son iterables).

### `for...in` – Iterar sobre propiedades de objetos

Recorre las **propiedades enumerables** de un objeto. No se recomienda usarlo con arreglos, ya que puede incluir propiedades heredadas.

Sintaxis:

```js
for (const key in object) {
  // código a ejecutar
}
```

Ejemplo:

```js
const person = { name: "John", age: 30 };

for (const key in person) {
  console.log(`${key}: ${person[key]}`); // "name: John", "age: 30"
}
```

>⚠️ **Evita** usar `for...in` en arreglos; prefiere `for...of` o métodos como `.forEach()`.

## Buenas prácticas con estructuras de bucle

- **Actualiza la condición** dentro del bucle para evitar bucles infinitos.
- **Prefiere métodos funcionales** como `.forEach()`, `.map()` o `.filter()` cuando sea posible, ya que mejoran la claridad.
- Usa **`for...of`** para recorrer elementos de arreglos de forma legible.
- Usa **`for...in`** solo para objetos simples y sin prototipos modificados.
- **Modera el uso de `break` y `continue`** para no romper el flujo natural del bucle.

```js
// Ejemplo con forEach()
const fruits = ["apple", "banana", "grape"];
fruits.forEach((fruit, index) => {
  console.log(`Fruit ${index + 1}: ${fruit}`);
});
// Fruit 1: apple, Fruit 2: banana, Fruit 3: grape
```
