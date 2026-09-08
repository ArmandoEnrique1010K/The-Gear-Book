---
orden: 23
tags:
  - Arreglos
Comentario:
estado: true
---

## Constructor `Array`

Permite crear arreglos utilizando el constructor global `Array`.

```js
const cars = new Array('BMW', 'Mercedes Benz', 'Volvo');
console.log(cars);
// ['BMW', 'Mercedes Benz', 'Volvo']
```

### Crear arreglos con espacios vacíos

El constructor `Array` también puede utilizarse indicando únicamente la longitud inicial.

```js
const numbers = new Array(5);
console.log(numbers);
// [ <5 empty items> ]
```

> **Importante:** `new Array(5)` no crea valores `undefined`, sino **espacios vacíos internos** (_empty slots_). Estos son diferentes de `undefined`; literalmente no existen como propiedades del arreglo.

### Comportamiento del constructor `Array`

Cuando `Array` recibe un único número, lo interpreta como longitud inicial y **no** como un elemento.

```js
console.log(new Array(3));
// [ <3 empty items> ]

console.log(new Array(3, 4));
// [3, 4] (dos números se tratan como elementos)
```

### Modificar la longitud de un arreglo

Puedes modificar el valor de la propiedad `length` para cambiar el tamaño del arreglo.

```js
const numbers = [1, 2];
numbers.length = 5;
console.log(numbers);
// [1, 2, empty × 3]
```

>**Nota:** Asignar `length = 0` vacía completamente el arreglo.

## Arreglos Dispersos (Sparse Arrays)

JavaScript permite crear arreglos con posiciones vacías.

```js
const cars = [];
cars[0] = 'BMW';
cars[3] = 'Audi';

console.log(cars);
// ['BMW', empty × 2, 'Audi']
```

>**Diferencia clave:** Los espacios vacíos (_empty slots_) son diferentes de `undefined`. Un índice vacío literalmente no existe dentro del arreglo, mientras que `undefined` es un valor asignado explícitamente.

## Comprobación de Arreglos

### Método `Array.isArray()`

La forma **recomendada** para verificar si un valor es realmente un arreglo.

```js
const cars = ['BMW', 'Mercedes Benz'];
console.log(Array.isArray(cars));
// true
```

### Operador `instanceof`

Comprueba si el objeto fue creado a partir de `Array`.

```js
const cars = ['BMW', 'Mercedes Benz'];
console.log(cars instanceof Array);
// true
```

>**Recomendación:** Usa `Array.isArray()` en lugar de `instanceof`, ya que funciona correctamente incluso con arreglos de otros contextos (como iframes).

## Conversión entre Arreglo y Texto

### `join()` – Arreglo a texto

Convierte un arreglo a string con un separador personalizado.

```js
const cars = ['BMW', 'Audi', 'Volvo'];
console.log(cars.join(' - '));
// "BMW - Audi - Volvo"
```

### `toString()` – Arreglo a texto automático

Convierte automáticamente el arreglo a texto separado por comas.

```js
const cars = ['BMW', 'Audi', 'Volvo'];
console.log(cars.toString());
// "BMW,Audi,Volvo"
```

### `split()` – Texto a arreglo

Convierte un string en arreglo usando un delimitador.

```js
const text = 'JavaScript,React,Node';
const technologies = text.split(',');
console.log(technologies);
// ['JavaScript', 'React', 'Node']
```

## Métodos Estáticos para Crear Arreglos

### `Array.from()`

Crea un nuevo arreglo a partir de objetos iterables o estructuras similares a arreglos.

```js
const text = 'Hello';
const letters = Array.from(text);
console.log(letters);
// ['H', 'e', 'l', 'l', 'o']
```

> **Nota:** Un objeto iterable es aquel que puede recorrerse elemento por elemento, como strings, arreglos, Sets o Maps.

### Uso de `Array.from()` con función de mapeo

