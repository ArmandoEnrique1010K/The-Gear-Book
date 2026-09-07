---
orden: 16
tags:
  - Objetos
Comentario:
estado: true
---

## Objetos en JavaScript

Los **objetos** en JavaScript son estructuras de datos fundamentales que permiten almacenar **colecciones de propiedades y valores**. Cada propiedad se compone de una **clave** (nombre) y un **valor** asociado, que puede ser de cualquier tipo de datos (primitivo, arreglo, función, otro objeto, etc.).

## Sintaxis de objetos

La forma más común y recomendada de crear un objeto es mediante **literales de objeto**, usando llaves `{}`.

```js
const car = {
  brand: "Ford",
  model: "Mustang",
  year: 2021
};
```

>**Nota:** Un objeto declarado con `const` **no impide modificar sus propiedades**, solo previene reasignar la referencia del objeto en sí.

## Acceso a propiedades

Puedes acceder a las propiedades de un objeto de dos maneras principales:

### Notación de punto (`.`)

Es la forma más común, legible y recomendada cuando el nombre de la clave es válido como identificador.

```js
const car = {
  brand: "Ford",
  model: "Mustang",
  year: 2021
};

console.log(car.brand);  // "Ford"
```

### Notación de corchetes (`[]`)

Útil cuando:

- El nombre de la clave tiene **espacios** o **caracteres especiales**.
- La clave es **dinámica** (almacenada en una variable).

```js
const car = {
  brand: "Ford",
  model: "Mustang",
  year: 2021
};

console.log(car["model"]);  // "Mustang"

const key = "year";
console.log(car[key]);      // 2021
```

## Visualizar objetos en consola

Para inspeccionar objetos durante el desarrollo:

- **`console.log(obj)`**: muestra el objeto en formato estándar.
- **`console.table(obj)`**: imprime el objeto en **forma de tabla**, ideal para visualizar múltiples propiedades de manera organizada.

```js
const car = {
  brand: "Ford",
  model: "Mustang",
  year: 2022,
  color: "Red"
};

console.table(car);
```

> Las propiedades se imprimen en orden alfabético por clave.

> **Tip:** `console.table` es especialmente útil cuando trabajas con arreglos de objetos o objetos con muchas propiedades.

## Optional Chaining (`?.`)

Introducido en **ES2020**, el operador **optional chaining** (`?.`) permite acceder a propiedades de objetos anidados **sin generar errores** si alguna propiedad intermedia es `null` o `undefined`.

- Ideal para trabajar con datos de **APIs REST** o **bases de datos** donde algunas propiedades pueden no estar presentes.

```js
const user = {
  name: "Carlos",
  profile: {
    age: 30,
  },
};

console.log(user.profile?.age);        // 30
console.log(user.profile?.address);    // undefined (sin error)
console.log(user.contact?.email);      // undefined (sin error)
```

### Comparación con el enfoque tradicional (antes de ES2020)

```js
const user = {
  name: "Carlos",
  profile: {
    age: 30,
  },
};

// Verificación manual de cada nivel
if (user && user.profile && user.profile.age) {
  console.log(user.profile.age);
} else {
  console.log("Age not available");
}

// Con optional chaining es mucho más limpio
console.log(user?.profile?.age ?? "Age not available");
```

## Manipular propiedades

### Agregar o modificar propiedades

Puedes agregar nuevas propiedades o modificar las existentes usando la notación de punto o corchetes.

```js
const car = {
  year: 2022
};

car.year = 2012;        // Modifica propiedad existente
car.brand = "Toyota";   // Agrega nueva propiedad
car["model"] = "Corolla";

console.log(car); // { year: 2012, brand: "Toyota", model: "Corolla" }
```

> Si la clave no existe, se **crea automáticamente**; si existe, se **actualiza** su valor.

### Eliminar propiedades

Usa el operador `delete` para eliminar una propiedad de un objeto.

```js
const car = {
  brand: "Ford",
  model: "Mustang",
  year: 2022
};

delete car.model;
console.log(car); // { brand: "Ford", year: 2022 }
```
