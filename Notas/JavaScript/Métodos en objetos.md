---
orden: 18
tags:
  - Objetos
Comentario:
estado: true
---

## ¿Qué es un método?

En JavaScript, los objetos pueden contener **funciones como valores** de sus propiedades. Cuando una función es propiedad de un objeto, se le llama **método**.

Los métodos permiten que los objetos **realicen acciones** o **procesen sus propios datos**.

### El operador `this` en objetos

Dentro de un método, `this` hace **referencia al objeto que contiene el método**, permitiendo acceder a sus propiedades internas.

```js
const person = {
  name: "Carlos",
  greet: function() {
    return `Hi, I'm ${this.name}`;
  }
};

console.log(person.greet()); // "Hi, I'm Carlos"
```

### Arrow functions y `this`

Las **arrow functions** no tienen su propio `this`, sino que heredan el `this` del contexto exterior. Por lo tanto, dentro de un método, usar `this` en una arrow function puede causar errores.

La solución es utilizar el nombre del objeto para acceder a sus propiedades.

```js
const person = {
  name: "Carlos",
  greet: () => {
    // Usa el nombre del objeto para acceder a la propiedad
    return `Hi, I'm ${person.name}`;
  }
};

console.log(person.greet()); // "Hi, I'm Carlos"
```

>**Recomendación:** Prefiere **function expressions** o **métodos abreviados** (ES6) para definir métodos, ya que las arrow functions no tienen su propio `this` y pueden causar comportamientos inesperados.

```js
const person = {
  name: "Carlos",
  // Método abreviado (recomendado)
  greet() {
    return `Hi, I'm ${this.name}`;
  }
};
```

### Métodos que procesan datos del objeto

Puedes crear métodos que manipulen o calculen información dentro de un objeto usando `this`.

```js
const invoice = {
  items: [
    { product: "keyboard", price: 400, quantity: 2 },
    { product: "mouse", price: 200, quantity: 1 },
  ],

  total() {
    let total = 0;
    this.items.forEach(item => {
      total += item.price * item.quantity;
    });
    return total;
  }
};

console.log(invoice.total()); // 1000
```

## Desestructuración en funciones y métodos

La **desestructuración** permite extraer propiedades de un objeto de forma directa, simplificando el acceso a los datos.

### Desestructuración en parámetros de función

Permite extraer propiedades del objeto que se pasa como argumento directamente en la firma de la función.

```js
const user = {
  username: "andres",
  email: "correo@google.com"
};

// Desestructuración directa en los parámetros
const showUserDetails = ({ username, email }) => {
  console.log(`User ${username} with email ${email}`);
};

showUserDetails(user);
// "User andres with email correo@google.com"
```

> **Nota:** El objeto pasado como argumento debe tener las mismas propiedades que se están desestructurando.

### Desestructuración dentro de un método

Puedes usar desestructuración al acceder a las propiedades internas de un objeto con `this`, haciendo el código más limpio y legible.

```js
const invoice = {
  client: {
    name: "Jhon",
    lastName: "Doe",
    age: 20
  },

  showClient() {
    const { name, lastName } = this.client;
    return `Client: ${name} ${lastName}`;
  }
};

console.log(invoice.showClient()); // "Client: Jhon Doe"
```

## Métodos de inmutabilidad

La **inmutabilidad** significa que un objeto no puede ser modificado después de su creación. JavaScript proporciona dos métodos para controlar la mutabilidad.

### `Object.freeze()`

Impide **modificar, agregar o eliminar** propiedades. El objeto se vuelve completamente **inmutable**.

```js
const car = Object.freeze({ brand: "Ford" });

car.brand = "Chevrolet"; // No tiene efecto (en modo estricto lanza error)
console.log(car.brand); // "Ford"
```

### `Object.seal()`

**Impide agregar o eliminar** propiedades, pero **permite modificar** las existentes.

```js
const sealedCar = Object.seal({ brand: "Ford" });

