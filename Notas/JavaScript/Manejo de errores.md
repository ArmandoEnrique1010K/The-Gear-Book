---
orden: 31
tags:
  - Errores
Comentario:
estado: true
---

## El objeto global `Error`

El objeto `Error` es el constructor base para todos los errores en JavaScript. Es un objeto nativo que proporciona información estandarizada sobre lo que salió mal durante la ejecución del código.

### Propiedades principales

- **`name`**: Cadena que indica el tipo de error (ej: `"TypeError"`, `"ReferenceError"`).
- **`message`**: Descripción legible del error.
- **`stack`**: Traza de la pila de llamadas (muy útil para depuración, aunque no es estándar en todos los entornos).

### Tipos de errores incorporados

JavaScript proporciona varios constructores de error especializados:

| Constructor      | Cuándo ocurre                                        |
| ---------------- | ---------------------------------------------------- |
| `SyntaxError`    | Error de sintaxis en el código                       |
| `ReferenceError` | Se hace referencia a una variable no definida        |
| `TypeError`      | Operación realizada con un tipo de dato incorrecto   |
| `RangeError`     | Valor fuera del rango permitido                      |
| `URIError`       | Error en funciones de URI (`encodeURI`, `decodeURI`) |
| `EvalError`      | Uso incorrecto de `eval()` (raro hoy en día)         |

```js
// Creando e inspeccionando un objeto Error
const customError = new Error('Database connection failed');
console.log(customError.name);      // "Error"
console.log(customError.message);   // "Database connection failed"
console.log(customError.stack);     // Información de la traza de pila
```

## `try`, `catch` y  `finally`

Son las palabras clave que conforman el bloque de manejo de excepciones en JavaScript. Permiten ejecutar código que podría fallar y manejar los errores de forma controlada sin que la aplicación se detenga abruptamente.

Sintaxis:

```js
try {
  // Código que podría lanzar un error
  const result = riskyOperation();
  console.log('Operation successful:', result);
} catch (error) {
  // Código que se ejecuta si ocurre un error
  console.error('Error caught:', error.message);
} finally {
  // Código que SIEMPRE se ejecuta, haya o no error
  console.log('Cleanup completed');
}
```

### Flujo de ejecución

| Situación | try                              | catch      | finally            |
| --------- | -------------------------------- | ---------- | ------------------ |
| Sin error | Se ejecuta completo              | Se omite   | Siempre se ejecuta |
| Con error | Se detiene en el punto del error | Se ejecuta | Siempre se ejecuta |

### Casos de uso típicos

- **`try`**: Operaciones que pueden fallar (acceso a API, lectura de archivos, parsing de JSON).
- **`catch`**: Registro de errores, mostrar mensajes amigables al usuario, intentar una estrategia alternativa.
- **`finally`**: Cerrar conexiones, liberar memoria, limpiar temporizadores, ocultar indicadores de carga.

```js
// Ejemplo práctico con parseo de JSON
function parseUserData(jsonString) {
  let userData = null;
  let parseError = null;
  
  try {
    userData = JSON.parse(jsonString);
    console.log('User data parsed successfully');
  } catch (error) {
    parseError = error;
    console.error('Failed to parse JSON:', error.message);
    // Devolver un objeto por defecto como fallback
    userData = { id: 0, name: 'Unknown' };
  } finally {
    console.log('Parse attempt completed');
    // Siempre registrar el intento
    logParseAttempt(jsonString, parseError !== null);
  }
  
  return userData;
}

function logParseAttempt(input, hadError) {
  // Función para registrar los intentos de parseo
  console.log(`Input length: ${input.length}, Had error: ${hadError}`);
}
```

>⚠️ Nota: El bloque `catch` solo captura errores síncronos. Para errores en promesas o `async/await`, se necesita un enfoque diferente.

## `Throw`

`throw` es la palabra clave que permite **lanzar manualmente** un error en cualquier punto del código. Esto es útil para validar condiciones y detener la ejecución cuando algo no cumple con los requisitos esperados.

Sintaxis:

```js
throw expression;
```

La `expression` puede ser cualquier valor, pero **se recomienda siempre usar instancias de `Error`** para mantener la trazabilidad y compatibilidad con herramientas de depuración.

### Tipos de valores que se pueden lanzar

| Tipo                 | Ejemplo                                   | ¿Recomendado?                     |
| -------------------- | ----------------------------------------- | --------------------------------- |
| Objeto `Error`       | `throw new Error('Invalid input')`        | Sí (mejor práctica)               |
| Cadena de texto      | `throw 'Error: Invalid input'`            | No (pierde información de pila)   |
| Número               | `throw 404`                               | No (poco descriptivo)             |
| Objeto personalizado | `throw { code: 400, msg: 'Bad Request' }` | Aceptable pero mejor usar `Error` |