```js
const numbers = Array.from([1, 2, 3], x => x * 2);
console.log(numbers);
// [2, 4, 6]
```

### `Array.of()`

Crea arreglos a partir de valores individuales, evitando el comportamiento ambiguo del constructor.

```js
const numbers = Array.of(1, 2, 3);
console.log(numbers);
// [1, 2, 3]

// Diferencia con el constructor:
console.log(Array.of(3));  // [3]
console.log(new Array(3)); // [ <3 empty items> ]
```

## El Método `at()` – Acceso desde el Final

Permite acceder a posiciones usando índices positivos o **negativos**.

```js
const cars = ['BMW', 'Audi', 'Volvo'];

console.log(cars.at(0));   // "BMW"
console.log(cars.at(-1));  // "Volvo" (último elemento)
console.log(cars.at(-2));  // "Audi"
```

>**Ventaja:** Los índices negativos comienzan desde el final del arreglo, más legible que `arr[arr.length - 1]`.

## Iteradores de Arreglos (`keys()`, `values()`, `entries()`)

### `keys()` – Recorre índices

```js
const cars = ['BMW', 'Audi', 'Volvo'];

for (const index of cars.keys()) {
  console.log(index);
}
// 0, 1, 2
```

### `values()` – Recorre valores

```js
for (const value of cars.values()) {
  console.log(value);
}
// 'BMW', 'Audi', 'Volvo'
```

### `entries()` – Recorre pares \[índice, valor]

```js
for (const [index, value] of cars.entries()) {
  console.log(index, value);
}
// 0 'BMW', 1 'Audi', 2 'Volvo'
```

## Copias Superficiales (Shallow Copies)

### Copia por referencia (¡Cuidado!)

Los arreglos se copian por referencia, no por valor.

```js
const original = ['BMW', 'Audi'];
const copy = original;  // Ambos apuntan al mismo arreglo

copy[0] = 'Volvo';
console.log(original);
// ['Volvo', 'Audi'] (el original también cambió)
```

### Crear una copia independiente

```js
const original = ['BMW', 'Audi'];
const copy = [...original];  // Copia superficial
// o: Array.from(original)
// o: original.slice()

copy[0] = 'Volvo';
console.log(original);
// ['BMW', 'Audi'] (original intacto)
```

### Copia superficial con objetos anidados

```js
const original = [{ name: 'John' }];
const copy = Array.from(original);

copy[0].name = 'Peter';  // ❌ Modifica el objeto interno

console.log(original[0].name);
// 'Peter' (el objeto interno se comparte)
```

>**Importante:** La copia es **superficial** (_shallow_). Los objetos internos siguen compartiendo referencia. Para copias profundas, usa `structuredClone()` o librerías como Lodash.

## Buenas practicas con conceptos avanzados de arreglos

- **Usa literales (`[]`) siempre que sea posible**: Es la forma más clara, rápida y recomendada para crear arreglos.
- **Prefiere `Array.from()` para conversiones**: Ideal para convertir iterables (como strings, Sets o Maps) en arreglos reales.
- **Usa `Array.of()` en lugar de `new Array()`**: Evita el comportamiento ambiguo del constructor cuando recibe un solo número.
- **Valida arreglos con `Array.isArray()`**: Es el método más fiable y seguro, incluso en contextos multiplataforma.
- **Ten cuidado con la propiedad `length`**: Puedes modificarla manualmente, incluso para vaciar el arreglo (`length = 0`), pero úsalo con precaución.
- **Evita arreglos dispersos (con espacios vacíos)**: Aunque JavaScript lo permite, pueden generar comportamientos inesperados al iterar.
- **Los arreglos pueden contener cualquier tipo de dato**: Números, strings, objetos, funciones, otros arreglos, etc.
- **Copia arreglos de forma explícita**: Usa el operador spread (`...`) o `slice()` para crear copias superficiales y evitar mutaciones accidentales.

