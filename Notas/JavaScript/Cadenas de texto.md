---
orden: 9
tags:
  - Conversiones
estado: true
---

# Strings en JavaScript

Un **string** (cadena de texto o cadena de caracteres) es un tipo de dato que representa texto. En JavaScript, los strings son **inmutables** (no se pueden modificar directamente) y se pueden declarar de varias formas.

## Declaración de Strings

| Tipo              | Sintaxis      | Ejemplo               |
| ----------------- | ------------- | --------------------- |
| Comillas simples  | `'texto'`     | `'Hello world'`       |
| Comillas dobles   | `"texto"`     | `"Hello world"`       |
| Template Literals | `` `texto` `` | `` `Hello ${name}` `` |

```js
let name = "Armando";
console.log(name); // Armando
```

### Escapar comillas internas

Usa la **barra invertida (`\`)** para incluir comillas dentro de un String.

```js
let phrase = "He said \"Hello\"";
console.log(phrase); // He said "Hello"

// También funciona con comillas simples
let other = 'She\'s happy';
console.log(other); // She's happy
```

## Propiedad `length`

Devuelve la **cantidad de caracteres** (incluye espacios).

```js
let greeting = "Hello Brais !";
console.log(greeting.length); // 13
```

>**⚠️ Nota:** Emojis y algunos caracteres Unicode pueden contar como **más de un carácter** (ej. `"😀"` tiene `length = 2`).

## Acceso por índice

Puedes acceder a caracteres individuales usando `[índice]`. El índice comienza en `0`.

```js
let greeting = "Hello Brais !";
console.log(greeting[0]);   // "H"
console.log(greeting[12]);  // "!"
console.log(greeting[99]);  // undefined (índice fuera de rango)
```

>📌 **Alternativa:** Si utilizas `greeting.charAt(0)` también funciona, pero los corchetes son más comunes.

## Concatenación

Puedes unir Strings de varias formas:

| Método            | Ejemplo                          | Resultado       |
| ----------------- | -------------------------------- | --------------- |
| `+` (operador)    | `"Hello" + " " + "World"`        | `"Hello World"` |
| `+=`              | `let s = "Hello"; s += " World"` | `"Hello World"` |
| Template Literals | `` `Hello ${nombre}` ``          | `"Hola Carlos"` |
| `.concat()`       | `"Hello".concat(" World")`       | `"Hello World"` |

```js
let name = "Brais";
let greeting = "Hello, " + name + "!";
console.log(greeting);           // Hello, Brais!
console.log(typeof greeting);    // string
```

## Métodos Útiles de String

Un método es una función ejecutable que se debe encadenar en este caso con un dato de tipo String.

Se tiene en cuenta los siguientes métodos asociados a un String:

### Búsqueda y verificación

| Método                   | Descripción                                                            | Ejemplo                             |
| ------------------------ | ---------------------------------------------------------------------- | ----------------------------------- |
| `indexOf(subcadena)`     | Devuelve el índice de la **primera coincidencia** o `-1` si no existe. | `"Hello".indexOf("el")` → `1`       |
| `lastIndexOf(subcadena)` | Devuelve el índice de la **última coincidencia**.                      | `"Hello".lastIndexOf("o")` → `4`    |
| `includes(subcadena)`    | `true` si contiene la subcadena.                                       | `"Hello".includes("el")` → `true`   |
| `startsWith(subcadena)`  | `true` si empieza con la subcadena.                                    | `"Hello".startsWith("He")` → `true` |
| `endsWith(subcadena)`    | `true` si termina con la subcadena.                                    | `"Hello".endsWith("lo")` → `true`   |

```js
let texto = "Hello Brais!";
console.log(texto.indexOf("Brais"));    // 5
console.log(texto.includes("MoureDev")); // false
console.log("JavaScript".startsWith("Java")); // true
console.log("script.js".endsWith(".js")); // true
```

### Transformación

| Método                           | Descripción                                 | Ejemplo                                               |
| -------------------------------- | ------------------------------------------- | ----------------------------------------------------- |
| `toUpperCase()`                  | Convierte a mayúsculas.                     | `"hello".toUpperCase()` → `"HELLO"`                   |
| `toLowerCase()`                  | Convierte a minúsculas.                     | `"HELLO".toLowerCase()` → `"hello"`                   |
| `trim()`                         | Elimina espacios al inicio y final.         | `" text ".trim()` → `"text"`                          |
| `trimStart()`                    | Elimina espacios al inicio.                 | `" text".trimStart()` → `"text"`                      |
| `trimEnd()`                      | Elimina espacios al final.                  | `"text ".trimEnd()` → `"text"`                        |
| `replace(buscar, reemplazar)`    | Reemplaza **solo la primera** coincidencia. | `"Hello world".replace("o", "0")` → `"Hell0 World"`   |
| `replaceAll(buscar, reemplazar)` | Reemplaza **todas** las coincidencias.      | `"Hola Mundo".replaceAll("o", "0")` → `"Hell0 W0rld"` |

 ```js
let saludo = "  Hello World  ";
console.log(saludo.trim());                      // "Hello world"
console.log(saludo.toUpperCase());               // "  HELLO WORLD  "
console.log("Hello World".replaceAll("o", "0")); // "Hell0 W0rld"
 ```

### Extracción y división

| Método                   | Descripción                                                             | Ejemplo                                |
| ------------------------ | ----------------------------------------------------------------------- | -------------------------------------- |
| `slice(inicio, fin)`     | Extrae desde `inicio` hasta `fin` (también funciona sin incluir `fin`). | `"Hello".slice(0, 2)` → `"He"`         |
| `substring(inicio, fin)` | Similar a `slice`, pero sin índices negativos.                          | `"Hello".substring(1, 3)` → `"el"`     |
| `split(separador)`       | Divide el string en un **array** usando el separador.                   | `"a,b,c".split(",")` → `["a","b","c"]` |
| `at(indice)`             | Extrae por el `indice` (puede utilizar índices negativos).              | `"Hello".at(-1)` → `"o"`               |

```js
let text = "Hello Brais!";
console.log(text.slice(0, 5));        // "Hello"
console.log("JS,Python,Java".split(",")); // ["JS", "Python", "Java"]
console.log("Hello".split(""));         // ["H", "e", "l", "l", "o"]
```

### Relleno y repetición

| Método                        | Descripción                                       | Ejemplo                           |
| ----------------------------- | ------------------------------------------------- | --------------------------------- |
| `padStart(longitud, relleno)` | Rellena al **inicio** hasta alcanzar la longitud. | `"5".padStart(3, "0")` → `"005"`  |
| `padEnd(longitud, relleno)`   | Rellena al **final** hasta alcanzar la longitud.  | `"JS".padEnd(5, ".")` → `"JS..."` |
| `repeat(n)`                   | Repite el string `n` veces.                       | `"Hi".repeat(3)` → `"HiHiHi"`     |

```js
console.log("5".padStart(3, "0"));   // "005"
console.log("JS".padEnd(5, "."));    // "JS..."
console.log("¡Hey! ".repeat(2));     // "¡Hey! ¡Hey! "
```

## Template Literals (ES6)

Los **Template Literals** son una forma moderna y poderosa de trabajar con Strings. Se definen con **backticks** (`` ` ``) y permiten incluir expresiones.

Una expresión en JavaScript es un fragmento de código que se evalúa y produce un valor como un cálculo o una llamada a una función.

### Incluir expresiones con `${}`

```js
const name = "Carlos";
const age = 25;
const message = `Hello, my name is ${name} and I am ${age} years old.`;
console.log(message); 
// Hello, my name is Carlos and I am 25 years old.
```

### Evaluar expresiones dentro del String

```js
const a = 5, b = 10;
console.log(`Five plus ten is ${a + b}`); 
// Five plus ten is 15
```

### Cadenas multilínea sin concatenación

```js
const multilinea = `This is a line
that spans several lines
and respects the line breaks.`;
console.log(multilinea);
```

### Template Literals anidados

```js
const nivel = 3;
const mensaje = `The level is ${nivel > 5 ? 'advanced' : 'basic'}`;
console.log(mensaje); // The level is basic
```
