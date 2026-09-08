---
orden: 19
tags:
  - Objetos
Comentario:
estado: true
---

## Crear objetos con el constructor `Object`

Los objetos pueden crearse usando el constructor `Object`, aunque la **sintaxis literal** (`{}`) es la más utilizada por su simplicidad y legibilidad.

```js
let person = new Object();
person.name = 'Carlos';
person.address = 'Saturno 15';
person.phone = '55443322';

console.log(person.phone); // 55443322
```

### Comparación con literales

Ambas formas crean objetos equivalentes, pero la sintaxis literal es **recomendada** por su claridad.

```js
// Constructor Object
let obj1 = new Object();
obj1.property = 'value';

// Sintaxis literal (recomendada)
let obj2 = { property: 'value' };

console.log(typeof obj1); // object
console.log(typeof obj2); // object
```

## Métodos abreviados (Enhanced Object Literals)

**ES6** introdujo una sintaxis más concisa para definir métodos dentro de objetos, eliminando la necesidad de la palabra clave `function` y los dos puntos.

```js
// Tradicional (antes de ES6)
const person = {
  name: 'Juan',
  greet: function() {
    return `Hola, soy ${this.name}`;
  }
};

// Abreviada (ES6 - recomendada)
const person = {
  name: 'Juan',
  greet() {
    return `Hola, soy ${this.name}`;
  }
};
```

### Ventajas de los métodos abreviados

- Sintaxis más limpia y legible.
- Mantienen correctamente el contexto de `this`.
- Son la forma recomendada en JavaScript moderno.

```js
const calculator = {
  value: 0,
  add(amount) {
    this.value += amount;
    return this;
  },
  subtract(amount) {
    this.value -= amount;
    return this;
  },
  getResult() {
    return this.value;
  }
};

console.log(calculator.add(5).subtract(2).getResult()); // 3
```

## Propiedades computadas en Objetos

Las **propiedades computadas** permiten definir dinámicamente el nombre de una propiedad de un objeto utilizando **expresiones** dentro de corchetes `[]`.

```js
const key = "email";
const value = "carlos@email.com";

const user = {
  name: "Carlos",
  // El nombre de la propiedad se "computa" usando la variable
  [key]: value
};

console.log(user.email); // "carlos@email.com"
```

### Uso con funciones

```js
const getKey = (prefix, suffix) => `${prefix}_${suffix}`;

const data = {
  [getKey("user", "id")]: 101,
  [getKey("user", "name")]: "Ana"
};

console.log(data.user_id);   // 101
console.log(data.user_name); // "Ana"
```

## Métodos `get` y `set` (Getters y Setters)

Los métodos `get` y `set` permiten **controlar cómo se accede y modifica** una propiedad dentro de un objeto.

- **`get`**: obtiene o calcula un valor al acceder a una propiedad.
- **`set`**: ejecuta lógica o validaciones antes de modificar una propiedad.

**Usos comunes:**

- Controlar el acceso a propiedades privadas.
- Validar datos antes de asignarlos.
- Crear propiedades calculadas dinámicamente.

```js
let person = {
  name: 'Juan',
  lastName: 'Perez',
  _language: 'es', // Convención: prefijo "_" para propiedades internas
  
  get fullName() {
    return `${this.name} ${this.lastName}`;
  },
  
  get lang() {
    return this._language.toUpperCase();
  },
  
  set lang(lang) {
    const validLanguages = ['es', 'en', 'fr'];
    if (validLanguages.includes(lang.toLowerCase())) {
      this._language = lang.toUpperCase();
    } else {
      console.log('Invalid language');
    }
  },
  
  greet() {
    return `Hola, soy ${this.fullName}`;
  }
};

console.log(person.fullName); // Juan Perez
console.log(person.lang);     // ES
person.lang = 'en';
console.log(person.lang);     // EN
person.lang = 'aleman';       // Invalid language
```

## Funciones Constructoras

Las funciones constructoras actúan como **plantillas** para crear múltiples objetos con la misma estructura.

```js
function Person(name, lastName, email) {
  this.name = name;
  this.lastName = lastName;
  this.email = email;
  
  // Método definido dentro del constructor (no recomendado)
  this.fullName = function() {
    return `${this.name} ${this.lastName}`;
  };
}
```

> **Nota:** Definir métodos dentro del constructor **no es eficiente**, ya que cada instancia crea su propia copia del método. La forma recomendada es usar el **prototype**.

### Creación de instancias

Cada instancia es un **objeto independiente** con sus propias propiedades.

```js
let father = new Person('Juan', 'Perez', 'jperez@mail.com');
let mother = new Person('Laura', 'Quintero', 'lquintero@mail.com');

console.log(father.fullName()); // Juan Perez
console.log(mother.fullName()); // Laura Quintero

// Modificación de propiedades
father.name = 'Carlos';
console.log(father.fullName()); // Carlos Perez
```

## El operador `new`

El operador `new` permite crear instancias a partir de funciones constructoras o clases.

**Lo que hace `new`:**

1. Crea un nuevo objeto vacío.
2. Enlaza `this` a la nueva instancia.
3. Ejecuta el constructor.
4. Devuelve el objeto automáticamente.

### Comparación de métodos de creación de objetos

Aunque JavaScript posee constructores nativos (`Object`, `Array`, `String`, etc.), se recomienda usar **sintaxis literal** por simplicidad y legibilidad.

