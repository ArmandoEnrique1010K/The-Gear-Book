---
orden:
tags:
estado: false
---
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