sealedCar.brand = "Chevrolet"; // Se puede modificar
delete sealedCar.brand;       // No tiene efecto
console.log(sealedCar.brand); // "Chevrolet"
```

## Unir objetos (Combinación)

Puedes combinar las propiedades de dos o más objetos en uno nuevo usando tres enfoques:

### `Object.assign()`

Copia las propiedades de uno o más objetos a un objeto destino.

```js
const client = { name: "Ana", age: 30 };
const extraData = { age: 32, city: "Lima", premium: true };

const updatedClient = Object.assign(client, extraData);
console.log(updatedClient);
// { name: "Ana", age: 32, city: "Lima", premium: true }
```

### Evitar mutación del objeto original

```js
const client = { name: "Ana", age: 30 };
const extraData = { age: 32, city: "Lima", premium: true };

// Usa un objeto vacío como destino para no mutar 'client'
const merged = Object.assign({}, client, extraData);
console.log(merged);
// { name: "Ana", age: 32, city: "Lima", premium: true }

console.log(client); // { name: "Ana", age: 30 } (sin mutar)
```

### Operador Spread (`...`)

La forma **más moderna y limpia** de combinar objetos (ES6+).

```js
const client = { name: "Ana", age: 30 };
const extraData = { age: 32, city: "Lima", premium: true };

const updatedClient = { ...client, ...extraData };
console.log(updatedClient);
// { name: "Ana", age: 32, city: "Lima", premium: true }
```

>**Orden de sobrescritura:** Las propiedades del último objeto tienen prioridad.

## Métodos para convertir objetos en arreglos

Estos métodos son útiles para iterar, transformar o inspeccionar objetos.

### `Object.keys()` – Obtener claves

Devuelve un arreglo con los nombres de las claves del objeto.

```js
const car = { brand: "Ford", model: "Mustang", year: 2022 };

console.log(Object.keys(car)); // ["brand", "model", "year"]
```

### `Object.values()` – Obtener valores

Devuelve un arreglo con los valores de las propiedades del objeto.

```js
const car = { brand: "Ford", model: "Mustang", year: 2022 };

console.log(Object.values(car)); // ["Ford", "Mustang", 2022]
```

### `Object.entries()` – Obtener pares clave-valor

Devuelve un arreglo de pares `[clave, valor]` para cada propiedad.

```js
const car = { brand: "Ford", model: "Mustang", year: 2022 };

console.log(Object.entries(car));
// [["brand", "Ford"], ["model", "Mustang"], ["year", 2022]]
```

> Puedes iterar sobre las propiedades de un objeto utilizando `Object.entries()` junto con el método `forEach()`.

```js
const car = { brand: "Ford", model: "Mustang", year: 2022 };

Object.entries(car).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});
// brand: Ford
// model: Mustang
// year: 2022
```

## Método `Object.hasOwn()`

El método `Object.hasOwn()` es una forma moderna y segura de verificar si un objeto tiene una **propiedad propia** (no heredada) con un nombre específico.

```js
const user = {
  name: "Ana",
  age: 30
};

// Propiedad propia
console.log(Object.hasOwn(user, "name")); // true

// Propiedad no existente
console.log(Object.hasOwn(user, "email")); // false
```

## Buenas Prácticas con técnicas comunes en objetos

- **Usa métodos abreviados (`method() {}`)** para definir métodos dentro de objetos, en lugar de la sintaxis `function() {}`.
- **Prefiere function expressions o métodos abreviados** sobre arrow functions cuando necesites que el método acceda al objeto mediante `this`.
- **Aplica desestructuración** tanto en parámetros de funciones como dentro de métodos para extraer propiedades de objetos de forma concisa.
- **Utiliza `Object.freeze()`** cuando necesites objetos completamente inmutables.
- **Usa `Object.seal()`** cuando quieras evitar que se agreguen o eliminen propiedades, pero permitir la modificación de las existentes.
- **Prefiere el operador spread (`...`)** sobre `Object.assign()` para combinar o clonar objetos, ya que es más legible, moderno y fácil de mantener.
