---
orden: 6
tags:
  - Datos
---

## Operadores Aritméticos

Realizan operaciones matemáticas básicas entre valores o variables.

| Operador | Nombre         | Descripción                                                          |
| -------- | -------------- | -------------------------------------------------------------------- |
| `+`      | Suma           | Suma dos números o **concatena** cadenas de texto                    |
| `-`      | Resta          | Resta el segundo valor del primero                                   |
| `*`      | Multiplicación | Multiplica dos números                                               |
| `/`      | División       | Divide el primer número entre el segundo                             |
| `%`      | Módulo         | Devuelve el **resto** de una división                                |
| `**`     | Potencia (ES6) | Eleva el primer número a la potencia del segundo                     |
| `++`     | Incremento     | Aumenta el valor de una variable en `1` (puede ser prefijo o sufijo) |
| `--`     | Decremento     | Disminuye el valor de una variable en `1`                            |

```javascript
let a = 12, b = 3;
console.log(a + b);   // 15
console.log(a - b);   // 9
console.log(a * b);   // 36
console.log(a / b);   // 4
console.log(a % b);   // 0
console.log(a ** b);  // 1728
console.log(++a);     // 13 (primero incrementa, luego muestra)
console.log(--b);     // 2  (primero decrementa, luego muestra)
```

## Operadores de Asignación

Modifican el valor de una variable aplicando una operación aritmética y reasignando el resultado.

| Operador | Nombre                      | Descripción                                                  |
| -------- | --------------------------- | ------------------------------------------------------------ |
| `=`      | Asignación simple           | Asigna el valor de la derecha a la variable de la izquierda. |
| `+=`     | Suma y asignación           | `x += y` equivale a `x = x + y`                              |
| `-=`     | Resta y asignación          | `x -= y` equivale a `x = x - y`                              |
| `*=`     | Multiplicación y asignación | `x *= y` equivale a `x = x * y`                              |
| `/=`     | División y asignación       | `x /= y` equivale a `x = x / y`                              |
| `%=`     | Módulo y asignación         | `x %= y` equivale a `x = x % y`                              |
| `**=`    | Potencia y asignación       | `x **= y` equivale a `x = x ** y`                            |

```javascript
let contador = 10;
let valor = 5;

contador += valor;  // 15
contador -= valor;  // 10
contador *= valor;  // 50
contador /= valor;  // 10
contador %= valor;  // 0

contador = 2;
contador **= valor; // 32
```

## **Operadores de Comparación**

Comparan dos valores y devuelven `true` o `false`.

| Operador | Nombre               | Descripción                                            |
| -------- | -------------------- | ------------------------------------------------------ |
| ``==``   | Igualdad débil       | Compara solo el valor, convierte tipos automáticamente |
| `===`    | Igualdad estricta    | Compara valor **y** tipo. **Recomendado**              |
| `!=`     | Desigualdad débil    | Compara si son distintos, convierte tipos              |
| `!==`    | Desigualdad estricta | Compara valor o tipo distinto. **Recomendado**         |
| `>`      | Mayor que            | `true` si el izquierdo es mayor que el derecho         |
| `<`      | Menor que            | `true` si el izquierdo es menor que el derecho         |
| `>=`     | Mayor o igual        | `true` si el izquierdo es mayor o igual al derecho     |
| `<=`     | Menor o igual        | `true` si el izquierdo es menor o igual al derecho     |

```javascript
console.log("5" == 5);   // true  (convierte "5" a número)
console.log("5" === 5);  // false (tipos distintos)
console.log("5" != 3);   // true
console.log("5" !== 5);  // true (tipo distinto)
console.log(10 > 5);     // true
console.log(10 < 5);     // false
console.log(10 >= 10);   // true
console.log(5 <= 3);     // false
```