### Validación de entrada

```js
// Función que valida la edad de un usuario
function validateAge(age) {
  if (typeof age !== 'number') {
    throw new TypeError('Age must be a number');
  }
  
  if (age < 0) {
    throw new RangeError('Age cannot be negative');
  }
  
  if (age < 18) {
    throw new Error('User must be at least 18 years old');
  }
  
  return true;
}

// Usando la validación
try {
  validateAge(16);
} catch (error) {
  console.error(`Validation failed: ${error.name} - ${error.message}`);
  // Salida: Validación fallida: Error - El usuario debe tener al menos 18 años
}
```

### Validación de configuración

```js
// Validando la configuración del entorno
function loadConfig(config) {
  if (!config.apiKey) {
    throw new Error('API key is required in configuration');
  }
  
  if (!config.endpoint) {
    throw new Error('Endpoint URL is required in configuration');
  }
  
  // Devolver la configuración validada
  return {
    apiKey: config.apiKey,
    endpoint: config.endpoint,
    timeout: config.timeout || 5000
  };
}

try {
  const config = loadConfig({ apiKey: 'abc123' });
  console.log('Config loaded:', config);
} catch (error) {
  console.error('Configuration error:', error.message);
  // Salida: Error de configuración: La URL del endpoint es requerida en la configuración
}
```

### Buenas prácticas con `throw`

1. **Siempre usa `new Error()`** en lugar de lanzar strings o valores primitivos.
2. **Sé específico**: Usa tipos específicos como `TypeError`, `RangeError` cuando corresponda.
3. **Proporciona mensajes claros** que ayuden a identificar el problema rápidamente.
4. **No abuses de `throw`** para flujo de control normal; úsalo solo para condiciones excepcionales.

## Errores personalizados (Custom Errors)

Los errores nativos son genéricos. Crear errores personalizados permite:

- Añadir propiedades específicas del dominio (códigos de error, niveles de severidad, etc.)
- Categorizar errores para manejarlos de manera diferente en `catch`.
- Mejorar la depuración con información contextual adicional.

Para crear un error personalizado, se debe **extender la clase `Error`** y asegurarse de:

1. Llamar a `super(message)` en el constructor.
2. Establecer `this.name` al nombre de la clase personalizada.
3. Opcionalmente, añadir propiedades adicionales.

```js
// Error personalizado para problemas relacionados con API
class ApiError extends Error {
  constructor(statusCode, message, details = null) {
    super(message);  // Llamar al constructor padre
    this.name = 'ApiError';  // Sobrescribir el nombre por defecto
    this.statusCode = statusCode;
    this.details = details;
    this.timestamp = new Date().toISOString();
    
    // Mantener la traza de pila adecuada
    if (Error.captureStackTrace) {
      Error.captureStackTrace(this, ApiError);
    }
  }
}

// Errores personalizados más específicos
class ValidationError extends Error {
  constructor(field, message) {
    super(`Validation failed for '${field}': ${message}`);
    this.name = 'ValidationError';
    this.field = field;
    this.isValidationError = true;
  }
}

class DatabaseError extends Error {
  constructor(operation, originalError) {
    super(`Database ${operation} failed: ${originalError.message}`);
    this.name = 'DatabaseError';
    this.operation = operation;
    this.originalError = originalError;
    this.isDatabaseError = true;
  }
}
```

### Uso practico de errores personalizados

```js
// Función que utiliza errores personalizados
function fetchUserData(userId) {
  if (!userId || typeof userId !== 'string') {
    throw new ValidationError('userId', 'Must be a non-empty string');
  }
  
  try {
    // Simulando una operación de base de datos
    if (userId === 'error') {
      throw new Error('Connection timeout');
    }
    
    // Simular recuperación exitosa de datos
    return { id: userId, name: 'John Doe', email: 'john@example.com' };
  } catch (error) {
    throw new DatabaseError('fetchUser', error);
  }
}

// Manejando diferentes tipos de errores personalizados
function handleUserRequest(userId) {
  try {
    const userData = fetchUserData(userId);
    console.log('User data:', userData);
    return userData;
  } catch (error) {
    // Manejo diferente basado en el tipo de error
    if (error instanceof ValidationError) {
      console.warn(`Validation issue: ${error.message}`);
      console.warn(`Field: ${error.field}`);
      // Devolver usuario por defecto para errores de validación
      return { id: userId, name: 'Guest' };
    }
    
    if (error instanceof DatabaseError) {
      console.error(`Database issue: ${error.message}`);
      console.error(`Operation: ${error.operation}`);
      // Lógica de reintento o fallback
      console.log('Attempting to use cached data...');
      return null;
    }
    
    // Error inesperado, relanzar
    throw error;
  }
}

// Probando el manejo de errores
console.log(handleUserRequest('123'));        // Caso exitoso
console.log(handleUserRequest(''));           // ValidationError
console.log(handleUserRequest('error'));      // DatabaseError
```

