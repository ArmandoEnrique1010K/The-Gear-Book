---
orden: 22
tags:
  - Arreglos
Comentario:
estado: true
---

## Métodos para agregar y eliminar elementos (mutables)

| Método             | Acción                                        | Mutación |
| ------------------ | --------------------------------------------- | -------- |
| `push(element)`    | Agrega un elemento al **final** del arreglo.  | Sí       |
| `pop()`            | Elimina el **último** elemento del arreglo.   | Sí       |
| `unshift(element)` | Agrega un elemento al **inicio** del arreglo. | Sí       |
| `shift()`          | Elimina el **primer** elemento del arreglo.   | Sí       |

```js
const fruits = ["Apple", "Pear", "Cherry"];

fruits.push("Kiwi");    // ["Apple", "Pear", "Cherry", "Kiwi"]
fruits.pop();           // ["Apple", "Pear", "Cherry"]
fruits.unshift("Grape"); // ["Grape", "Apple", "Pear", "Cherry"]
fruits.shift();         // ["Apple", "Pear", "Cherry"]
```

## Métodos para cortar, copiar y combinar arreglos

| Método                        | Acción                                                                        | Mutación |
| ----------------------------- | ----------------------------------------------------------------------------- | -------- |
| `slice(start, end)`           | Crea una copia desde el índice `start` hasta `end` (sin incluir este último). | No       |
| `concat(array)`               | Une dos o más arreglos y devuelve uno nuevo.                                  | No       |
| `...array` (Spread)           | Copia o concatena arreglos de forma moderna y legible.                        | No       |
| `splice(start, count, items)` | Elimina, reemplaza o agrega elementos.                                        | Sí       |

```js
const fruits = ["Apple", "Pear", "Cherry"];
const copy = fruits.slice(0, 2); // ["Apple", "Pear"]

const combined = fruits.concat(["Pineapple", "Strawberry"]);
// ["Apple", "Pear", "Cherry", "Pineapple", "Strawberry"]

const extraFruits = ["Pears", "Apples"];
const market = [...fruits, ...extraFruits, "Lettuce", "Potatoes"];
// ["Apple", "Pear", "Cherry", "Pears", "Apples", "Lettuce", "Potatoes"]
```

>**Recomendación:** Usa **Spread** (`...`) en lugar de `concat` cuando sea posible; es más moderno y legible.

### Casos de uso del método `splice`

```js
// Elimina 2 elementos a partir del índice 1
const fruits2 = ["Apple", "Pear", "Cherry", "Kiwi"];
fruits2.splice(1, 2);
// ["Apple", "Kiwi"]

// Agrega "Pear" y "Kiwi" en el índice 1
const fruits3 = ["Apple", "Cherry"];
fruits3.splice(1, 0, "Pear", "Kiwi");
// ["Apple", "Pear", "Kiwi", "Cherry"]

// Reemplaza "Pear" por "Melon"
const fruits4 = ["Apple", "Pear", "Cherry"];
fruits4.splice(1, 1, "Melon");
// ["Apple", "Melon", "Cherry"]

// Elimina todos los elementos desde el índice 2
const fruits5 = ["Apple", "Pear", "Cherry", "Kiwi"];
fruits5.splice(2);
// ["Apple", "Pear"]

// Elimina 2 elementos y agrega 3 en su lugar
const fruits6 = ["Apple", "Pear", "Cherry", "Kiwi"];
fruits6.splice(1, 2, "Melon", "Grape", "Mango");
// ["Apple", "Melon", "Grape", "Mango", "Kiwi"]
```

## Métodos de búsqueda y prueba (inmutables)

| Método                | Acción                                                                      | Mutación |
| --------------------- | --------------------------------------------------------------------------- | -------- |
| `includes(value)`     | Verifica si el arreglo contiene el elemento. Devuelve `true` o `false`.     | No       |
| `indexOf(value)`      | Devuelve el índice del elemento o `-1` si no existe.                        | No       |
| `findIndex(callback)` | Devuelve el **índice** del primer elemento que cumple la condición, o `-1`. | No       |

```js
const fruits = ["Apple", "Melon", "Cherry", "Pineapple", "Strawberry"];
const numbers = [10, 20, 30, 40];

console.log(fruits.includes("Melon"));   // true
console.log(fruits.indexOf("Cherry"));   // 2

const indexGreaterThan25 = numbers.findIndex(num => num > 25);
console.log(indexGreaterThan25);         // 2 (posición del primer número que cumple)
```

