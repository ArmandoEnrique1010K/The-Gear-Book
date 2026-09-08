---
orden: 20
tags:
  - Arreglos
Comentario:
estado: true
---

## Arreglos en JavaScript

Los **arreglos (arrays)** son **estructuras de datos ordenadas** que almacenan una **colección de elementos** de cualquier tipo. La forma recomendada de declararlos es mediante **literales de arreglo**, usando corchetes `[]` y separando los elementos con comas.

>**Buena práctica:** Mantener todos los elementos del mismo tipo (strings, números, objetos, etc.).

```js
const fruits = ["Apple", "Banana", "Cherry"];
const numbers = [1, 2, 3, 4, 5];
```

## Naturaleza de los arreglos

Aunque técnicamente son objetos, su propósito y comportamiento difieren de los objetos literales:

- **Objeto literal:** Organiza datos en **pares clave-valor**.
- **Arreglo:** Contiene una **colección ordenada** de elementos.

```js
const fruits = ["Apple", "Banana", "Cherry"];
console.log(typeof fruits); // "object"
```

### Acceso a elementos

Se accede mediante su **índice**, que comienza en `0`.

```js
const fruits = ["Apple", "Banana", "Cherry"];

console.log(fruits[0]); // "Apple"
console.log(fruits[2]); // "Cherry"
console.log(fruits[3]); // undefined
```

### Propiedad `length`

Devuelve la **cantidad de elementos** del arreglo.

```js
const fruits = ["Apple", "Banana", "Cherry"];
console.log(fruits.length); // 3
```

## Arreglos de objetos

Representa una lista de objetos con la misma estructura. Útil para representar colecciones de elementos similares.

```js
const products = [
  { name: "Keyboard", price: 400, quantity: 2 },
  { name: "Mouse", price: 200, quantity: 1 },
  { name: "Paper", price: 100, quantity: 10 }
];

console.log(products[0].name); // "Keyboard"
```

## Recorrer un arreglo

Puedes iterar en arreglos, de tal manera que puedas acceder a cada valor o elemento del arreglo.

### Bucle `for` clásico

Control total sobre el índice (`i`). Permite acceder a elementos específicos, modificar el arreglo, recorrer en orden inverso o con saltos personalizados.

```js
const fruits = ["Apple", "Banana", "Cherry"];

for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```

### Bucle `for...of`

Itera directamente sobre los **valores** del arreglo, sin índice. No permite modificar el arreglo directamente.

```js
const fruits = ["Apple", "Banana", "Cherry"];

for (const fruit of fruits) {
  console.log(fruit);
}
```

### Método `forEach`

Ejecuta una función por cada elemento. No devuelve un nuevo arreglo y no permite `break` o `continue`.

```js
const fruits = ["Apple", "Banana", "Cherry"];

fruits.forEach((fruit) => console.log(fruit));
```

## Desestructuración de arreglos

La desestructuración permite extraer valores y asignarlos a variables usando la **posición** de los elementos.

```js
const fruits = ["Apple", "Pear", "Cherry"];

const [first, second] = fruits;

console.log(first);  // "Apple"
console.log(second); // "Pear"
```

### Omitir elementos

Puedes omitir posiciones dejando comas vacías.

```js
const fruits = ["Apple", "Pear", "Cherry"];

const [first, , third] = fruits;
console.log(third); // "Cherry"
```

>**Nota:** La desestructuración usa la **posición**, no el nombre de la variable.

## Operador rest (`...`)

Agrupa los **elementos restantes** en un nuevo arreglo durante la desestructuración.

```js
const fruits = ["Apple", "Pear", "Cherry"];
const [first, ...rest] = fruits;

console.log(first); // "Apple"
console.log(rest);  // ["Pear", "Cherry"]
```

## Operador spread (`...`)

Se usa para **copiar, combinar o expandir** elementos de un arreglo (iterables).

```js
const fruits = ["Apple", "Pear", "Cherry"];
const extras = ["Grape", "Watermelon"];

// Copia
const copyFruits = [...fruits];
console.log(copyFruits); // ["Apple", "Pear", "Cherry"]

// Combinar
const allFruits = [...fruits, ...extras];
console.log(allFruits); // ["Apple", "Pear", "Cherry", "Grape", "Watermelon"]

// Añadir elementos
const newFruits = [...fruits, "Strawberry"];
console.log(newFruits); // ["Apple", "Pear", "Cherry", "Strawberry"]
```

> Recuerda que el operador **Rest** agrupa elementos restantes en una desestructuración, mientras que el operador **Spread** expande elementos de un arreglo existente.

## Arreglos Multidimensionales

Un arreglo que contiene otros arreglos como elementos internos, permitiendo representar matrices, tablas o datos organizados en filas y columnas.

```js
const matrix = [
  [1, 2],
  [3, 4],
  [5, 6]
];

console.log(matrix[1][0]); // 3 (fila 1, columna 0)

// Recorrer una matriz
for (let i = 0; i < matrix.length; i++) {
  for (let j = 0; j < matrix[i].length; j++) {
    console.log(`matrix[${i}][${j}] = ${matrix[i][j]}`);
  }
}
```