```js
// Objetos
let obj1 = new Object();
let obj2 = {}; // recomendado

// Strings
let str1 = new String('Hola');
let str2 = 'Hola'; // recomendado

// Números
let num1 = new Number(1);
let num2 = 1; // recomendado

// Booleanos
let bool1 = new Boolean(false);
let bool2 = false; // recomendado

// Arrays
let arr1 = new Array();
let arr2 = []; // recomendado

// Funciones
let fn1 = new Function('a', 'b', 'return a + b');
let fn2 = (a, b) => a + b; // recomendado
```

## Prototype y herencia prototípica

La propiedad `prototype` de una función constructora permite **compartir propiedades y métodos** entre todas las instancias creadas a partir de ella.

- Evita duplicar métodos en memoria.
- Forma la base de la **herencia prototípica** en JavaScript.

```js
function Person(name, lastName, email) {
  this.name = name;
  this.lastName = lastName;
  this.email = email;
}

// Propiedad compartida
Person.prototype.phone = '00000000';

// Métodos compartidos
Person.prototype.fullName = function() {
  return `${this.name} ${this.lastName}`;
};

Person.prototype.greet = function() {
  return `Hola, soy ${this.fullName()}`;
};
```

### Instancias y cadena de prototipos

Las instancias pueden acceder a propiedades y métodos del `prototype`. También pueden sobrescribir propiedades heredadas.

```js
let father = new Person('Juan', 'Perez', 'jperez@mail.com');
let mother = new Person('Laura', 'Quintero', 'lquintero@mail.com');

// Sobrescribir propiedad del prototype
father.phone = '11223344';
mother.phone = '66889900';

console.log(father.fullName()); // Juan Perez
console.log(mother.greet());    // Hola, soy Laura Quintero

// Verificar la cadena de prototipos
console.log(father.hasOwnProperty('name')); // true
console.log(father.hasOwnProperty('fullName')); // false (está en el prototype)
```

## Métodos `call` y `apply` – Préstamo de métodos

Permiten **invocar un método de un objeto en otro contexto**, es decir, "prestar" métodos.

### Método `call`

Pasa los argumentos de forma **individual**.

```js
let person1 = {
  name: 'Juan',
  lastName: 'Perez',
  fullName: function(title, phone) {
    return `${title}: ${this.name} ${this.lastName}, ${phone}`;
  }
};

let person2 = { name: 'Carlos', lastName: 'Lara' };

console.log(person1.fullName('Lic.', '44332288'));
// Lic.: Juan Perez, 44332288

console.log(person1.fullName.call(person2, 'Ing.', '5544332211'));
// Ing.: Carlos Lara, 5544332211
```

### Método `apply`

Funciona igual que `call`, pero recibe los argumentos en un **array**.

```js
console.log(person1.fullName.apply(person2, ['Dr.', '9988776655']));
// Dr.: Carlos Lara, 9988776655

// Ejemplo práctico con Math.max
let numbers = [1, 5, 3, 9, 2];
console.log(Math.max.apply(null, numbers)); // 9

// Forma moderna con spread
console.log(Math.max(...numbers)); // 9
```

## Ejemplo integrado

Sistema de gestión de personas que incluye constructor, prototype, getters/setters y préstamo de métodos.

```js
function Person(name, lastName, age) {
  this.name = name;
  this.lastName = lastName;
  this.age = age;
  this.id = Date.now();
}

// Métodos en prototype
Person.prototype.fullName = function() {
  return `${this.name} ${this.lastName}`;
};

Person.prototype.isAdult = function() {
  return this.age >= 18;
};

Person.prototype.toString = function() {
  return `Person: ${this.fullName()} (${this.age} years old)`;
};

// Getters y setters en instancias (o en prototype)
Person.prototype.getInfo = function() {
  return {
    fullName: this.fullName(),
    age: this.age,
    isAdult: this.isAdult()
  };
};

// Instancias
let employee1 = new Person('Ana', 'Garcia', 28);
let employee2 = new Person('Luis', 'Martinez', 17);

console.log(employee1.fullName());   // Ana Garcia
console.log(employee1.isAdult());    // true
console.log(employee2.isAdult());    // false
console.log(employee1.toString());   // Person: Ana Garcia (28 years old)

// Préstamo de método
let context = { name: 'External', lastName: 'Context' };
console.log(Person.prototype.fullName.call(context)); // External Context
```

## Buenas Prácticas con conceptos avanzados de objetos

- **Usa métodos abreviados (`method() {}`)** para definir métodos dentro de objetos, en lugar de `function() {}`. Es más limpio, moderno y mantiene correctamente el contexto de `this`.
- **Utiliza funciones constructoras o clases** cuando necesites crear múltiples objetos con la misma estructura.
- **Declara métodos en el `prototype`** para evitar duplicarlos en memoria y aprovechar la herencia prototípica.
- **Usa getters y setters** para controlar el acceso a propiedades y validar datos antes de asignarlos.
- **Aplica `call` y `apply`** para reutilizar métodos en distintos contextos sin duplicar código.
- **Prefiere el operador spread (`...`)** sobre `apply` cuando sea posible (ej. `Math.max(...numbers)`).
- **Nombra los métodos con verbos** que indiquen acciones (ej. `calculateTotal()`, `showDetails()`, `validateUser()`).
