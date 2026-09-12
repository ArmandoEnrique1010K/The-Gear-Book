---
orden:
tags:
Comentario:
estado:
---

## Error vs Excepción

Un **error** es una condición anómala que ocurre durante la ejecución del programa. Representa un problema real: un dato inválido, una división por cero, un recurso no disponible, etc. En JavaScript, los errores son representados por objetos que heredan de `Error`.

Una **excepción** es el **mecanismo de control** que se activa cuando un error es lanzado (`throw`). Es el flujo que interrumpe la ejecución normal del programa y viaja por la pila de llamadas hasta encontrar un manejador (`catch`).

### Analogía práctica

Imagina que un **error** es un incendio (el problema real). La **excepción** es la alarma que se activa y recorre el edificio avisando. El **manejo de errores** es el protocolo que sigue el personal para evacuar y controlar la situación.

Aunque conceptualmente son distintos, en JavaScript se usan casi como sinónimos. Cuando algo falla, se **lanza una excepción** que **transporta un objeto Error**. Por eso decimos "capturar una excepción" y "manejar un error".

```js
// El ERROR es la condición: dividir entre cero conceptualmente es inválido
function divide(a, b) {
  if (b === 0) {
    // La EXCEPCIÓN es el mecanismo que lanzamos aquí
    throw new Error('No se puede dividir entre cero');
  }
  return a / b;
}

// El MANEJO es lo que hacemos al capturar la excepción
try {
  const result = divide(10, 0);
  console.log('Resultado:', result);
} catch (error) {
  // Aquí manejamos el error que viajó como excepción
  console.error('Operación inválida:', error.message);
}
```

### Buenas practicas

- Piensa en el **error** como el "qué" y en la **excepción** como el "cómo se transporta".
- No todas las condiciones anómalas deben ser excepciones (algunas se manejan con valores de retorno).
- Usa excepciones para **situaciones verdaderamente excepcionales**, no para flujo normal.

## Propagación de errores

La **propagación** (o burbujeo) es el mecanismo por el cual un error que no ha sido capturado en el nivel actual **sube hacia el contexto superior** (la función que llamó a la actual). Si tampoco se captura ahí, sigue subiendo hasta llegar al nivel más alto.

Cuando una función lanza un error y no lo captura:

1. El error interrumpe la ejecución de esa función.
2. El error "burbujea" hacia la función que la llamó.
3. Si esa función tampoco lo captura, sigue subiendo.
4. Si llega al nivel superior (global) sin ser capturado, el programa se detiene con un error no manejado.

```js
// Nivel 3: La función más profunda lanza el error
function levelThree() {
  throw new Error('Algo falló en el nivel 3');
}

// Nivel 2: No captura, el error burbujea hacia arriba
function levelTwo() {
  console.log('Entrando al nivel 2');
  levelThree();  // El error sube desde aquí
  console.log('Esto nunca se ejecuta');
}

// Nivel 1: No captura, el error sigue subiendo
function levelOne() {
  console.log('Entrando al nivel 1');
  levelTwo();
  console.log('Esto tampoco se ejecuta');
}

// Nivel 0: Aquí capturamos el error que burbujeó desde el nivel 3
try {
  levelOne();
} catch (error) {
  console.error('Error capturado en el nivel superior:', error.message);
  // Salida: Error capturado en el nivel superior: Algo falló en el nivel 3
}
```

### Propagación con captura intermedia

```js
// Nivel 3: Lanza el error
function fetchData() {
  throw new Error('Fallo de red');
}

// Nivel 2: Captura, enriquece y relanza
function processData() {
  try {
    fetchData();
  } catch (error) {
    // Enriquecer el error con contexto adicional
    error.context = 'Ocurrió al procesar datos del usuario';
    // Relanzar para que siga propagándose
    throw error;
  }
}

// Nivel 1: Captura final
function handleRequest() {
  try {
    processData();
  } catch (error) {
    console.error('Error:', error.message);
    console.error('Contexto:', error.context);
    // Salida:
    // Error: Fallo de red
    // Contexto: Ocurrió al procesar datos del usuario
  }
}

handleRequest();
```

>Nota: Si no se captura el error, en el navegador, el error aparece en consola, pero el resto del script puede seguir si esta en otro bloque.

### Buenas prácticas

- **Captura en el nivel adecuado**: no tan abajo que pierdas contexto, no tan arriba que ocultes problemas.
- **Relanza con contexto**: si capturas y relanzas, añade información útil.
- **No captures y silencies**: un `catch` vacío es una mala práctica.
- **Documenta qué errores puede lanzar cada función** cuando sea relevante.

## Manejo de errores asíncronos

El manejo de errores síncronos con `try/catch` **no funciona** directamente con código asíncrono basado en callbacks, porque el `try/catch` termina su ejecución antes de que el callback se ejecute. Con promesas y `async/await` sí funciona, pero con matices.

MEJORAR ESTA SECCION PARA UN ENTORNO FRONTEND
