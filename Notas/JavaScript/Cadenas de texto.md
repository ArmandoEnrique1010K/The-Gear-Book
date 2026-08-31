---
orden: 9
tags:
  - Conversiones
---

# Strings en JavaScript

Un **string** (cadena de texto o cadena de caracteres) es un tipo de dato que representa texto. En JavaScript, los strings son **inmutables** (no se pueden modificar directamente) y se pueden declarar de varias formas.

## Declaración de Strings

| Tipo              | Sintaxis      | Ejemplo                |
| ----------------- | ------------- | ---------------------- |
| Comillas simples  | `'texto'`     | `'Hola mundo'`         |
| Comillas dobles   | `"texto"`     | `"Hola mundo"`         |
| Template Literals | `` `texto` `` | `` `Hola ${nombre}` `` |

```js
let nombre = "Armando";
console.log(nombre); // Armando
```

### Escapar comillas internas

Usa la **barra invertida (`\`)** para incluir comillas dentro de un String.

```js
let frase = "He said \"Hello\"";
console.log(frase); // He said "Hello"

// También funciona con comillas simples
let otra = 'She\'s happy';
console.log(otra); // She's happy
```

## Propiedad `length`

Devuelve la **cantidad de caracteres** (incluye espacios).

```js
let greeting = "Hola Brais !";
console.log(greeting.length); // 12
```

>**⚠️ Nota:** Emojis y algunos caracteres Unicode pueden contar como **más de un carácter** (ej. `"😀"` tiene `length = 2`).

## Acceso por índice

Puedes acceder a caracteres individuales usando `[índice]`. El índice comienza en `0`.

```js
let greeting = "Hola Brais !";
console.log(greeting[0]);   // "H"
console.log(greeting[11]);  // "!"
console.log(greeting[99]);  // undefined (índice fuera de rango)
```

>📌 **Alternativa:** Si utilizas `greeting.charAt(0)` también funciona, pero los corchetes son más comunes.

## Concatenación

Puedes unir Strings de varias formas:

| Método            | Ejemplo                         | Resultado       |
| ----------------- | ------------------------------- | --------------- |
| `+` (operador)    | `"Hola" + " " + "Mundo"`        | `"Hola Mundo"`  |
| `+=`              | `let s = "Hola"; s += " Mundo"` | `"Hola Mundo"`  |
| Template Literals | `` `Hola ${nombre}` ``          | `"Hola Carlos"` |
| `.concat()`       | `"Hola".concat(" Mundo")`       | `"Hola Mundo"`  |

```js
let nombre = "Brais";
let saludo = "Hola, " + nombre + "!";
console.log(saludo); // Hola, Brais!
console.log(typeof saludo); // string
```

## Métodos Útiles de String

Un método es una función ejecutable que se debe encadenar en este caso con un dato de tipo String.

Se tiene en cuenta los siguientes métodos asociados a un String:

### Búsqueda y verificación

| Método                   | Descripción                                                            | Ejemplo                            |
| ------------------------ | ---------------------------------------------------------------------- | ---------------------------------- |
| `indexOf(subcadena)`     | Devuelve el índice de la **primera coincidencia** o `-1` si no existe. | `"Hola".indexOf("ol")` → `1`       |
| `lastIndexOf(subcadena)` | Devuelve el índice de la **última coincidencia**.                      | `"Hola".lastIndexOf("a")` → `3`    |
| `includes(subcadena)`    | `true` si contiene la subcadena.                                       | `"Hola".includes("ol")` → `true`   |
| `startsWith(subcadena)`  | `true` si empieza con la subcadena.                                    | `"Hola".startsWith("Ho")` → `true` |
| `endsWith(subcadena)`    | `true` si termina con la subcadena.                                    | `"Hola".endsWith("la")` → `true`   |

```js
let texto = "Hola Brais!";
console.log(texto.indexOf("Brais"));    // 5
console.log(texto.includes("MoureDev")); // false
console.log("JavaScript".startsWith("Java")); // true
console.log("script.js".endsWith(".js")); // true
```

### Transformación

| Método                           | Descripción                                 | Ejemplo                                              |
| -------------------------------- | ------------------------------------------- | ---------------------------------------------------- |
| `toUpperCase()`                  | Convierte a mayúsculas.                     | `"hola".toUpperCase()` → `"HOLA"`                    |
| `toLowerCase()`                  | Convierte a minúsculas.                     | `"HOLA".toLowerCase()` → `"hola"`                    |
| `trim()`                         | Elimina espacios al inicio y final.         | `" texto ".trim()` → `"texto"`                       |
| `trimStart()`                    | Elimina espacios al inicio.                 | `" texto".trimStart()` → `"texto"`                   |
| `trimEnd()`                      | Elimina espacios al final.                  | `"texto ".trimEnd()` → `"texto"`                     |
| `replace(buscar, reemplazar)`    | Reemplaza **solo la primera** coincidencia. | `"Hola Mundo".replace("o", "0")` → `"H0la Mundo"`    |
| `replaceAll(buscar, reemplazar)` | Reemplaza **todas** las coincidencias.      | `"Hola Mundo".replaceAll("o", "0")` → `"H0la Mund0"` |

 ```js
let saludo = "  Hola Mundo  ";
console.log(saludo.trim());          // "Hola Mundo"
console.log(saludo.toUpperCase());   // "  HOLA MUNDO  "
console.log("Hola Mundo".replaceAll("o", "0")); // "H0la Mund0"
 ```

### Extracción y división

| Método                   | Descripción                                                             | Ejemplo                                |
| ------------------------ | ----------------------------------------------------------------------- | -------------------------------------- |
| `slice(inicio, fin)`     | Extrae desde `inicio` hasta `fin` (también funciona sin incluir `fin`). | `"Hola".slice(0, 2)` → `"Ho"`          |
| `substring(inicio, fin)` | Similar a `slice`, pero sin índices negativos.                          | `"Hola".substring(1, 3)` → `"ol"`      |
| `split(separador)`       | Divide el string en un **array** usando el separador.                   | `"a,b,c".split(",")` → `["a","b","c"]` |
| `at(indice)`             | Extrae por el `indice` (puede utilizar índices negativos).              | `"Hola".at(-1)` → `"a"`                |

```js
let texto = "Hola Brais!";
console.log(texto.slice(0, 4));        // "Hola"
console.log("JS,Python,Java".split(",")); // ["JS", "Python", "Java"]
console.log("Hola".split(""));         // ["H", "o", "l", "a"]
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
const nombre = "Carlos";
const edad = 25;
const mensaje = `Hola, mi nombre es ${nombre} y tengo ${edad} años.`;
console.log(mensaje); 
// Hola, mi nombre es Carlos y tengo 25 años.
```

### Evaluar expresiones dentro del String

```js
const a = 5, b = 10;
console.log(`Cinco más diez es ${a + b}`); 
// Cinco más diez es 15
```

### Cadenas multilínea sin concatenación

```js
const multilinea = `Esta es una línea
que ocupa varias líneas
y respeta los saltos.`;
console.log(multilinea);
```

### Template Literals anidados

```js
const nivel = 3;
const mensaje = `El nivel es ${nivel > 5 ? 'avanzado' : 'básico'}`;
console.log(mensaje); // El nivel es básico
```
