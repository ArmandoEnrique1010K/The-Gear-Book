---
tags:
  - Datos
orden: 5
---

## Tipos de datos en JavaScript

JavaScript tiene **8 tipos de datos** (7 primitivos y 1 de referencia). Los **primitivos** son valores inmutables y se almacenan directamente en la variable. Los **objetos** (tipo de referencia) son mutables y se almacenan por referencia.

>💡 **Importante**: los primitivos son inmutables, pero las variables que los contienen pueden reasignarse a nuevos valores.

- Tipos primitivos: `string`, `number`, `boolean`, `null`, `undefined`, `bigint` y `symbol`.
- Tipo de referencia: `object`.

## `string` — Cadena de texto

Representa texto o secuencias de caracteres. Se definen con comillas simples (`'`), dobles (`"`) o backticks (`` ` ``) para **template literals** (permiten interpolación y saltos de línea).

**Inmutables**: no se pueden modificar caracteres individualmente.

```javascript
let firstName = 'Ana';
let email = "correo@example.com";
let greeting = `Hola, ${firstName}`; // Template literal
```

## `number` — Número (entero o decimal)

Representa tanto enteros como decimales (no hay distinción entre `int` y `float` como en otros lenguajes).

- Incluye valores especiales: `NaN` (Not a Number) e `Infinity`.
- **Precisión limitada**: operaciones con decimales pueden tener errores (ej. `0.1 + 0.2 !== 0.3`).

```javascript
let age = 25;
let price = 19.99;
let result = 10 / 0;      // Infinity
let notANumber = "abc" / 2; // NaN
```

## `boolean` — Booleano

Representa un valor lógico: `true` (verdadero) o `false` (falso). Es fundamental en estructuras condicionales (`if`, `while`, etc.).

```javascript
let isAdult = (age >= 18); // true o false

if (isAdult) {
  console.log("Is an adult");
}
```

## `null` — Nulo (ausencia intencional)

Representa la **ausencia intencional de un valor**. Se asigna manualmente para indicar "vacío" o "sin valor".

>⚠️ **Error histórico**: `typeof null` devuelve `"object"` (esto es un bug del lenguaje que no se corrige por compatibilidad).

```javascript
let user = null; // Valor asignado para indicar "vacío"
console.log(typeof null); // "object" (¡Cuidado!)
```

## `undefined` — No definido

Indica que una variable **ha sido declarada pero no inicializada**. Es el valor por defecto de cualquier variable sin asignación explícita.

```javascript
let x;
console.log(x); // undefined
console.log(typeof x); // "undefined"
```

## `bigint` — Número entero muy grande (ES2020)

Se usa para representar números enteros mayores que `2⁵³ - 1` (límite de `number`). Se crea añadiendo `n` al final o usando `BigInt()`.

>⚠️ **No se puede mezclar** con `number` directamente (da error).

```javascript
let bigNum = 9007199254740991n;
let anotherBig = BigInt("12345678901234567890");

console.log(bigNum + 1n); // 9007199254740992n

// 10n + 10; // TypeError: Cannot mix BigInt and number
```

## `symbol` — Símbolo único (ES6)

Genera valores **únicos e inmutables**, ideales para claves privadas en objetos o para evitar colisiones en propiedades.

Cada símbolo es único, incluso si tienen la misma descripción.

```javascript
let id = Symbol("id");
let user = {
  name: "Carlos",
  [id]: 123 // Clave única
};
console.log(user[id]); // 123

const a = Symbol("desc");
const b = Symbol("desc");
console.log(a === b); // false
```

## `object` — Objeto (y derivados)

Los objetos son estructuras de datos que agrupan pares clave-valor. Incluyen:

- Objetos literales (`{}`)
- Arreglos (`[]`)
- Funciones
- Fechas, expresiones regulares, etc.

A diferencia de los primitivos, **los objetos son mutables** y se pasan por referencia.

```javascript
let person = { name: "Luis", age: 30 };
let colors = ["red", "green", "blue"];

person.age = 31; // Mutación permitida
colors.push("yellow"); // Mutación permitida
```

## Verificación de tipos con `typeof`

El operador `typeof` devuelve una cadena con el tipo de dato:

```javascript
console.log(typeof "Hola");        // "string"
console.log(typeof 42);            // "number"
console.log(typeof true);          // "boolean"
console.log(typeof null);          // "object" (⚠️ error histórico)
console.log(typeof undefined);     // "undefined"
console.log(typeof Symbol("id"));  // "symbol"
console.log(typeof 10n);           // "bigint"
console.log(typeof {});            // "object"
console.log(typeof []);            // "object" (los arrays son objetos)
console.log(typeof function(){});  // "function" (caso especial)
```
