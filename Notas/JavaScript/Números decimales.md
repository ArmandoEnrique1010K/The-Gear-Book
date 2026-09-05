---
orden: 11
tags:
  - Conversiones
estado: true
---

## Redondeo de Decimales

Además del uso de `Math.floor()` y `Math.ceil()` para redondear hacia abajo o hacia arriba, puedes optar por uno de los siguientes métodos según tus necesidades:

### `toFixed(decimales)`

Redondea un número a un número fijo de decimales y devuelve un **String**.

```js
console.log((3.14159).toFixed(3)); // "3.142" (redondea)
console.log((3.14159).toFixed(2)); // "3.14"
console.log((3.14159).toFixed(1)); // "3.1"
console.log((3.14159).toFixed(0)); // "3"
```

>⚠️ **Problema común:** `toFixed` puede comportarse de forma inesperada en casos específicos.

```js
// Esto pasa por el mismo problema de precisión de IEEE 754
console.log((1.005).toFixed(2)); // "1.00" (¡debería ser 1.01!)

// Problemas con números grandes
console.log((123456789.12345).toFixed(2)); // "123456789.12"
console.log((0.0000001).toFixed(10)); // "0.0000001000" (añade ceros)
```

### `toPrecision(digitos)`

Redondea a un número específico de **dígitos significativos** (incluye enteros y decimales).

```js
console.log((123.456).toPrecision(4)); // "123.5"
console.log((123.456).toPrecision(2)); // "1.2e+2" (notación científica para pocos dígitos)
console.log((0.000123456).toPrecision(3)); // "0.000124"
console.log((0.000123456).toPrecision(5)); // "0.00012346"
```

### `Math.round()`

Redondea a un número específico de decimales sin convertir a String.

```js
function roundTo(decimals, value) {
  const factor = Math.pow(10, decimals);
  return Math.round(value * factor) / factor;
}

console.log(roundTo(2, 3.14159)); // 3.14
console.log(roundTo(3, 3.14159)); // 3.142
console.log(roundTo(4, 3.14159)); // 3.1416
console.log(roundTo(0, 3.14159)); // 3
```

### `Number.EPSILON`

`Number.EPSILON` representa la **diferencia mínima** entre el número 1 y el siguiente número que puede ser representado en el estándar IEEE 754 de doble precisión.

```js
Number.EPSILON; // 2.220446049250313e-16
```

**En términos prácticos**, es el **margen de error más pequeño** que JavaScript puede detectar en operaciones con números decimales.

Se utiliza para **comparar números decimales** y **corregir errores de redondeo** en cálculos que involucran números fraccionarios.

```js
function roundUpSafely(decimals, value) {
  const factor = Math.pow(10, decimals);
  return Math.round((value + Number.EPSILON) * factor) / factor;
}

function roundTo(decimals, value) {
  const factor = Math.pow(10, decimals);
  return Math.round(value * factor) / factor;
}

console.log(roundUpSafely(2, 1.005));    // 1.01 (evita error)
console.log(roundUpSafely(4, 0.0001));   // 0.0001 
console.log(roundTo(2, 1.005));          // 1 (error de precisión)

```

> **✅ Recomendación:** Se utiliza `Number.EPSILON` en cálculos simples de hasta 3 decimales como máximo, no se recomienda su uso en cálculos financieros o científicos.

## Problemas con Decimales

JavaScript usa el estándar **IEEE 754** (doble precisión de 64 bits), lo que causa **errores de precisión** en operaciones con decimales:

```js
console.log(0.1 + 0.2); // 0.30000000000000004 (¡NO es 0.3!)
console.log(0.1 + 0.2 === 0.3); // false
console.log(0.3 - 0.1); // 0.19999999999999998
console.log(0.1 * 0.2); // 0.020000000000000004
console.log(0.3 / 0.1); // 2.9999999999999996
```

Puedes optar por una de las siguientes soluciones para manejar decimales con precisión:

### Redondear con `toFixed()`

```js
const result = 0.1 + 0.2;
console.log(Number(result.toFixed(2))); // 0.3
```

### Multiplicar por potencia de 10

```js
const result = (0.1 * 10 + 0.2 * 10) / 10;
console.log(result); // 0.3
```

### Usar bibliotecas especializadas

- **Decimal.js** o **Big.js** para cálculos financieros.
- **BigInt** para enteros grandes.

```js
// Ejemplo con BigInt (solo enteros)
const a = 9007199254740991n;
const b = 1n;
console.log(a + b); // 9007199254740992n
```

## Patrones Útiles

Ten en cuenta lo siguiente:

### Generar número aleatorio entero en un rango

```js
function randomNumber(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

console.log(randomNumber(5, 15)); // Entre 5 y 15
```

### Generar número aleatorio decimal en un rango

```js
function randomDecimal(min, max) {
  return Math.random() * (max - min) + min;
}

console.log(randomDecimal(5, 15)); // Entre 5 y 15 (decimal)
```

### Validar si un valor es un número válido

```js
function isValidNumber(value) {
  return typeof value === 'number' && !Number.isNaN(value) && isFinite(value);
}

console.log(isValidNumber(123));     // true
console.log(isValidNumber(NaN));     // false
console.log(isValidNumber(Infinity)); // false
console.log(isValidNumber("123"));    // false
```

### Contar el número de decimales

```js
function countDecimalPlaces(valor) {
  if (!Number.isFinite(valor)) return 0;
  const str = valor.toString();
  const decimalPart = str.split('.')[1];
  return decimalPart ? decimalPart.length : 0;
}

console.log(countDecimalPlaces(3.14159)); // 5
console.log(countDecimalPlaces(3.0));     // 0
console.log(countDecimalPlaces(123));     // 0
```

### Calculo de precio con IVA y redondeo seguro

```js
function calculatePriceIncludingIVA(price, iva = 21) {
  const total = price * (1 + iva / 100);
  return roundTo(2, total); 
}

function roundTo(decimals, value) {
  const factor = Math.pow(10, decimals);
  return Math.round(value * factor) / factor;
}
console.log(calculatePriceIncludingIVA(9.99)); // 12.09
console.log(calculatePriceIncludingIVA(0.99)); // 1.20
```
