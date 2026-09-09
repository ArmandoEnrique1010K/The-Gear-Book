---
orden: 30
tags:
  - Fechas
Comentario:
estado: true
---

## Cálculos con fechas

Los objetos `Date` permiten realizar **operaciones matemáticas, comparaciones y manipulaciones** de tiempo, fundamentales en aplicaciones que manejan vencimientos, calendarios, reservas, temporizadores o diferencias entre fechas.

## Sumar y Restar tiempo a una fecha

### Sumar días

Para modificar una fecha, usa métodos `set` como `setDate()`. **Siempre crea una copia** para evitar mutar la fecha original.

```js
function addDays(date, days) {
  const newDate = new Date(date); // Copia para no modificar la original
  newDate.setDate(newDate.getDate() + days);
  return newDate;
}

const today = new Date();
const nextWeek = addDays(today, 7);
console.log(`Today: ${today.toDateString()}`);
console.log(`Next week: ${nextWeek.toDateString()}`);
```

> **Nota:** `setDate()` ajusta automáticamente meses y años si el valor supera los días válidos del mes.

### Sumar meses

JavaScript ajusta automáticamente fechas inválidas cuando un mes no tiene suficientes días.

```js
function addMonths(date, months) {
  const newDate = new Date(date);
  newDate.setMonth(newDate.getMonth() + months);
  return newDate;
}

const today = new Date(2025, 0, 31); // 31 de enero
const nextMonth = addMonths(today, 1);
console.log(nextMonth.toDateString()); // Se ajusta a marzo (febrero no tiene 31)
```

> **Importante:** Al sumar meses, JavaScript puede cambiar el día automáticamente si la fecha resultante no existe.

### Sumar años

```js
function addYears(date, years) {
  const newDate = new Date(date);
  newDate.setFullYear(newDate.getFullYear() + years);
  return newDate;
}
```

## Restar tiempo a una fecha

### Restar días

```js
function subtractDays(date, days) {
  const newDate = new Date(date);
  newDate.setDate(newDate.getDate() - days);
  return newDate;
}

const today = new Date();
const lastWeek = subtractDays(today, 7);
```

### Restar meses y años

```js
function subtractMonths(date, months) {
  const newDate = new Date(date);
  newDate.setMonth(newDate.getMonth() - months);
  return newDate;
}

function subtractYears(date, years) {
  const newDate = new Date(date);
  newDate.setFullYear(newDate.getFullYear() - years);
  return newDate;
}
```

## Calcular diferencias entre fechas

### Diferencia en milisegundos, segundos, minutos, horas y días

```js
function getDateDiff(startDate, endDate) {
  const diffMs = endDate.getTime() - startDate.getTime();
  
  return {
    milliseconds: diffMs,
    seconds: diffMs / 1000,
    minutes: diffMs / (1000 * 60),
    hours: diffMs / (1000 * 60 * 60),
    days: diffMs / (1000 * 60 * 60 * 24)
  };
}

const start = new Date(2025, 0, 1);
const end = new Date(2025, 0, 10);
const diff = getDateDiff(start, end);

console.log(diff.days);        // 9
console.log(diff.hours);       // 216
console.log(diff.minutes);     // 12960
```

### Diferencia en días (redondeo)

```js
function getDaysDifference(date1, date2) {
  const diffMs = date2.getTime() - date1.getTime();
  return Math.round(diffMs / (1000 * 60 * 60 * 24));
}
```

## Comparaciones de fechas

### Comparaciones directas (operadores relacionales)

Las fechas se pueden comparar con operadores `<`, `>`, `<=`, `>=` porque JavaScript las convierte a timestamps internamente.

```js
const date1 = new Date(2025, 0, 1);
const date2 = new Date(2025, 0, 15);

console.log(date1 < date2);   // true
console.log(date1 > date2);   // false
console.log(date1 <= date2);  // true
console.log(date1 >= date2);  // false
```

### Comparación de igualdad

Dos objetos `Date` **nunca** son iguales con === si son instancias diferentes, aunque representen el mismo momento.

```js
const date1 = new Date(2025, 0, 1);
const date2 = new Date(2025, 0, 1);

console.log(date1 === date2);               // false (comparación de referencia)
console.log(date1.getTime() === date2.getTime()); // true (comparación de valor)
```

### Comparar solo la fecha (ignorando hora)

```js
function isSameDate(date1, date2) {
  return date1.toDateString() === date2.toDateString();
}

const dateA = new Date('2025-03-02T10:00:00');
const dateB = new Date('2025-03-02T22:30:00');

console.log(isSameDate(dateA, dateB)); // true
```

