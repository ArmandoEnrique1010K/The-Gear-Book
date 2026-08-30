---
orden: 3
tags:
  - Introducción
---

## Comentarios

Los comentarios son líneas de texto que el motor de JavaScript ignora por completo. Se utilizan para **documentar el código** o para **desactivar temporalmente** partes del mismo sin eliminarlas.

```jsx
// Comentario de una línea (al inicio de la línea)
let name = "Enrique"; // También puede ir al final de una línea

/*
  Comentario multilínea:
  Puede abarcar varias líneas
  y es útil para explicar bloques de código más grandes.
*/
```

## Tipos de comillas para cadenas de texto

En JavaScript, puedes definir cadenas (strings) usando tres tipos de comillas:

- **Comillas simples** (`' '`)
- **Comillas dobles** (`" "`)
- **Comillas inversas o backticks** (`` ` ``) — estas permiten **interpolación** con `${}` y cadenas multilínea.

```jsx
let greeting1 = "Hello world";
let greeting2 = 'Hello world';
let greeting3 = `Hello world`;  // Más versátil: permite ${variable}
```

## El punto y coma (`;`)

El punto y coma es **opcional** en JavaScript gracias al mecanismo **ASI (Automatic Semicolon Insertion)**, que los añade automáticamente en ciertos casos. Sin embargo, **se recomienda usarlo siempre** para evitar errores inesperados.

```jsx
let x = 5; // Correcto
let y = 10 // Funciona, pero menos seguro

// Problema clásico con ASI:
function example() {
  return
    { name: "Juan" }; // Devuelve undefined, porque el salto de línea inserta un ';' después de return
}

// Solución:
function example() {
  return { name: "Juan" }; // Correcto
}
```

>💡 **Buena práctica**: Usa siempre `;` al final de cada sentencia, tanto en JavaScript como en CSS, para evitar bugs difíciles de rastrear.

## Sensibilidad a mayúsculas y minúsculas (Case Sensitive)

JavaScript **distingue entre mayúsculas y minúsculas**. Por lo tanto, `nombre`, `Nombre` y `NOMBRE` son tres variables diferentes.

Esto aplica a:

- **Variables y constantes**
- **Palabras reservadas** (ej. `for` es válido, `For` no lo es)
- **Nombres de funciones y métodos** (ej. `toLowerCase()` es correcto, `tolowercase()` no existe)

```jsx
let age = 25;
let Age = 30; // Variable diferente

console.log(age); // 25
console.log(Age); // 30

// Métodos sensibles a mayúsculas:
console.log("HELLO".toLowerCase()); // "hello"
console.log("hello".toUpperCase()); // "HELLO"
```

## Reglas para nombrar variables

Los nombres de variables deben cumplir estas reglas:

- **Pueden comenzar con**: una letra (a-z, A-Z), el guion bajo (`_`) o el signo de dólar (`$`).
- **No pueden comenzar con**: un número.
- **No pueden ser**: palabras reservadas del lenguaje (como `let`, `if`, `function`, `class`, etc.).

**Convención de estilo**: Se recomienda usar **camelCase** (ej. `miVariable`) para variables y funciones. Aunque `snake_case` (ej. `mi_variable`) funciona, no es la práctica estándar en JavaScript.

```jsx
// Válidos
let _user_;
let $total;
let name1;
let usuarioActivo; // camelCase (recomendado)

// Inválidos
// let 1name;      // Error: comienza con número
// let let;        // Error: palabra reservada
// let my-name;    // Error: guion no permitido
```

## Espacios y saltos de línea

JavaScript **ignora los espacios en blanco y los saltos de línea adicionales**. Esto te permite dar formato al código para que sea más legible, sin afectar su funcionamiento.

```jsx
// Código legible y bien formateado
function add(a, b) {
  return a + b;
}

// Código equivalente pero ilegible
function add(a,b){return a+b;}
```

>✅ Siempre prioriza la legibilidad: usa indentación, espacios y saltos de línea para que tu código sea fácil de entender.

## El código se ejecuta de forma lineal

JavaScript ejecuta el código **de arriba hacia abajo y de izquierda a derecha**, en el orden en que está escrito. Por eso es importante declarar variables y funciones antes de usarlas.

```jsx
// Declaración de variables
let userName = "Carlos";
const PI = 3.1416;

// Definición de función
function greet() {
  return "Hello, " + userName;
}

// Ejecución (se llama después de declarar)
console.log(greet()); // "Hello, Carlos"
```
