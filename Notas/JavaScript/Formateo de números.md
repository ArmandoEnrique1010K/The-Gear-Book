---
orden: 11.5
tags:
  - Conversiones
Comentario:
estado: true
---

## Formateo de Números en JavaScript

JavaScript ofrece varias formas de formatear números para mostrarlos de manera legible según el contexto. La herramienta más potente y flexible es el objeto **`Intl.NumberFormat`**, que soporta internacionalización, monedas, unidades, porcentajes y más.

Sintaxis:

```js
new Intl.NumberFormat(locale, options)
```

Ejemplo:

```js
const formatter = new Intl.NumberFormat('es-ES');
console.log(formatter.format(1234567.89)); // "1.234.567,89"
```

## Opciones principales de formato

| Opción                     | Valores posibles                                           | Descripción                      | Ejemplo                 |
| -------------------------- | ---------------------------------------------------------- | -------------------------------- | ----------------------- |
| `style`                    | `'decimal'`, `'currency'`, `'percent'`, `'unit'`           | Tipo de formato                  | `'currency'`            |
| `currency`                 | Código ISO (ej: `'USD'`, `'EUR'`, `'JPY'`)                 | Moneda a usar                    | `'USD'`                 |
| `currencyDisplay`          | `'symbol'`, `'code'`, `'name'`                             | Cómo mostrar la moneda           | `'symbol'` → `$`        |
| `useGrouping`              | `true` o `false`                                           | Separadores de miles             | `true` → `1,234.56`     |
| `minimumIntegerDigits`     | `1` a `21`                                                 | Mínimo de dígitos enteros        | `3` → `001`             |
| `minimumFractionDigits`    | `0` a `20`                                                 | Mínimo de decimales              | `2` → `1,234.56`        |
| `maximumFractionDigits`    | `0` a `20`                                                 | Máximo de decimales              | `2` → `1,234.56`        |
| `minimumSignificantDigits` | `1` a `21`                                                 | Mínimo de dígitos significativos | `3` → `123`             |
| `maximumSignificantDigits` | `1` a `21`                                                 | Máximo de dígitos significativos | `3` → `123`             |
| `notation`                 | `'standard'`, `'scientific'`, `'engineering'`, `'compact'` | Notación del número              | `'compact'` → `1.2K`    |
| `unit`                     | Unidades (ej: `'kilometer'`, `'mile'`)                     | Unidad a mostrar                 | `'kilometer'`           |
| `unitDisplay`              | `'long'`, `'short'`, `'narrow'`                            | Cómo mostrar la unidad           | `'long'` → `kilometers` |

## Formato de moneda

### Moneda USD (inglés)

```js
const usd = new Intl.NumberFormat('en-US', {
  style: 'currency',
  currency: 'USD',
  minimumFractionDigits: 2,
  maximumFractionDigits: 2,
});
console.log(usd.format(1234.5)); // "$1,234.50"
```

### Moneda EUR (español) - distintas formas de mostrar

```js
// Símbolo
const eurSymbol = new Intl.NumberFormat('es-ES', {
  style: 'currency',
  currency: 'EUR',
  currencyDisplay: 'symbol',
});
console.log(eurSymbol.format(1234.5)); // "1.234,50 €"

// Código
const eurCode = new Intl.NumberFormat('es-ES', {
  style: 'currency',
  currency: 'EUR',
  currencyDisplay: 'code',
});
console.log(eurCode.format(1234.5)); // "1.234,50 EUR"

// Nombre
const eurName = new Intl.NumberFormat('es-ES', {
  style: 'currency',
  currency: 'EUR',
  currencyDisplay: 'name',
});
console.log(eurName.format(1234.5)); // "1.234,50 euros"
```

### Moneda peruana (SOL)

```js
const pen = new Intl.NumberFormat('es-PE', {
  style: 'currency',
  currency: 'PEN',
  minimumFractionDigits: 2,
});
console.log(pen.format(1234.5)); // "S/ 1,234.50"
```

## Formato de porcentaje

```js
const percent = new Intl.NumberFormat('en-US', {
  style: 'percent',
  minimumFractionDigits: 1,
  maximumFractionDigits: 2,
});
console.log(percent.format(0.1234)); // "12.34%"
console.log(percent.format(1));      // "100.00%"
console.log(percent.format(0.005));  // "0.50%"
```

## Formato con unidades

