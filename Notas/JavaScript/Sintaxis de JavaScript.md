---
number: 3
---

## Comentarios

Los comentarios se usan para documentar código o desactivar partes sin borrarlas, se puede escribir en una sola línea o en varias líneas.

```jsx
// Esto es un comentario (no afecta el código)
let name = "Enrique"; // También puede ir al lado de código

/*
Esto es un comentario
multilínea, que puede 
abarcar varias líneas.
*/
```

## Los tipos de comillas

Puedes definir cadenas de texto utilizando **comillas simples (`'`)**, **comillas dobles (`"`)**, o **comillas inversas (```)**.

```jsx
let greeting1 = "Hello world";
let greeting2 = 'Hello world';
let greeting3 = `Hello world`;
```

## El punto y coma

**Es opcional**, pero se recomienda utilizarlo para evitar errores.

JavaScript los inserta automáticamente en ciertos casos (**ASI: Automatic Semicolon Insertion**), pero puede fallar.

```jsx
let x = 5; // Correcto
let y = 10 // Funciona, pero es mejor con ;

// Problema con ASI:
function example() {
  return
    { name: "Juan" }; // Devuelve `undefined` por el salto de línea
}
```

> Siempre utiliza `;` tanto en archivos JavaScript como en CSS para evitar bugs (errores inesperados).

## Sensibilidad a mayúsculas y minúsculas

JavaScript es **Case Sensitive,** es decir, distingue entre mayúsculas y minúsculas en:

- **Variables**: `nombre` ≠ `Nombre` ≠ `NOMBRE`.
- **Palabras reservadas**: `for` ≠ `For` (este último no es una palabra clave).
- **Funciones y métodos**: `toLowerCase()` ≠ `tolowercase()` (este último se trata de una función definida)

```jsx
let age = 25;
let Age = 30; // Variable diferente

console.log(age); // 25
console.log(Age); // 30

// Métodos de string:
console.log("HELLO".toLowerCase()); // "hello"
console.log("hello".toUpperCase()); // "HELLO"
```

## Nombres de variables

**Los nombres de las variables declaradas deben comenzar** con: `$`, `_` o una letra. No pueden comenzar con números o palabras reservadas en JavaScript: `let`, `if`, `function`, etc.

JavaScript sigue la convención **camelCase** para nombrar variables y funciones. Evita usar nombres como `Nombre_Usuario` (**snake_case**), aunque funcionan, no son un estándar en JavaScript.

```jsx
// Variables validas
let _user_;
let $total;
let name1;

// Variables invalidas
// let 1name;    // Error
// let let;        // Palabra reservada
// let my-name;  // Guión no permitido
```

## Espacios y saltos de línea

**JavaScript ignora espacios en blanco y saltos de línea adicionales**. Solamente se utilizan al momento de escribir código fuente para mejorar la legibilidad.

```jsx
// Código legible:
function add(a, b) {
  return a + b;
}

// Funciona igual (pero es ilegible):
function add(a,b){return a+b;}
```

## El código es lineal

Recuerda que en JavaScript, **el código se ejecuta de arriba hacia abajo y de izquierda a derecha**. En el siguiente ejemplo se han aplicado las bases para escribir código limpio y evitar errores comunes.

```jsx
// Declaración de variables
let username = "Carlos";
const PI = 3.1416;

// Función con retorno
function greet() {
  return "Hello, " + username;
}

// Llamada a función
console.log(greet());
```
