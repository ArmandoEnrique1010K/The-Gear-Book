---
orden: 28
tags:
  - Fechas
Comentario:
estado: true
---

## El objeto `Date` en JavaScript

El objeto `Date` en JavaScript es una herramienta fundamental para manejar fechas y horas. Permite **crear, manipular, formatear y calcular** momentos en el tiempo de manera eficiente.

Cada instancia de `Date` representa un instante específico y almacena internamente la cantidad de milisegundos transcurridos desde el **1 de enero de 1970 00:00:00 UTC** (conocido como **Época Unix**).

## Creación de fechas

El constructor `Date` admite múltiples formatos para crear instancias:

```js
// Fecha y hora actual del sistema
const now = new Date();
console.log(now);
// Sat Mar 02 2025 14:30:15 GMT-0500

// Fecha específica (año, mes, día) - mes 0 = enero
const date1 = new Date(2024, 0, 15); // 15 de enero de 2024

// Desde string en formato ISO
const date2 = new Date('2024-01-15');
const date3 = new Date('01/15/2024');

// Desde timestamp (milisegundos desde 1970)
const date4 = new Date(1705344000000);
```

>**⚠️ Importante:** Los meses van de **0 (enero)** a **11 (diciembre)**.

## Variantes del constructor `new Date`

Sintaxis completa:

```js
new Date(year, month, day, hours, minutes, seconds, milliseconds)
```

Ejemplo:

```js
const fullDate = new Date(2025, 2, 2, 14, 30, 0, 200);
console.log(fullDate); // Sun Mar 02 2025 14:30:00 GMT-0500
```

### Formatos ISO 8601

JavaScript soporta fechas en formato ISO 8601, siendo el formato más recomendado por compatibilidad y consistencia:

- `"YYYY-MM-DD"`: interpretado como **UTC**.
- `"YYYY-MM-DDTHH:mm:ss"`: interpretado como **hora local**.
- `"YYYY-MM-DDTHH:mm:ssZ"`: interpretado como **UTC**.

```js
const isoDate = new Date("2025-03-02");          // UTC
const localDate = new Date("2025-03-02T14:30:00"); // Local
const utcDate = new Date("2025-03-02T14:30:00Z"); // UTC
```

### Constructor con timestamp Unix

`Date` también puede construirse usando timestamps Unix en milisegundos.

```js
const unixDate = new Date(1709370000000);
// En segundos: new Date(1709370000 * 1000);
```

>**Nota:** JavaScript usa milisegundos, multiplica por `1000` si tienes segundos.

## Métodos para obtener valores (getters)

Por defecto, estos métodos trabajan con la zona horaria local del sistema.

### Métodos de fecha (hora local)

| Método          | Descripción      | Rango           |
| --------------- | ---------------- | --------------- |
| `getFullYear()` | Año (4 dígitos)  | —               |
| `getMonth()`    | Mes              | 0–11            |
| `getDate()`     | Día del mes      | 1–31            |
| `getDay()`      | Día de la semana | 0 (domingo) – 6 |

```js
const date = new Date(2025, 2, 2, 14, 30, 45, 500);

console.log(date.getFullYear());  // 2025
console.log(date.getMonth());     // 2 (marzo)
console.log(date.getDate());      // 2
console.log(date.getDay());       // 0 (domingo)
```

> **Nota:** El método `getYear()` está obsoleto, usa `getFullYear()`.

### Métodos de hora (hora local)

|Método|Descripción|Rango|
|---|---|---|
|`getHours()`|Hora|0–23|
|`getMinutes()`|Minutos|0–59|
|`getSeconds()`|Segundos|0–59|
|`getMilliseconds()`|Milisegundos|0–999|

```js
const date = new Date(2025, 2, 2, 14, 30, 45, 500);

console.log(date.getHours());        // 14
console.log(date.getMinutes());      // 30
console.log(date.getSeconds());      // 45
console.log(date.getMilliseconds()); // 500
```

### Métodos UTC (hora universal)

Obtienen valores usando el tiempo universal coordinado (UTC), ignorando la zona horaria local.

|Método|Descripción|
|---|---|
|`getUTCFullYear()`|Año en UTC|
|`getUTCMonth()`|Mes en UTC|
|`getUTCHours()`|Hora en UTC|

```js
const date = new Date(2025, 2, 2, 14, 30, 45, 500);

console.log(date.getUTCHours()); // 19 (14 - 5 horas si local es GMT-5)
```

>El resultado puede variar según la zona horaria del sistema.

## Timestamps y Cálculos

Un timestamp representa un momento específico en el tiempo transcurrido desde el 1 de enero de 1970, expresado en milisegundos.

### Obtener timestamp actual

```js
console.log(Date.now()); // 1709370000000
```

### Timestamp de una fecha

```js
const date = new Date(2025, 2, 2, 14, 30, 45, 500);
console.log(date.getTime()); // 1740925845500
```

### Diferencia entre fechas (en milisegundos)

```js
const start = new Date(2025, 0, 1);
const end = new Date(2025, 11, 31);

const diffMs = end.getTime() - start.getTime();
console.log(diffMs); // 31449600000
```

### Conversiones útiles

Ten en cuenta las siguientes conversiones:

| Unidad    | Milisegundos        |
| --------- | ------------------- |
| 1 segundo | 1000                |
| 1 minuto  | 1000 × 60           |
| 1 hora    | 1000 × 60 × 60      |
| 1 día     | 1000 × 60 × 60 × 24 |

```js
const start = new Date(2025, 0, 1);
const end = new Date(2025, 11, 31);

const diffMs = end.getTime() - start.getTime();

// Conversión a dias
const diffDays = diffMs / (1000 * 60 * 60 * 24);
console.log(diffDays); // 9
```

## Métodos para establecer valores (setters)

Todos los métodos `set` son **mutables** (modifican el objeto original).

### Métodos de fecha:

|Método|Descripción|
|---|---|
|`setFullYear(year)`|Establece el año|
|`setMonth(month)`|Establece el mes (0–11)|
|`setDate(day)`|Establece el día del mes (1–31)|

```js
const date = new Date();

date.setFullYear(2024);
date.setMonth(5);   // Junio
date.setDate(25);

console.log(date); // 2024-06-25T04:24:02.641Z
```

### Métodos de hora

| Método                | Descripción                        |
| --------------------- | ---------------------------------- |
| `setHours(hours)`     | Establece la hora (0–23)           |
| `setMinutes(minutes)` | Establece los minutos (0–59)       |
| `setSeconds(seconds)` | Establece los segundos (0–59)      |
| `setMilliseconds(ms)` | Establece los milisegundos (0–999) |

```js
const date = new Date();

date.setHours(14);
date.setMinutes(30);
date.setSeconds(0);
date.setMilliseconds(500);

console.log(date); // 2026-09-08T14:30:00.500Z
```

### Métodos UTC

| Método             | Descripción              |
| ------------------ | ------------------------ |
| `setUTCFullYear()` | Establece el año en UTC  |
| `setUTCHours()`    | Establece la hora en UTC |

```js
const date = new Date();

date.setUTCFullYear(2024);
date.setUTCHours(14);

console.log(date); // 2024-09-08T14:24:34.756Z
```

>**Ventaja:** Evitan problemas con diferencias de zona horaria.

## Comportamiento automático de ajuste

JavaScript ajusta automáticamente valores fuera de rango

```js
const date = new Date(2025, 0, 31); // 31 de enero
date.setMonth(1); // Febrero (no tiene 31 días)
console.log(date); // Sun Mar 02 2025 (se ajusta a marzo)
```

>**Útil:** Permite manejar fechas inválidas sin errores.
