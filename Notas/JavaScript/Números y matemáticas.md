---
orden: 10
tags:
  - Conversiones
---

## Tipos de Números en JavaScript

JavaScript solo tiene un tipo de número: **`number`** (IEEE 754, doble precisión de 64 bits). Esto significa que **todos los números son decimales**, aunque parezcan enteros.

| Tipo      | Ejemplo               | Nota                                              |
| --------- | --------------------- | ------------------------------------------------- |
| Enteros   | `42`, `-10`, `0`      | Internamente son decimales sin parte fraccionaria |
| Decimales | `3.14`, `-0.5`, `1.0` | También llamados números de punto flotante        |
| BigInt    | `9007199254740991n`   | Para números enteros **muy grandes** (ES2020)     |

```js
console.log(typeof 42);        // "number"
console.log(typeof 3.14);      // "number"
console.log(typeof 9007199254740991n); // "bigint"
```

## Operaciones Matemáticas Básicas

| Operador | Nombre         | Ejemplo  | Resultado |
| -------- | -------------- | -------- | --------- |
| `+`      | Suma           | `5 + 3`  | `8`       |
| `-`      | Resta          | `10 - 4` | `6`       |
| `*`      | Multiplicación | `7 * 3`  | `21`      |
| `/`      | División       | `15 / 3` | `5`       |
| `%`      | Módulo (resto) | `10 % 3` | `1`       |
| `**`     | Potencia (ES6) | `2 ** 3` | `8`       |

```js
let suma = 5 + 3;          // 8
let resta = 10 - 4;        // 6
let multiplicacion = 7 * 3; // 21
let division = 15 / 3;     // 5
let modulo = 10 % 3;       // 1
let potencia = 2 ** 3;     // 8
```

>**⚠️ Importante:** La división entre `0` no da error, sino `Infinity` o `-Infinity`.

## El Objeto Global `Math`

`Math` es un objeto global que proporciona **métodos y constantes** para operaciones matemáticas avanzadas.

### Redondeo

| Método          | Descripción                                     | Ejemplo                 |
| --------------- | ----------------------------------------------- | ----------------------- |
| `Math.round(x)` | Redondea al entero más cercano (`.5` → arriba). | `Math.round(4.5)` → `5` |
| `Math.floor(x)` | Redondea **hacia abajo** (al entero menor).     | `Math.floor(3.7)` → `3` |
| `Math.ceil(x)`  | Redondea **hacia arriba** (al entero mayor).    | `Math.ceil(4.1)` → `5`  |
| `Math.trunc(x)` | Elimina la parte decimal (trunca).              | `Math.trunc(4.7)` → `4` |

```js
// Comparativa con números negativos
console.log(Math.round(-4.5)); // -4  (redondeo al más cercano)
console.log(Math.floor(-3.7)); // -4  (hacia abajo, más negativo)
console.log(Math.ceil(-4.1));  // -4  (hacia arriba, menos negativo)
console.log(Math.trunc(-4.7)); // -4  (elimina decimal)
```

### Aleatorios

|Método|Descripción|Ejemplo|
|---|---|---|
|`Math.random()`|Número aleatorio entre `0` (incluido) y `1` (excluido).|`0.123456789`|

```js
console.log(Math.random()); // 0.2374 (ejemplo)
```

### Máximos y mínimos

| Método              | Descripción               | Ejemplo                      |
| ------------------- | ------------------------- | ---------------------------- |
| `Math.max(...nums)` | Devuelve el valor máximo. | `Math.max(10, 20, 5)` → `20` |
| `Math.min(...nums)` | Devuelve el valor mínimo. | `Math.min(10, 20, 5)` → `5`  |

```js
// Uso de un array
const numeros = [10, 20, 5];
console.log(Math.max(...numeros)); // 20 (usa spread operator)
console.log(Math.min(...numeros)); // 5
```

### Potencias y raíces

| Método                | Descripción                            | Ejemplo                  |
| --------------------- | -------------------------------------- | ------------------------ |
| `Math.pow(base, exp)` | Potencia.                              | `Math.pow(2, 3)` → `8`   |
| `Math.sqrt(x)`        | Raíz cuadrada.                         | `Math.sqrt(16)` → `4`    |
| `Math.cbrt(x)`        | Raíz cúbica.                           | `Math.cbrt(27)` → `3`    |
| `Math.hypot(...nums)` | Raíz cuadrada de la suma de cuadrados. | `Math.hypot(3, 4)` → `5` |

