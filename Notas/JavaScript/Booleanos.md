---
orden: 7
tags:
  - Datos
---

## Valores Truthy y Falsy

En JavaScript, **todo valor tiene un comportamiento booleano implícito** cuando se usa en contextos como `if`, `while`, `&&`, `||` o `!`. No es necesario que sea estrictamente `true` o `false`.

### Valores Falsy (se comportan como `false`)

Son aquellos que **se convierten automáticamente a `false`** en evaluaciones booleanas:

| Tipo       | Valores Falsy              |
| ---------- | -------------------------- |
| Booleano   | `false`                    |
| Números    | `0`, `-0`, `0n` (BigInt)   |
| Cadenas    | `""` (cadena vacía)        |
| Especiales | `null`, `undefined`, `NaN` |

```javascript
if (0) console.log("Esto no se ejecuta");
if ("") console.log("Esto tampoco");
if (null) console.log("Ni esto");
```

### Valores Truthy (se comportan como `true`)

Cualquier valor que **no esté en la lista de falsy** es truthy:

| Tipo      | Ejemplos                         |
| --------- | -------------------------------- |
| Números   | `1`, `-5`, `3.14`                |
| Cadenas   | `"hola"`, `"0"`, `" "` (espacio) |
| Objetos   | `{}`, `{ clave: "valor" }`       |
| Arreglos  | `[]`, `[1, 2, 3]`                |
| Funciones | `function() {}`, `() => {}`      |

```javascript
if (1) console.log("Sí se ejecuta");
if ([]) console.log("Arreglo vacío es truthy");
if ({}) console.log("Objeto vacío también");
```

## Comparaciones curiosas (y peligrosas)

El operador \=\= convierte tipos, lo que puede dar resultados inesperados:

```javascript
console.log(0 == false);        // true  (0 se convierte a false)
console.log(0 === false);       // false (tipos distintos)
console.log(undefined == null); // true  (ambos son "vacíos")
console.log(undefined === null);// false (tipos distintos)
console.log("" == 0);           // true  ("" → 0)
console.log("" === 0);          // false
```

>**✅ Buenas prácticas:** Siempre usa \=\=\= y `!==` para evitar errores por conversiones implícitas.

## Operadores Lógicos

Se usan para combinar o invertir condiciones. Pero **no siempre devuelven `true` o `false`**, sino el **valor evaluado por última vez**.

| Operador | Nombre   | Comportamiento                                                          |
| -------- | -------- | ----------------------------------------------------------------------- |
| `&&`     | AND (Y)  | Retorna el **primer valor falsy**, o el **último** si todos son truthy. |
| `\|\|`   | OR (O)   | Retorna el **primer valor truthy**, o el **último** si todos son falsy. |
| `!`      | NOT (NO) | Invierte el valor booleano (`!truthy` → `false`, `!falsy` → `true`).    |

```javascript
// &&: cortocircuito con falsy
console.log(0 && "Hola");       // 0
console.log("Hola" && 123);     // 123 (ambos truthy → último)

// ||: cortocircuito con truthy
console.log(null || "Usuario"); // "Usuario"
console.log("" || 0 || false);  // false (todos falsy → último)

// !: negación
console.log(!0);                // true
console.log(!"Texto");          // false
console.log(!(5 > 3 && true));  // false
```

### Usos prácticos del cortocircuito

Se utiliza el operador `&&` para ejecutar algo **solo si el valor (o condición) de la izquierda es truthy**.

El operador `||` se utiliza para asignar **valores por defecto solamente si el valor de la izquierda es falsy.**

```javascript
// Ejecutar solo si la condición es truthy
let usuario = { nombre: "Ana" };
usuario && console.log(usuario.nombre); // "Ana"

// Asignar valor por defecto si es falsy
let nombre = "" || "Invitado";          // "Invitado"
let edad = 0 || 18;                     // 18 (cuidado: 0 es falsy)
```

## Operador Nullish Coalescing (`??`)

Permite asignar un **valor por defecto solo si la variable es `null` o `undefined`**.

A diferencia de `||`, **respeta valores válidos** como `0`, `""` o `false`.

| Operador | Se activa con        | Ejemplo          |
| -------- | -------------------- | ---------------- |
| `??`     | `null` o `undefined` | `0 ?? 10` → `0`  |
| `\|\|`   | Cualquier falsy      | `0 \| 10` → `10` |

```javascript
// Con ?? (solo null/undefined)
const p1 = null ?? 1;      // 1
const p2 = 0 ?? 1;         // 0  (válido)
const p3 = "" ?? "Texto";  // "" (válido)

// Con || (cualquier falsy)
const p4 = 0 || 1;         // 1
const p5 = "" || "Texto";  // "Texto"
```

>**🔍 Recomendación:** Usa `??` para valores por defecto cuando `0`, `false` o `""` sean datos válidos, utiliza `||` solo cuando quieras reemplazar **cualquier valor falsy** en general.
