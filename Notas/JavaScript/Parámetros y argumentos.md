---
orden: 13
tags:
  - Funciones
Comentario:
estado: true
---

## Parámetros y argumentos en funciones

Recuerda que en JavaScript, los **parámetros** son las **variables listadas en la definición de una función**, mientras que los **argumentos** son los **valores reales** que se pasan cuando la función es invocada.

```js
// name es un parámetro
function greet(name) {
  console.log("Hola, " + name);
}

// "Juan" es el argumento
greet("Juan"); // "Hello, Juan"
```

## Omitir argumentos

Si una función espera parámetros pero se invoca sin pasar argumentos, esos parámetros reciben el valor `undefined`.

```js
function greet(name) {
  console.log("Hello, " + name);
}

greet(); // "Hello, undefined"
```

## Múltiples parámetros y orden

Una función puede tener varios parámetros. Los argumentos se asignan en el **mismo orden** en que fueron declarados.

```js
function introduce(name, age) {
  console.log(`Hi, my name is ${name} and I am ${age} years old.`);
}

introduce("Carlos", 25); // "Hi, my name Carlos and I am 25 years old."
```

## Valores por defecto (Default Parameters)

Desde ES6, los parámetros pueden tener **valores predeterminados** que se usan cuando no se pasa un argumento o se pasa `undefined`.

- Pueden ser **valores simples**, **expresiones** o incluso **llamadas a funciones**.
- Se evalúan en **tiempo de ejecución**, de izquierda a derecha.

```js
function greet(message = 'Hello', name = 'Guest') {
  return `${message}, ${name}!`;
}

greet();                   // "Hello, Guest!"
greet('Greetings');        // "Greetings, Guest!"
greet('Welcome', 'Ana');   // "Welcome, Ana!"
```

## Retorno de valores (`return`)

**Todas las funciones en JavaScript retornan un valor**. Si no se usa `return`, retornan `undefined` implícitamente.

### Funciones que retornan un valor

```js
const subtract = (a = 0, b = 0) => a - b;
const result = subtract(20, 5);
console.log(result); // 15
```

### Guardar el resultado en una variable

```js
const result = sumar(10, 20);
console.log(result); // 30
```

### Funciones que no retornan valor (procedimientos)

```js
const showMessage = () => {
  console.log("Hello world");
};

showMessage();               // "Hello world"
const result = showMessage();
console.log(result);         // undefined
```

## Patrones comunes de retorno

Las funciones pueden devolver distintos tipos de datos según su propósito:

| Tipo de retorno      | Descripción                            | Ejemplo                              |
| -------------------- | -------------------------------------- | ------------------------------------ |
| **Primitivo**        | `number`, `string`, `boolean`, etc.    | `return x * x;`                      |
| **Objeto o arreglo** | Para devolver múltiples valores        | `return { a: 1, b: 2 };`             |
| **Función**          | Para crear funciones de orden superior | `return () => console.log("Hello");` |
| **Promesa**          | Para operaciones asíncronas            | `return fetch(url);`                 |

```js
// Retorno simple
function square(x) {
  return x * x;
}

// Retorno condicional
function isGreater(a, b) {
  return a > b; // ya retorna true o false
}

// Retorno de objeto (múltiples valores)
function calculateOperations(x) {
  return {
    square: x * x,
    cube: x * x * x
  };
}

// Early return (retorno temprano)
function validateUser(user) {
  if (!user.name) return false;
  if (!user.email) return false;
  return true;
}

console.log(`8 squared is ${square(8)}`);                         // 64
console.log(`10 is greater than 20: ${isGreater(10, 20)}`);       // false
console.log(calculateOperations(3));                              // { square: 9, cube: 27 }

const user = { name: "Armando", email: "ejemplo@correo.com" };
console.log(`¿Valid user?: ${validateUser(user)}`);               // true
```

## Buenas prácticas con parámetros y argumentos

- **Usa valores por defecto** para evitar `undefined` inesperados.
- **Prefiere `return` explícito** en funciones que devuelven datos.
- **Usa early return** para simplificar la lógica condicional.
- **Nombra los parámetros con claridad** para mejorar la legibilidad.
- **Evita modificar los parámetros** directamente (mantén la inmutabilidad cuando sea posible).