```js
console.log(Math.pow(2, 3));   // 8
console.log(Math.sqrt(16));    // 4
console.log(Math.cbrt(27));    // 3
console.log(Math.hypot(3, 4)); // 5  (teorema de Pitágoras)
```

### Valor absoluto y signo

| Método         | Descripción                      | Ejemplo                 |
| -------------- | -------------------------------- | ----------------------- |
| `Math.abs(x)`  | Valor absoluto.                  | `Math.abs(-7)` → `7`    |
| `Math.sign(x)` | Devuelve `1`, `-1`, `0` o `NaN`. | `Math.sign(-15)` → `-1` |

```js
console.log(Math.abs(-7));  // 7
console.log(Math.sign(-15)); // -1
console.log(Math.sign(0));  // 0
console.log(Math.sign(NaN)); // NaN
```

### Constantes matemáticas

`Math` también incluye constantes útiles:

| Constante    | Descripción        | Valor                |     |
| ------------ | ------------------ | -------------------- | --- |
| `Math.PI`    | Número Pi          | `3.141592653589793`  |     |
| `Math.E`     | Número de Euler    | `2.718281828459045`  |     |
| `Math.SQRT2` | Raíz cuadrada de 2 | `1.4142135623730951` |     |

```js
console.log(Math.PI);                // 3.141592653589793
console.log(Math.sin(Math.PI / 2));  // 1 (seno de 90°)
```

## Números Especiales

JavaScript tiene valores numéricos especiales que representan casos límite:

| Valor                     | Descripción                                         | Ejemplo                 |
| ------------------------- | --------------------------------------------------- | ----------------------- |
| `NaN`                     | **Not a Number** - resultado de operación inválida. | `"texto" * 2` → `NaN`   |
| `Infinity`                | Infinito positivo.                                  | `10 / 0` → `Infinity`   |
| `-Infinity`               | Infinito negativo.                                  | `-10 / 0` → `-Infinity` |
| `Number.MAX_VALUE`        | Máximo número representable.                        | `1.79e+308`             |
| `Number.MIN_VALUE`        | Mínimo número positivo representable.               | `5e-324`                |
| `Number.MAX_SAFE_INTEGER` | Máximo entero seguro.                               | `9007199254740991`      |
| `Number.MIN_SAFE_INTEGER` | Mínimo entero seguro.                               | `-9007199254740991`     |

```js
console.log("texto" * 2);              // NaN
console.log(10 / 0);                   // Infinity
console.log(-10 / 0);                  // -Infinity
console.log(Number.MAX_VALUE);         // 1.7976931348623157e+308
console.log(Number.MAX_SAFE_INTEGER);  // 9007199254740991
```

## Verificación de Números

| Método                        | Descripción                                            | Ejemplo                                 |
| ----------------------------- | ------------------------------------------------------ | --------------------------------------- |
| `isNaN(valor)`                | **Convierte** a número y verifica si es `NaN`.         | `isNaN("Hola")` → `true`                |
| `Number.isNaN(valor)`         | **No convierte**, solo `true` si es exactamente `NaN`. | `Number.isNaN("Hola")` → `false`        |
| `isFinite(valor)`             | Verifica si es un número finito.                       | `isFinite(100)` → `true`                |
| `Number.isFinite(valor)`      | **No convierte**, verifica si es número finito.        | `Number.isFinite("100")` → `false`      |
| `Number.isInteger(valor)`     | Verifica si es un número entero.                       | `Number.isInteger(10.5)` → `false`      |
| `Number.isSafeInteger(valor)` | Verifica si es un entero seguro.                       | `Number.isSafeInteger(2**53)` → `false` |

```js
console.log(isNaN("Hola"));              // true (convierte "Hola" → NaN)
console.log(Number.isNaN("Hola"));       // false (no convierte)
console.log(isFinite(100));              // true
console.log(Number.isFinite("100"));     // false (no convierte)
console.log(Number.isInteger(10.5));     // false
console.log(Number.isInteger(10));       // true
```

>**✅ Recomendación:** Siempre usa `Number.isNaN()` y `Number.isFinite()` para evitar falsos positivos.