```js
// Unidades en formato largo (español)
const unitLong = new Intl.NumberFormat('es-ES', {
  style: 'unit',
  unit: 'kilometer',
  unitDisplay: 'long',
});
console.log(unitLong.format(5.5)); // "5,5 kilómetros"

// Unidades en formato corto (inglés)
const unitShort = new Intl.NumberFormat('en-US', {
  style: 'unit',
  unit: 'mile',
  unitDisplay: 'short',
});
console.log(unitShort.format(10.5)); // "10.5 mi"

// Otras unidades comunes
const unitLiter = new Intl.NumberFormat('en-US', {
  style: 'unit',
  unit: 'liter',
  unitDisplay: 'short',
});
console.log(unitLiter.format(2.5)); // "2.5 L"
```

## Notación compacta (abreviaturas)

Útil para mostrar números grandes de forma resumida:

```js
const compact = new Intl.NumberFormat('en-US', {
  notation: 'compact',
  compactDisplay: 'short',
});
console.log(compact.format(1234567)); // "1.2M"
console.log(compact.format(1234));    // "1.2K"
console.log(compact.format(987654321)); // "987.7M"
```

### Notación compacta en español

```js
const compactES = new Intl.NumberFormat('es-ES', {
  notation: 'compact',
  compactDisplay: 'short',
});
console.log(compactES.format(1234567)); // "1,2 M"
```

## Notación científica

```js
const scientific = new Intl.NumberFormat('en-US', {
  notation: 'scientific',
  maximumFractionDigits: 2,
});
console.log(scientific.format(1234567)); // "1.23E6"
console.log(scientific.format(0.000123)); // "1.23E-4"
```

## Control de dígitos y formato

### Sin separadores de miles

```js
const noGrouping = new Intl.NumberFormat('es-ES', {
  useGrouping: false,
  minimumFractionDigits: 2,
});
console.log(noGrouping.format(1234.56)); // "1234,56"
```

### Relleno con ceros a la izquierda

```js
const withZeros = new Intl.NumberFormat('en-US', {
  minimumIntegerDigits: 5,
  minimumFractionDigits: 2,
});
console.log(withZeros.format(123.45)); // "00,123.45"
```

### Control de dígitos significativos

```js
const significant = new Intl.NumberFormat('en-US', {
  minimumSignificantDigits: 3,
  maximumSignificantDigits: 5,
});
console.log(significant.format(123.456)); // "123.456"
console.log(significant.format(0.000123456)); // "0.00012346"
```

## Comparativa de locales

El mismo número se muestra diferente según el parámetro `locale`:

```js
const num = 1234567.89;
const locales = ['es-ES', 'en-US', 'de-DE', 'ja-JP', 'fr-FR'];

locales.forEach(locale => {
  const formatter = new Intl.NumberFormat(locale);
  console.log(`${locale}: ${formatter.format(num)}`);
});

// Resultados:
// es-ES: 1.234.567,89
// en-US: 1,234,567.89
// de-DE: 1.234.567,89
// ja-JP: 1,234,567.89
// fr-FR: 1 234 567,89
```

## Casos de uso comunes

| Caso de uso                          | Código                                                                                      |
| ------------------------------------ | ------------------------------------------------------------------------------------------- |
| **Precio de producto (USD)**         | `new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' })`                    |
| **Precio de producto (EUR)**         | `new Intl.NumberFormat('es-ES', { style: 'currency', currency: 'EUR' })`                    |
| **Porcentaje de descuento**          | `new Intl.NumberFormat('es-ES', { style: 'percent', minimumFractionDigits: 0 })`            |
| **Distancia en km**                  | `new Intl.NumberFormat('es-ES', { style: 'unit', unit: 'kilometer', unitDisplay: 'long' })` |
| **Número de seguidores (K/M)**       | `new Intl.NumberFormat('en-US', { notation: 'compact' })`                                   |
| **Tabla de precios (sin decimales)** | `new Intl.NumberFormat('es-ES', { maximumFractionDigits: 0 })`                              |

## Consideraciones importantes

1. **`Intl.NumberFormat`** es la herramienta más completa y flexible.
2. **`locale`** define el formato regional (separadores de miles, decimales, posición de moneda).
3. Los **códigos de moneda** deben ser ISO 4217 (ej. `USD`, `EUR`, `PEN`).
4. **`useGrouping`** controla los separadores de miles.
5. **`notation: 'compact'`** es ideal para redes sociales o dashboards.
6. **`minimumFractionDigits`** y **`maximumFractionDigits`** controlan los decimales.
7. **`minimumIntegerDigits`** es útil para códigos o números formateados.
8. Puedes combinar opciones (ej. moneda + notación compacta).