> `toDateString()` elimina la parte de la hora y conserva solo la fecha.

### Verificar si una fecha está dentro de un rango

```js
function isDateInRange(date, startDate, endDate) {
  const time = date.getTime();
  return time >= startDate.getTime() && time <= endDate.getTime();
}

const date = new Date(2025, 5, 15);
const start = new Date(2025, 5, 1);
const end = new Date(2025, 5, 30);

console.log(isDateInRange(date, start, end)); // true
```

## Validaciones de fechas

### Verificar si es fin de semana

```js
function isWeekend(date) {
  const day = date.getDay();
  return day === 0 || day === 6; // 0 = domingo, 6 = sábado
}
```

### Verificar si es día laborable

```js
function isBusinessDay(date) {
  const day = date.getDay();
  return day !== 0 && day !== 6;
}
```

### Verificar si un año es bisiesto

```js
function isLeapYear(year) {
  return (year % 4 === 0 && year % 100 !== 0) || (year % 400 === 0);
}

console.log(isLeapYear(2024)); // true
console.log(isLeapYear(2025)); // false
```

## Límites y consideraciones del objeto `Date`

### Rango de fechas válidas

JavaScript puede representar fechas entre aproximadamente **-271,821 a.C.** y **+275,760 d.C.**

```js
const minDate = new Date(-8640000000000000);
const maxDate = new Date(8640000000000000);

console.log(minDate.toString()); // ~20 de abril de 271821 a.C.
console.log(maxDate.toString()); // ~13 de septiembre de 275760 d.C.
```

### Fecha de inicio Unix

El timestamp `0` representa el inicio de la época Unix:

```js
const unixEpoch = new Date(0);
console.log(unixEpoch.toISOString()); // "1970-01-01T00:00:00.000Z"
```

### Meses basados en 0

Los meses van de `0` (enero) a `11` (diciembre):

```js
const date = new Date(2025, 0, 1);
console.log(date.getMonth()); // 0 = Enero
```

### Parsing y zonas horarias

Diferentes formatos de string pueden dar resultados distintos según la zona horaria:

```js
const utcDate = new Date("2025-03-02");        // Interpretado como UTC
const localDate = new Date("2025-03-02T00:00:00"); // Interpretado como hora local

console.log(utcDate);
console.log(localDate);
```

## Reloj en tiempo real con `setInterval`

La función `setInterval()` permite ejecutar código repetidamente cada cierto intervalo.

```js
function updateClock() {
  const now = new Date();

  const hours = now.getHours().toString().padStart(2, "0");
  const minutes = now.getMinutes().toString().padStart(2, "0");
  const seconds = now.getSeconds().toString().padStart(2, "0");

  console.log(`${hours}:${minutes}:${seconds}`);
}

// Actualizar cada segundo
setInterval(updateClock, 1000);

// 14:30:01
// 14:30:02
// 14:30:03
```

## Consideraciones de rendimiento

Aunque `Date` es relativamente ligero, crear demasiadas instancias puede afectar el rendimiento en operaciones intensivas:

| Recomendación                                                     | Motivo                                     |
| ----------------------------------------------------------------- | ------------------------------------------ |
| Reutiliza instancias cuando sea posible                           | Evita sobrecarga de creación de objetos    |
| Evita convertir fechas a strings repetidamente dentro de bucles   | Las conversiones son costosas              |
| Usa timestamps (`Date.now()` o `getTime()`) para cálculos masivos | Los números son más rápidos que objetos    |
| Evita parsear strings de fecha repetidamente                      | El parsing es costoso y propenso a errores |

## Consideraciones importantes

1. **Meses:** van de `0` a `11` (enero a diciembre).
2. **Días de la semana:** van de `0` (domingo) a `6` (sábado).
3. **Almacenamiento interno:** las fechas se almacenan en UTC.
4. **Zona horaria:** los métodos `get`/`set` usan la zona local; `getUTC`/`setUTC` usan UTC.
5. **Mutabilidad:** `Date` es mutable; los métodos `set` modifican el objeto original.
6. **Comparación:** usa `getTime()` para comparar valores, no \=\=\=.
7. **Timestamp actual:** `Date.now()` devuelve el timestamp actual en milisegundos.
8. **Formateo internacional:** `Intl.DateTimeFormat` es la forma recomendada.
9. **Parsing de ISO:** los strings ISO pueden cambiar según la zona horaria.
