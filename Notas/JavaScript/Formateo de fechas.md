---
orden: 29
tags:
  - Fechas
Comentario:
estado: true
---

## Métodos Básicos de Formateo

Estos métodos convierten una fecha a string sin opciones adicionales.

| Método           | Descripción                                      | Ejemplo de salida                     |
| ---------------- | ------------------------------------------------ | ------------------------------------- |
| `toString()`     | Fecha completa en formato legible del sistema    | `"Sun Mar 02 2025 14:30:00 GMT-0500"` |
| `toDateString()` | Solo la parte de la fecha                        | `"Sun Mar 02 2025"`                   |
| `toTimeString()` | Solo la parte de la hora                         | `"14:30:00 GMT-0500"`                 |
| `toISOString()`  | Formato ISO 8601 UTC (ideal para bases de datos) | `"2025-03-02T19:30:00.000Z"`          |
| `toJSON()`       | Formato JSON (equivalente a ISO)                 | `"2025-03-02T19:30:00.000Z"`          |

```js
const date = new Date(2025, 2, 2, 14, 30, 0);

console.log(date.toString());       // "Sun Mar 02 2025 14:30:00 GMT-0500 (EST)"
console.log(date.toDateString());   // "Sun Mar 02 2025"
console.log(date.toTimeString());   // "14:30:00 GMT-0500 (EST)"
console.log(date.toISOString());    // "2025-03-02T19:30:00.000Z"
console.log(date.toJSON());         // "2025-03-02T19:30:00.000Z"
```

## Métodos de Formateo Localizado (`toLocale*`)

Estos métodos adaptan el formato según la **configuración regional (`locale`)** y zona horaria del sistema o navegador.

| Método                 | Descripción                                  | Ejemplo de salida           |
| ---------------------- | -------------------------------------------- | --------------------------- |
| `toLocaleDateString()` | Fecha según la configuración regional        | `"2/3/2025"`                |
| `toLocaleTimeString()` | Hora según la configuración regional         | `"2:30:00 p. m."`           |
| `toLocaleString()`     | Fecha y hora según la configuración regional | `"2/3/2025, 2:30:00 p. m."` |

```js
const date = new Date(2025, 2, 2, 14, 30, 0);

console.log(date.toLocaleDateString());  // "3/2/2025" (formato MM/DD/YYYY en EE.UU.)
console.log(date.toLocaleTimeString());  // "2:30:00 PM" (formato 12h)
console.log(date.toLocaleString());      // "3/2/2025, 2:30:00 PM"
```

## Formateo Personalizado Manual

Puedes crear tus propias funciones para controlar exactamente el formato de salida.

```js
function formatDate(date) {
  const day = date.getDate().toString().padStart(2, '0');
  const month = (date.getMonth() + 1).toString().padStart(2, '0');
  const year = date.getFullYear();

  return `${day}/${month}/${year}`;
}

console.log(formatDate(new Date())); // "02/03/2025"
```

>**Nota:** `padStart(2, '0')` asegura que días y meses tengan siempre dos dígitos.

## Formateo Legible con `toLocaleDateString()` 

El método `toLocaleDateString()` acepta dos argumentos:

1. **`locale`**: identificador de idioma/región (ej. `"es-ES"`)
2. **`options`**: objeto con opciones de formato

### Opciones principales

| Opción    | Descripción      | Valores comunes                               |
| --------- | ---------------- | --------------------------------------------- |
| `weekday` | Día de la semana | `"long"`, `"short"`, `"narrow"`               |
| `year`    | Año              | `"numeric"`, `"2-digit"`                      |
| `month`   | Mes              | `"numeric"`, `"2-digit"`, `"long"`, `"short"` |
| `day`     | Día del mes      | `"numeric"`, `"2-digit"`                      |

### Valores de formato

| Valor       | Resultado aproximado |
| ----------- | -------------------- |
| `'numeric'` | `2`, `2025`          |
| `'2-digit'` | `02`, `25`           |
| `'long'`    | `domingo`, `marzo`   |
| `'short'`   | `dom.`, `mar.`       |