## Métodos para aplanar arreglos (inmutables)

| Método              | Acción                                                                                    | Mutación |
| ------------------- | ----------------------------------------------------------------------------------------- | -------- |
| `flat(level)`       | Aplana el arreglo hasta el nivel de profundidad especificado (por defecto, **un nivel**). | No       |
| `flatMap(callback)` | Aplica una función de transformación y aplana el resultado **un nivel**.                  | No       |

```js
const arr = [1, [2, 3], [4, [5]]];
console.log(arr.flat());      // [1, 2, 3, 4, [5]]
console.log(arr.flat(2));     // [1, 2, 3, 4, 5]

const words = ["Hello", "World"];
const result = words.flatMap(word => word.split(""));
console.log(result);
// ["H", "e", "l", "l", "o", "W", "o", "r", "l", "d"]
```

## Métodos de ordenación (mutables)

| Método      | Acción                                                               | Mutación |
| ----------- | -------------------------------------------------------------------- | -------- |
| `sort()`    | Ordena alfabéticamente (por Unicode) o según función de comparación. | Sí       |
| `reverse()` | Invierte el orden de los elementos.                                  | Sí       |

```js
const numbers = [3, 1, 4];
numbers.sort();     // [1, 3, 4] (mutación)
numbers.reverse();  // [4, 3, 1] (mutación)
```

### Orden numérico correcto

Por defecto, `sort` ordena como **strings**. Para ordenar números correctamente, usa una función de comparación.

```js
const numbers = [3, 1, 4, 10, 2];

numbers.sort((a, b) => a - b); // Orden numérico ascendente
console.log(numbers); // [1, 2, 3, 4, 10]
```

### Ordenación inmutable

Para evitar mutaciones, crea una copia antes de ordenar.

```js
const numbers = [3, 1, 4, 10, 2];
const sortedCopy = [...numbers].sort((a, b) => a - b);

console.log(sortedCopy); // [1, 2, 3, 4, 10]
console.log(numbers);    // [3, 1, 4, 10, 2] (original intacto)
```

## Métodos de validación (inmutables)

|Método|Acción|Mutación|
|---|---|---|
|`some(callback)`|Verifica si **al menos un** elemento cumple la condición.|No|
|`every(callback)`|Verifica si **todos** los elementos cumplen la condición.|No|

```js
const numbers = [10, 20, 30];

console.log(numbers.some(num => num > 29)); // true
console.log(numbers.every(num => num > 5)); // true

const products = [
  { name: "Keyboard", price: 400 },
  { name: "Mouse", price: 200 },
  { name: "Monitor", price: 1200 }
];

const hasExpensiveProduct = products.some(p => p.price > 1000);
console.log(hasExpensiveProduct); // true
```

## Método de acumulación (inmutable)

|Método|Acción|Mutación|
|---|---|---|
|`reduce(callback, initial)`|Acumula los elementos en un único valor. El `callback` recibe el acumulador y el elemento actual.|No|

```js
const numbers = [10, 20, 30];

// total = acumulador, num = elemento actual
const sum = numbers.reduce((total, num) => total + num, 0);
console.log(sum); // 60
```

### Agrupar elementos con `reduce`

El método `reduce()` también puede construir un objeto a partir de un arreglo de objetos.

```js
const products = [
  { name: "Laptop", category: "Technology" },
  { name: "Mouse", category: "Technology" },
  { name: "Chair", category: "Home" }
];

const grouped = products.reduce((acc, product) => {
  if (!acc[product.category]) {
    acc[product.category] = [];
  }
  acc[product.category].push(product.name);
  return acc;
}, {});

console.log(grouped);
// {
//   Technology: ["Laptop", "Mouse"],
//   Home: ["Chair"]
// }
```

## Mutabilidad vs Inmutabilidad

- **Métodos que Mutan el arreglo original:** `push()`, `pop()`,`shift()`, `unshift()`, `splice()`, `sort()`, `reverse()`.
- **Métodos Inmutables (crean un nuevo arreglo):** `map()`, `filter()`, `find()`, `findIndex()`, `concat(), slice(), flat(), flatMap(), reduce()`, `some()`, `every()`, `includes()`, `indexOf()`.

> **Principio clave:** Para mantener un código predecible y evitar efectos secundarios, prefiere los métodos inmutables siempre que sea posible, especialmente en frameworks como React.
