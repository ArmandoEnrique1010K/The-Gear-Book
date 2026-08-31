---
orden: 11
tags:
  - Conversiones
---

## Redondeo de Decimales

Puedes optar por uno de los siguientes métodos según tus necesidades:

### `toFixed(decimales)`

Redondea un número a un número fijo de decimales y devuelve un **String**.

```js
console.log((3.14159).toFixed(3)); // "3.142" (redondea)
console.log((3.14159).toFixed(2)); // "3.14"
console.log((3.14159).toFixed(1)); // "3.1"
console.log((3.14159).toFixed(0)); // "3"
```

### `toPrecision(digitos)`

Redondea a un número específico de **dígitos significativos**.

```js
console.log((123.456).toPrecision(4)); // "123.5"
console.log((123.456).toPrecision(2)); // "1.2e+2" (notación científica para pocos dígitos)
console.log((0.000123456).toPrecision(3)); // "0.000124"
console.log((0.000123456).toPrecision(5)); // "0.00012346"
```

### `Math.round()`

Redondea a un número específico de decimales sin convertir a String:

```js
function redondearA(decimales, valor) {
  const factor = Math.pow(10, decimales);
  return Math.round(valor * factor) / factor;
}

console.log(redondearA(2, 3.14159)); // 3.14
console.log(redondearA(3, 3.14159)); // 3.142
console.log(redondearA(4, 3.14159)); // 3.1416
console.log(redondearA(0, 3.14159)); // 3
```

## Convertir de String a número

| Método                  | Descripción          | Ejemplo                          |
| ----------------------- | -------------------- | -------------------------------- |
| `Number(valor)`         | Convierte a número.  | `Number("3.14")` → `3.14`        |
| `parseFloat(valor)`     | Convierte a decimal. | `parseFloat("3.14abc")` → `3.14` |
| `parseInt(valor, base)` | Convierte a entero.  | `parseInt("3.14", 10)` → `3`     |
| `+` (unario)            | Conversión rápida.   | `+"3.14"` → `3.14`               |

```js
let decimal = Number((3.14159).toFixed(2));
console.log(decimal);              // 3.14 (ahora es número)
console.log(typeof decimal);       // "number"

let entero = parseInt("3.14", 10);
console.log(entero);               // 3
```

## Problemas con Decimales

JavaScript usa el estándar **IEEE 754** (doble precisión de 64 bits), lo que causa **errores de precisión** en operaciones con decimales:

```js
console.log(0.1 + 0.2); // 0.30000000000000004 (¡NO es 0.3!)
console.log(0.1 + 0.2 === 0.3); // false
console.log(0.3 - 0.1); // 0.19999999999999998
console.log(0.1 * 0.2); // 0.020000000000000004
console.log(0.3 / 0.1); // 2.9999999999999996
```

Puedes optar por una de las siguientes soluciones:

### Redondear con `toFixed()`

```js
const resultado = 0.1 + 0.2;
console.log(Number(resultado.toFixed(2))); // 0.3
```

### Multiplicar por potencia de 10

