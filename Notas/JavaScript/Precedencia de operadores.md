---
orden: 27
tags:
  - Condiciones
Comentario:
estado: true
---

## ¿Qué es la precedencia de operadores?

La **precedencia de operadores** determina el **orden en que JavaScript evalúa los operadores** dentro de una expresión. Cuando una expresión contiene varios operadores, JavaScript los ejecuta según su nivel de precedencia (de mayor a menor). Si dos operadores tienen la misma precedencia, se aplica su **asociatividad** (izquierda o derecha).

## Tabla de Precedencia (de mayor a menor)

| Nivel | Operador                                  | Tipo                              | Asociatividad | Ejemplo        |
| ----- | ----------------------------------------- | --------------------------------- | ------------- | -------------- |
| 1     | `()`                                      | Agrupación                        | —             | `(a + b) * c`  |
| 2     | `++`, `--` (post)                         | Post-incremento / Post-decremento | —             | `a++`          |
| 3     | `!`, `typeof`, `+`, `-`, `++`, `--` (pre) | Unarios                           | Derecha       | `!x`, `-x`     |
| 4     | `**`                                      | Exponenciación                    | Derecha       | `2 ** 3 ** 2`  |
| 5     | `*`, `/`, `%`                             | Multiplicación, división, módulo  | Izquierda     | `a * b / c`    |
| 6     | `+`, `-`                                  | Suma y resta                      | Izquierda     | `a + b - c`    |
| 7     | `<`, `<=`, `>`, `>=`, `in`, `instanceof`  | Relacionales                      | Izquierda     | `a < b`        |
| 8     | \=\=, `!=`, \=\=\=, `!==`                 | Igualdad                          | Izquierda     | `a === b`      |
| 9     | `&&`                                      | AND lógico                        | Izquierda     | `a && b`       |
| 10    | `\|`, `??`                                | OR lógico / Nullish coalescing    | Izquierda     | `a \| b`       |
| 11    | `?:`                                      | Ternario (condicional)            | Derecha       | `cond ? a : b` |
| 12    | `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `**=`  | Asignación                        | Derecha       | `a += 5`       |
| 13    | `,`                                       | Coma                              | Izquierda     | `a = 1, b = 2` |

>**Consejo:** Cuando tengas dudas, **usa paréntesis `()`**. Mejoran la legibilidad y evitan resultados inesperados.

## Ejemplos Prácticos

### Expresiones Aritméticas

```js
let a = 10;
let b = 5;
let c = 2;

let result1 = a + b * c;    // 10 + (5 * 2) = 20
let result2 = (a + b) * c;  // (10 + 5) * 2 = 30
```

### Operadores Lógicos

 ```js
let x = 5;
let y = 10;
let z = 15;

// && tiene mayor precedencia que ||
let logic1 = x < y && y < z || x > z;        // (true && true) || false = true
let logic2 = x < y && (y < z || x > z);      // true && (true || false) = true
 ```

### Asignación vs. Comparación

```js
let a, b;

a = b = 5; // Evaluación de derecha a izquierda: b=5, luego a=b
console.log(a); // 5

// Error común: usar = en lugar de == o ===
if (a = b) { // Asigna b a a, luego evalúa a (5 → truthy)
  console.log("Executes because a=5 is truthy");
}
```

### Operadores Unarios

```js
let x = 5;
let y = 10;

let r1 = -x + y;   // (-5) + 10 = 5
let r2 = !x + y;   // false + 10 = 10 (false se convierte a 0)
```

## Casos Comunes de Confusión

### Concatenación vs. Suma

```js
console.log("5" + 2 + 3); // "523" (concatena todo como string)
console.log(2 + 3 + "5"); // "55" (suma 2+3, luego concatena "5")
console.log(2 + 3 + parseInt("5")); // 10 (suma numérica)
```

### Ternario Anidado (asociatividad derecha)

```js
let age = 20;
let canVote = age >= 18 ? "Yes" : "No"; // "Yes"

let score = 85;
let grade = score >= 90 ? "A" :
            score >= 80 ? "B" :
            score >= 70 ? "C" : "F"; // "B"
```

### Cortocircuito en Operadores Lógicos

```js
function getValue() {
  console.log("Function executed");
  return 10;
}

// && se corta si el primer operando es falsy
false && getValue(); // No ejecuta la función

// || se corta si el primer operando es truthy
true || getValue(); // No ejecuta la función
```

## Buenas Prácticas

### Usa paréntesis para mejorar la claridad

```js
// Menos claro
let result = a + b * c / d;

// Más claro
let result = a + (b * c) / d;
```

### Evita expresiones demasiado complejas

```js
// Difícil de leer
let x = a && b || c ? d : e;

// Mejor
let condition = (a && b) || c;
let x = condition ? d : e;
```

### Ten cuidado con los efectos secundarios

```js
let i = 0;
let arr = [1, 2, 3];

// Incremento dentro de la condición
while (arr[i++] !== undefined) {
  console.log(arr[i - 1]);
}
// Imprime 1, 2, 3
```
