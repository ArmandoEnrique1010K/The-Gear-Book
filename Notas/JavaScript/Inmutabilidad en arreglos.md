---
orden: 21
tags:
  - Arreglos
Comentario:
estado: true
---

## Modificación directa (mutación)

Puedes acceder al índice de un elemento para modificarlo, pero esto **muta el arreglo original**.

```js
const technologies = ["HTML", "CSS", "JavaScript", "React.js", "Node.js"];
// Esto muta el arreglo original:
technologies[4] = "Nest.js";
console.log(technologies);
// ["HTML", "CSS", "JavaScript", "React.js", "Nest.js"]
```

## Eliminación directa (mutación)

Métodos como `shift()` eliminan el primer elemento, pero también **mutan el arreglo original**.

```js
const technologies = ["HTML", "CSS", "JavaScript", "React.js", "Node.js"];
// Elimina el primer elemento (mutación)
technologies.shift();
console.log(technologies);
// ["CSS", "JavaScript", "React.js", "Node.js"]
```

## Principio de inmutabilidad

En JavaScript, muchos métodos **modifican (mutan) el arreglo original**. Esto puede causar problemas en entornos como **React**, donde se recomienda **no modificar directamente el estado**.

En su lugar, debemos usar **métodos inmutables** que devuelvan un **nuevo arreglo** sin alterar el original, como `map`, `filter` y `find`.

## Método `map` – Transformación inmutable

**Crea un nuevo arreglo** aplicando una función a cada elemento. Es ideal para transformar datos sin mutar el original.

```js
const fruits = ["Apple", "Banana", "Cherry"];

const newArray = fruits.map((fruit) => fruit);
console.table(newArray);
// ["Apple", "Banana", "Cherry"]
```

> **Tip:** Usa `console.table()` para visualizar arreglos en forma de tabla.

### Modificar un elemento con `map`

Combina `map` con una condición para modificar solo ciertos elementos.

```js
const technologies = ["HTML", "CSS", "JavaScript", "React.js", "Node.js"];

// Solo modifica el elemento que cumple la condición
const modifiedTechnologies = technologies.map(tech =>
  tech === "Node.js" ? "Nest.js" : tech
);

console.log(modifiedTechnologies);
// ["HTML", "CSS", "JavaScript", "React.js", "Nest.js"]
```

### Uso común con arreglos de objetos

Por lo general se suele utilizar el método `map` para modificar los elementos de un arreglo que contiene objetos.

```js
const products = [
  { id: 1, name: "Keyboard", price: 400 },
  { id: 2, name: "Mouse", price: 200 }
];

// Actualiza el precio de un producto específico
const updatedProducts = products.map(p =>
  p.id === 2 ? { ...p, price: 250 } : p
);

console.log(updatedProducts);
// [{ id: 1, name: "Keyboard", price: 400 }, { id: 2, name: "Mouse", price: 250 }]
```

## Método `filter` – Filtrado inmutable

Crea un nuevo arreglo con los elementos que **cumplen cierta condición**.

```js
const fruits = ["Apple", "Pear", "Cherry"];

const startsWithC = fruits.filter(f => f.startsWith("C"));

console.log(startsWithC); // ["Cherry"]
```

> **Nota:** `startsWith()` verifica si un string comienza con un carácter dado, devuelve `true` o `false`.

### Eliminar un elemento con `filter`

Usa el operador `!==` para excluir elementos.

```js
const technologies = ["HTML", "CSS", "JavaScript", "React.js", "Node.js"];

const filteredTechnologies = technologies.filter(tech => tech !== "HTML");

console.log(filteredTechnologies);
// ["CSS", "JavaScript", "React.js", "Node.js"]
```

### Uso común con arreglos de objetos

`filter` es uno de los métodos que más se utilizan con arreglos de tipo objeto para buscar elementos que cumplan con la condición.

```js
const products = [
  { id: 1, name: "Keyboard", price: 400 },
  { id: 2, name: "Mouse", price: 200 },
  { id: 3, name: "Monitor", price: 1200 }
];

// Filtra productos con precio > 300
const expensiveProducts = products.filter(p => p.price > 300);

// Elimina un producto por ID
const withoutMouse = products.filter(p => p.id !== 2);

console.log(expensiveProducts);
// [{ id: 1, name: "Keyboard", price: 400 }, { id: 3, name: "Monitor", price: 1200 }]

console.log(withoutMouse);
// [{ id: 1, name: "Keyboard", price: 400 }, { id: 3, name: "Monitor", price: 1200 }]
```

## Método `find` – Búsqueda inmutable

Devuelve el **primer elemento** que cumple la condición, o `undefined` si no existe.

```js
const numbers = [10, 20, 30, 40];

const greaterThan25 = numbers.find(num => num > 25);
console.log(greaterThan25); // 30 (primer número que cumple)
```

### Buscar por identificador en objetos

Es una técnica común en arreglos de objetos, busca un elemento por una de las propiedades del objeto.

```js
const products = [
  { id: 1, name: "Keyboard", price: 400 },
  { id: 2, name: "Mouse", price: 200 },
  { id: 3, name: "Monitor", price: 1200 }
];

const foundProduct = products.find(p => p.id === 2);
console.log(foundProduct);
// { id: 2, name: "Mouse", price: 200 }
```

## Congelar arreglos (`Object.freeze`)

Usa `Object.freeze()` para evitar modificaciones accidentales.

```js
const numbers = Object.freeze([1, 2, 3]);
numbers[0] = 100; // No tiene efecto
console.log(numbers); // [1, 2, 3]
```

## Mutabilidad vs Inmutabilidad

La siguiente comparación muestra la diferencia entre **modificar directamente un arreglo** (mutar) y **crear una nueva versión del mismo** sin alterar el original (inmutabilidad).

Esto es clave para entender cómo mantener un estado predecible en JavaScript o en frameworks como React.

```js
// Mutable (modifica el original)
const a = [1, 2, 3];
a[1] = 99;
console.log(a); // [1, 99, 3]

// Inmutable (crea una nueva copia)
const b = [1, 2, 3];
const c = b.map(x => (x === 2 ? 99 : x));
console.log(b); // [1, 2, 3]  ← original intacto
console.log(c); // [1, 99, 3] ← nuevo arreglo
```

>**Principio clave:** En el enfoque mutable se modifica directamente el arreglo original, lo que puede causar errores difíciles de rastrear. En el enfoque inmutable se crea un nuevo arreglo con nueva referencia en memoria, manteniendo el original intacto y garantizando un comportamiento más predecible.
