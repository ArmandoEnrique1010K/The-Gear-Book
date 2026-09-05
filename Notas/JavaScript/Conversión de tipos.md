---
orden: 8
tags:
  - Conversiones
estado: true
---

## Conversión Implícita (Coerción)

Ocurre cuando JavaScript **convierte automáticamente** un valor a otro tipo durante una operación o comparación.

### En operaciones aritméticas

|Operador|Comportamiento|
|---|---|
|`+`|Si un operando es **string**, convierte el otro a **string** y **concatena**.|
|`-`, `*`, `/`, `%`|Convierte ambos operandos a **número**.|

```javascript
console.log(10 + "5");      // "105" (concatena)
console.log("10" - 5);      // 5    (convierte "10" a número)
console.log("10" * "2");    // 20   (convierte ambos)
console.log("20" / "4");    // 5
console.log("hola" - 1);    // NaN  (no se puede convertir "hola")
```

### En comparaciones

| Operador | Comportamiento                                 |
| -------- | ---------------------------------------------- |
| \=\=     | Convierte tipos antes de comparar (peligroso). |
| \=\=\=   | No convierte tipos (seguro y recomendado).     |

```javascript
console.log(5 == "5");      // true  (string → número)
console.log("" == false);   // true  (ambos son falsy)
console.log(0 == false);    // true
console.log(5 === "5");     // false (tipos distintos)
```

>**⚠️ Advertencia:** La coerción con \== puede generar resultados inesperados. Siempre prefiere \=== y `!==`.

## Conversión Explícita (Manual)

Se realiza **intencionalmente** usando funciones o métodos. Es más segura y predecible.

### De string a número

| Método                  | Descripción                                                                     | Ejemplo                          |
| ----------------------- | ------------------------------------------------------------------------------- | -------------------------------- |
| `Number(valor)`         | Convierte a número (decimal incluido). Devuelve `NaN` si no es válido.          | `Number("123.45")` → `123.45`    |
| `parseInt(valor, base)` | Convierte a **entero** (ignora decimales). Recomendado especificar `base = 10`. | `parseInt("10px", 10)` → `10`    |
| `parseFloat(valor)`     | Convierte a **decimal** (incluye punto flotante).                               | `parseFloat("10.5abc")` → `10.5` |
| `+` (unario)            | Conversión rápida a número.                                                     | `+"12.5"` → `12.5`               |

```javascript
console.log(Number("123"));        // 123
console.log(Number("abc"));        // NaN
console.log(parseInt("10px", 10)); // 10
console.log(parseFloat("10.5.6")); // 10.5 (solo el primer punto)
console.log(+"12.5");              // 12.5
```

>**📌 Nota:** `parseInt` y `parseFloat` leen hasta el primer carácter no numérico. Si no encuentran ningún número al inicio, devuelven `NaN`.

### De número o booleano a String

| Método          | Descripción                                                            | Ejemplo                    |
| --------------- | ---------------------------------------------------------------------- | -------------------------- |
| `String(valor)` | Convierte cualquier valor a string.                                    | `String(100)` → `"100"`    |
| `.toString()`   | Método de números/booleanos. **No funciona con `null` o `undefined`**. | `(50).toString()` → `"50"` |
| `+ ""`          | Concatena con string vacío (coerción rápida).                          | `false + ""` → `"false"`   |

```javascript
console.log(String(100));          // "100"
console.log((50).toString());      // "50"
console.log((true).toString());    // "true"
console.log(false + "");           // "false"
```

>**⚠️ Advertencia:** `null.toString()` y `undefined.toString()` lanzan un error. Usa `String()` en su lugar.

### De cualquier tipo a booleano

| Método                | Descripción                                                | Ejemplo                     |
| --------------------- | ---------------------------------------------------------- | --------------------------- |
| `Boolean(valor)`      | Convierte explícitamente según reglas **truthy/falsy**.    | `Boolean("Hello")` → `true` |
| `!!` (doble negación) | Forma rápida y concisa de obtener el equivalente booleano. | `!!0` → `false`             |

```javascript
console.log(Boolean("Hello"));   // true
console.log(Boolean(""));        // false
console.log(!!0);                // false
console.log(!![]);               // true  (arreglo vacío es truthy)
```

## Validación de `NaN` (Not a Number)

`NaN` aparece cuando una operación numérica falla. Para detectarlo correctamente:

| Método                | Comportamiento                                                                     | Ejemplo                           |
| --------------------- | ---------------------------------------------------------------------------------- | --------------------------------- |
| `isNaN(valor)`        | **Convierte** el valor a número primero. Puede dar `true` en valores no numéricos. | `isNaN("hello")` → `true`         |
| `Number.isNaN(valor)` | **No convierte**. Solo `true` si el valor es exactamente `NaN` y tipo `number`.    | `Number.isNaN("hello")` → `false` |

```javascript
console.log(Number("123abc"));            // NaN
console.log(0 / 0);                       // NaN

console.log(isNaN("hello"));              // true (convierte "hello" → NaN)
console.log(isNaN(undefined));            // true
console.log(isNaN("123"));                // false

console.log(Number.isNaN("hello"));       // false (no es número)
console.log(Number.isNaN(undefined));     // false
console.log(Number.isNaN(NaN));           // true
console.log(Number.isNaN(Number("abc"))); // true
```

>**✅ Recomendación:** Siempre usa `Number.isNaN()` para evitar falsos positivos.

## `null` vs `undefined` en conversiones

| Valor       | `String()`    | `Number()` | `Boolean()` | \=\=                     | \=\=\=  |
| ----------- | ------------- | ---------- | ----------- | ------------------------ | ------- |
| `null`      | `"null"`      | `0`        | `false`     | `true` (con `undefined`) | `false` |
| `undefined` | `"undefined"` | `NaN`      | `false`     | `true` (con `null`)      | `false` |

```javascript
console.log(String(null));       // "null"
console.log(String(undefined));  // "undefined"
console.log(Number(null));       // 0
console.log(Number(undefined));  // NaN
console.log(Boolean(null));      // false
console.log(Boolean(undefined)); // false
console.log(undefined == null);  // true
console.log(undefined === null); // false
```

## Patrón seguro para validar números

Este patrón es muy útil para **validar entradas de usuario** (formularios, inputs) en el Frontend.

```javascript
const input = "123.45";

if (!Number.isNaN(Number(input))) {
  console.log("Valid number:", Number(input));
} else {
  console.log("¡It is not a number.!");
}
```