```js
const resultado = (0.1 * 10 + 0.2 * 10) / 10;
console.log(resultado); // 0.3
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

### Generar número aleatorio en rango (entero)

```js
function numeroAleatorio(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

console.log(numeroAleatorio(5, 15)); // Entre 5 y 15
```

### Generar número aleatorio en rango (decimal)

```js
function aleatorioDecimal(min, max) {
  return Math.random() * (max - min) + min;
}

console.log(aleatorioDecimal(5, 15)); // Entre 5 y 15 (decimal)
```

### Validar si un valor es un número válido

```js
function esNumeroValido(valor) {
  return typeof valor === 'number' && !Number.isNaN(valor) && isFinite(valor);
}

console.log(esNumeroValido(123));     // true
console.log(esNumeroValido(NaN));     // false
console.log(esNumeroValido(Infinity)); // false
console.log(esNumeroValido("123"));    // false
```

### Contar el número de decimales

```js
function contarDecimales(valor) {
  if (!Number.isFinite(valor)) return 0;
  const str = valor.toString();
  const decimalPart = str.split('.')[1];
  return decimalPart ? decimalPart.length : 0;
}

console.log(contarDecimales(3.14159)); // 5
console.log(contarDecimales(3.0));     // 0
console.log(contarDecimales(123));     // 0
```

## Formato de números

JavaScript ofrece varias formas de formatear números para mostrarlos de manera legible según el contexto.

El objeto `Intl.NumberFormat`es la **herramienta más potente y flexible** para formatear números en JavaScript. Soporta internacionalización, monedas, unidades, porcentajes y más.

| Opción                     | Valores Posibles                                           | Descripción                       | Ejemplo                 |
| -------------------------- | ---------------------------------------------------------- | --------------------------------- | ----------------------- |
| `style`                    | `'decimal'`, `'currency'`, `'percent'`, `'unit'`           | Tipo de formato.                  | `'currency'`            |
| `currency`                 | Código ISO (ej: `'USD'`, `'EUR'`, `'JPY'`)                 | Moneda a usar.                    | `'USD'`                 |
| `currencyDisplay`          | `'symbol'`, `'code'`, `'name'`                             | Cómo mostrar la moneda.           | `'symbol'` → `$`        |
| `useGrouping`              | `true` o `false`                                           | Separadores de miles.             | `true` → `1,234.56`     |
| `minimumIntegerDigits`     | `1` a `21`                                                 | Mínimo de dígitos enteros.        | `3` → `001`             |
| `minimumFractionDigits`    | `0` a `20`                                                 | Mínimo de decimales.              | `2` → `1,234.56`        |
| `maximumFractionDigits`    | `0` a `20`                                                 | Máximo de decimales.              | `2` → `1,234.56`        |
| `minimumSignificantDigits` | `1` a `21`                                                 | Mínimo de dígitos significativos. | `3` → `123`             |
| `maximumSignificantDigits` | `1` a `21`                                                 | Máximo de dígitos significativos. | `3` → `123`             |
| `notation`                 | `'standard'`, `'scientific'`, `'engineering'`, `'compact'` | Notación del número.              | `'compact'` → `1.2K`    |
| `unit`                     | Unidades (ej: `'kilometer'`, `'mile'`)                     | Unidad a mostrar.                 | `'kilometer'`           |
| `unitDisplay`              | `'long'`, `'short'`, `'narrow'`                            | Cómo mostrar la unidad.           | `'long'` → `kilometers` |

```js
// Formato básico
const formateador = new Intl.NumberFormat('es-ES');
console.log(formateador.format(1234567.89)); // "1.234.567,89"

// Formato de moneda (USD)
const usd = new Intl.NumberFormat('en-US', {
  style: 'currency',
  currency: 'USD',
  minimumFractionDigits: 2,
  maximumFractionDigits: 2,
});
console.log(usd.format(1234.5)); // "$1,234.50"

// Formato de moneda (Euro) - distintas formas de mostrar
const eurSymbol = new Intl.NumberFormat('es-ES', {
  style: 'currency',
  currency: 'EUR',
  currencyDisplay: 'symbol',
});
console.log(eurSymbol.format(1234.5)); // "1.234,50 €"

const eurCode = new Intl.NumberFormat('es-ES', {
  style: 'currency',
  currency: 'EUR',
  currencyDisplay: 'code',
});
console.log(eurCode.format(1234.5)); // "1.234,50 EUR"

const eurName = new Intl.NumberFormat('es-ES', {
  style: 'currency',
  currency: 'EUR',
  currencyDisplay: 'name',
});
console.log(eurName.format(1234.5)); // "1.234,50 euros"

// Formato de porcentaje
const porcentaje = new Intl.NumberFormat('en-US', {
  style: 'percent',
  minimumFractionDigits: 1,
  maximumFractionDigits: 2,
});
console.log(porcentaje.format(0.1234)); // "12.34%"
console.log(porcentaje.format(1));      // "100.00%"

// Formato con unidades
const unidadLarga = new Intl.NumberFormat('es-ES', {
  style: 'unit',
  unit: 'kilometer',
  unitDisplay: 'long',
});
console.log(unidadLarga.format(5.5)); // "5,5 kilómetros"

const unidadCorta = new Intl.NumberFormat('en-US', {
  style: 'unit',
  unit: 'mile',
  unitDisplay: 'short',
});
console.log(unidadCorta.format(10.5)); // "10.5 mi"

// Notación compacta (abreviaturas)
const compacto = new Intl.NumberFormat('en-US', {
  notation: 'compact',
  compactDisplay: 'short',
});
console.log(compacto.format(1234567)); // "1.2M"
console.log(compacto.format(1234));    // "1.2K"

// Notación científica
const cientifica = new Intl.NumberFormat('en-US', {
  notation: 'scientific',
  maximumFractionDigits: 2,
});
console.log(cientifica.format(1234567)); // "1.23E6"

// Sin separadores de miles
const sinSeparadores = new Intl.NumberFormat('es-ES', {
  useGrouping: false,
  minimumFractionDigits: 2,
});
console.log(sinSeparadores.format(1234.56)); // "1234,56"

// Relleno con ceros a la izquierda
const conCeros = new Intl.NumberFormat('en-US', {
  minimumIntegerDigits: 5,
  minimumFractionDigits: 2,
});
console.log(conCeros.format(123.45)); // "00,123.45"

// Control de dígitos significativos
const significativos = new Intl.NumberFormat('en-US', {
  minimumSignificantDigits: 3,
  maximumSignificantDigits: 5,
});
console.log(significativos.format(123.456)); // "123.456"
console.log(significativos.format(0.000123456)); // "0.00012346"
```