### Jerarquía de errores personalizados

```js
// Creando una jerarquía de errores personalizados
class AppError extends Error {
  constructor(message, code = 'APP_ERROR') {
    super(message);
    this.name = 'AppError';
    this.code = code;
  }
}

class NetworkError extends AppError {
  constructor(message) {
    super(message, 'NETWORK_ERROR');
    this.name = 'NetworkError';
  }
}

class AuthenticationError extends AppError {
  constructor(message) {
    super(message, 'AUTH_ERROR');
    this.name = 'AuthenticationError';
  }
}

// Usando la jerarquía
try {
  throw new AuthenticationError('Invalid token');
} catch (error) {
  if (error instanceof AuthenticationError) {
    console.log('Authentication failure:', error.message);
  } else if (error instanceof NetworkError) {
    console.log('Network issue:', error.message);
  } else if (error instanceof AppError) {
    console.log('Application error:', error.message, error.code);
  } else {
    console.log('Unexpected error:', error);
  }
}
```

### Buenas prácticas para errores personalizados

1. **Extiende siempre de `Error`**, nunca de objetos planos.
2. **Mantén el `name` actualizado** al nombre de tu clase.
3. **Añade propiedades útiles** pero no excesivas (statusCode, field, etc.).
4. **Usa `instanceof`** para diferenciar tipos de errores.
5. **Documenta tus errores personalizados** para que otros desarrolladores sepan cómo usarlos.
6. **Considera usar una jerarquía** (AppError → NetworkError → etc.) para mayor flexibilidad.

## Ejemplo combinado de manejo de errores

```js
// Ejemplo completo combinando todos los conceptos
class PaymentError extends Error {
  constructor(transactionId, amount, message) {
    super(`Payment failed for transaction ${transactionId}: ${message}`);
    this.name = 'PaymentError';
    this.transactionId = transactionId;
    this.amount = amount;
    this.timestamp = new Date();
    this.isRetryable = amount < 1000;
  }
}

function processPayment(transactionId, amount) {
  // Validar entradas
  if (!transactionId || typeof transactionId !== 'string') {
    throw new TypeError('Transaction ID must be a non-empty string');
  }
  
  if (typeof amount !== 'number' || amount <= 0) {
    throw new RangeError('Amount must be a positive number');
  }
  
  // Simular procesamiento de pago
  if (amount > 5000) {
    throw new PaymentError(transactionId, amount, 'Amount exceeds maximum limit');
  }
  
  if (amount > 2000 && amount <= 5000) {
    throw new PaymentError(transactionId, amount, 'Requires manual approval');
  }
  
  // Pago exitoso
  return {
    transactionId,
    amount,
    status: 'approved',
    approvalCode: `APP-${Date.now()}`
  };
}

// Ejecución principal con manejo completo de errores
function executePayment(transactionId, amount) {
  let paymentResult = null;
  
  try {
    console.log(`Processing payment for ${transactionId}...`);
    paymentResult = processPayment(transactionId, amount);
    console.log('Payment approved:', paymentResult);
    return paymentResult;
  } catch (error) {
    // Manejar diferentes tipos de error
    if (error instanceof TypeError) {
      console.error('Type error:', error.message);
    } else if (error instanceof RangeError) {
      console.error('Range error:', error.message);
    } else if (error instanceof PaymentError) {
      console.error(`Payment error (retryable: ${error.isRetryable}):`, error.message);
      console.error(`   Transaction: ${error.transactionId}, Amount: ${error.amount}`);
      
      // Si es reintentable, intentar recuperación
      if (error.isRetryable) {
        console.log('Retry attempt...');
        try {
          paymentResult = processPayment(transactionId, amount + 1);
          console.log('Retry successful:', paymentResult);
          return paymentResult;
        } catch (retryError) {
          console.error('Retry failed:', retryError.message);
        }
      }
    } else {
      console.error('Unexpected error:', error);
      throw error; // Relanzar si no podemos manejarlo
    }
    
    // Devolver resultado de fallback si todos los intentos fallan
    return { transactionId, amount, status: 'failed', reason: error.message };
  } finally {
    console.log(`Payment attempt logged for ${transactionId} at ${new Date().toISOString()}`);
  }
}

// Probar el flujo completo
console.log('=== TEST 1: Valid payment ===');
executePayment('TXN-001', 1500);

console.log('\n=== TEST 2: Invalid amount ===');
executePayment('TXN-002', -100);

console.log('\n=== TEST 3: Payment requiring retry ===');
executePayment('TXN-003', 2500);

console.log('\n=== TEST 4: Payment exceeding limit ===');
executePayment('TXN-004', 6000);
```