```js
function getReadableDate(date) {
  const options = { 
    weekday: 'long', 
    year: 'numeric', 
    month: 'long', 
    day: 'numeric' 
  };
  return date.toLocaleDateString('es-ES', options);
}

console.log(getReadableDate(new Date())); 
// "domingo, 2 de marzo de 2025"
```

## Formateo Internacional con `Intl.DateTimeFormat`

La API **`Intl.DateTimeFormat`** es la forma más recomendada para mostrar fechas internacionales, ya que adapta automáticamente:

- **Idioma** y **formato regional**
- **Orden de fecha** (DD/MM vs MM/DD)
- **Nombres de meses y días** en el idioma adecuado
- **Formato de hora** (12h/24h)
- **Zona horaria**

> **Ventaja:** No modifica el objeto `Date`, solo genera una representación en texto.

Sintaxis:

```js
new Intl.DateTimeFormat(locale, options)
```

### Uso del método `format()`

Convierte una fecha en un string.

```js
const date = new Date();

const formatter = new Intl.DateTimeFormat("es-ES", {
  year: "numeric",
  month: "long",
  day: "numeric",
  weekday: "long",
});

console.log(formatter.format(date));
// "domingo, 2 de marzo de 2025"
```

### Configuraciones regionales (`locale`)

El parámetro `locale` define el idioma y la región para mostrar la fecha.

| Locale    | Idioma / Región      |
| --------- | -------------------- |
| `"es-ES"` | Español (España)     |
| `"es-PE"` | Español (Perú)       |
| `"en-US"` | Inglés (EE.UU.)      |
| `"en-GB"` | Inglés (Reino Unido) |
| `"ja-JP"` | Japonés (Japón)      |
| `"de-DE"` | Alemán (Alemania)    |
| `"fr-FR"` | Francés (Francia)    |

```js
const date = new Date(2025, 2, 2);

console.log(new Intl.DateTimeFormat("es-ES").format(date)); // "2/3/2025"
console.log(new Intl.DateTimeFormat("en-US").format(date)); // "3/2/2025"
console.log(new Intl.DateTimeFormat("ja-JP").format(date)); // "2025/3/2"
console.log(new Intl.DateTimeFormat("de-DE").format(date)); // "2.3.2025"
```

>El mismo objeto `Date` se muestra de forma diferente según el `locale`.

## Opciones Avanzadas de Formateo

El segundo parámetro (`options`) permite un control granular:

| Opción         | Descripción                      | Valores comunes                               |
| -------------- | -------------------------------- | --------------------------------------------- |
| `weekday`      | Día de la semana                 | `"long"`, `"short"`, `"narrow"`               |
| `year`         | Año                              | `"numeric"`, `"2-digit"`                      |
| `month`        | Mes                              | `"numeric"`, `"2-digit"`, `"long"`, `"short"` |
| `day`          | Día del mes                      | `"numeric"`, `"2-digit"`                      |
| `hour`         | Hora                             | `"numeric"`, `"2-digit"`                      |
| `minute`       | Minutos                          | `"numeric"`, `"2-digit"`                      |
| `second`       | Segundos                         | `"numeric"`, `"2-digit"`                      |
| `timeZoneName` | Nombre de la zona horaria        | `"short"`, `"long"`                           |
| `timeZone`     | Zona horaria específica          | `"America/Lima"`, `"Europe/Madrid"`           |
| `hour12`       | Formato 12h (true) o 24h (false) | `true`, `false`                               |
| `dateStyle`    | Estilo de fecha predefinido      | `"full"`, `"long"`, `"medium"`, `"short"`     |
| `timeStyle`    | Estilo de hora predefinido       | `"full"`, `"long"`, `"medium"`, `"short"`     |

```js
const options = {
  year: "numeric",
  month: "long",
  day: "numeric",
  weekday: "long",
  hour: "2-digit",
  minute: "2-digit",
  second: "2-digit",
  timeZone: "America/Lima",
  timeZoneName: "short",
  hour12: true,
};

const formatter = new Intl.DateTimeFormat("es-PE", options);

console.log(formatter.format(new Date()));
// "domingo, 2 de marzo de 2025, 02:30:00 p. m. GMT-5"
```
