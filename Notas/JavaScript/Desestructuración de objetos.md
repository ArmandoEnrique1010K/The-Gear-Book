---
orden: 17
tags:
  - Objetos
Comentario:
estado: true
---

## Objetos Anidados

Un **objeto anidado** es un objeto que contiene otro objeto como valor de una de sus propiedades. Permite representar relaciones jerárquicas o agrupar datos relacionados de manera lógica.

- Puedes acceder a las propiedades anidadas **encadenando** los nombres de las propiedades con notación de punto o corchetes.

```js
const invoice = {
  id: 1,
  client: {
    name: "Juan",
    lastName: "Pérez",
    age: 30
  }
};

console.log(invoice.client.name);        // "Juan"
console.log(invoice["client"]["lastName"]); // "Pérez"

// Usando optional chaining para evitar errores
console.log(invoice.client?.address?.city); // undefined (sin error)
```

## Desestructuración de Objetos

La **desestructuración** permite extraer valores de un objeto y asignarlos a variables de manera concisa y legible.

```js
const car = {
  brand: "Ford",
  model: "Mustang"
};

const { brand, model } = car;

console.log(brand); // "Ford"
console.log(model); // "Mustang"
```

### Uso de alias (renombrar propiedades)

Puedes **renombrar** propiedades al desestructurar usando `:`.

```js
const client = {
  name: "Juan",
  age: 30
};

const { name: clientName, age } = client;

console.log(clientName); // "Juan"
console.log(age);        // 30
```

### Desestructuración con valores por defecto

Puedes asignar valores predeterminados en caso de que la propiedad no exista.

```js
const product = {
  name: "Tablet"
};

const { name, price = 100, available = true } = product;

console.log(name);      // "Tablet"
console.log(price);     // 100 (valor por defecto)
console.log(available); // true (valor por defecto)
```

### Desestructuración anidada

Puedes extraer propiedades de objetos anidados

```js
const invoice = {
  id: 1,
  client: {
    name: "Juan",
    lastName: "Pérez"
  }
};

const { client: { name, lastName } } = invoice;
console.log(name);     // "Juan"
console.log(lastName); // "Pérez"
```

### Antes de la desestructuración

Tenias que asignar una variable a cada una de las claves o nombre de la propiedad de un objeto.

```js
const product = {
  name: "Tablet",
  price: 300,
  available: false
};

const name = product.name;
const price = product.price;
const available = product.available;

console.log(name);      // "Tablet"
console.log(price);     // 300
console.log(available); // false
```

## Object Literal Enhancement (Mejora de Literales de Objeto)

Esta característica de **ES6** permite crear objetos de manera más eficiente cuando las variables ya existen en el ámbito.

Si el nombre de la variable coincide con el nombre de la propiedad (**Shorthand Property**), puedes omitir la asignación explícita.

```js
const brand = "Ford";
const model = "Mustang";

// Equivalente a { brand: brand, model: model }
const car = { brand, model };

console.log(car); // { brand: "Ford", model: "Mustang" }
```

## Operador spread (`...`) en Objetos

El operador **spread** permite copiar, combinar y extender objetos de forma concisa.

### Clonar objetos (copia superficial - shallow copy)

```js
const car = { brand: "Ford", model: "Mustang", year: 2022 };
const newCar = { ...car, color: "Red" };

console.log(newCar);
// { brand: "Ford", model: "Mustang", year: 2022, color: "Red" }
```

### Combinar objetos y sobrescribir propiedades

Si dos objetos tienen propiedades con el mismo nombre, **la última declaración sobrescribe la anterior**.

```js
const base = { color: "Red", year: 2020 };
const extra = { year: 2022 };

const result = { ...base, ...extra };
console.log(result);
// { color: "Red", year: 2022 }
```

### Comparación de referencias

Un objeto clonado con spread es **un objeto nuevo e independiente** (copia superficial).

```js
const user1 = { name: "Armando", age: 24 };
const user2 = { ...user1 };

console.log(user1 === user2); // false → son objetos distintos
```

### Referencia vs. Copia

- **Sin el operador spread**, se pasa la referencia del objeto original, los cambios afectan al original y al destino.
- **Con el operador spread**, se copia el objeto, los cambios posteriores en el original no afectan la copia.

```js
const product = { name: "Tablet", price: 300 };

const cartRef = { quantity: 1, product }; // product es una referencia
const cartCopy = { quantity: 1, ...product }; // copia de propiedades

product.price = 800;

console.log(cartRef.product.price); // 800 → el cambio afecta al objeto original
console.log(cartCopy.price); // 300 → la copia es independiente
```

>**Advertencia:** El spread crea una **copia superficial** (shallow copy). Si el objeto tiene propiedades que son objetos o arreglos, estos se copian por referencia. Para copias profundas, necesitas herramientas como `structuredClone()` o librerías como Lodash.
