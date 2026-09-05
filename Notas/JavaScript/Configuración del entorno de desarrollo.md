---
orden: 2
tags:
  - Introducción
Comentario: Cambiar la imagen de la consola de chrome
estado: true
---

## Navegador web recomendado

Se recomienda usar **Brave** o **Google Chrome** debido a su excelente compatibilidad con las herramientas de desarrollo y su amplio ecosistema de extensiones. Ambos navegadores incluyen motores JavaScript rápidos y modernos, y ofrecen una consola y depurador muy completos.

>💡 También son válidos **Firefox**, **Edge** o **Safari**, pero Chrome y Brave son los más utilizados en entornos de desarrollo profesional.

## Editor de código

Un buen editor de código es clave para la productividad. Debe ofrecer:

- **Autocompletado inteligente**: acelera la escritura y reduce errores tipográficos.
- **Formateo automático**: mantiene un estilo de código limpio y consistente.
- **Depuración integrada**: permite detectar y corregir errores sin salir del editor.
- **Extensiones personalizables**: añaden soporte para lenguajes, frameworks y utilidades adicionales.

## Devin Desktop (antes Windsurf)

**Windsurf ha sido reemplazado por Devin Desktop** como parte de la integración con la marca Devin. La transición es sencilla: el IDE, las extensiones y los flujos de trabajo se mantienen igual, solo cambian el nombre y la marca.

Windsurf era considerado el editor de código con IA más avanzado y popular, sucesor directo de Codeium. Se trata de un IDE inteligente y gratuito, diseñado para desarrolladores FullStack e ingenieros de IA generativa. Su principal ventaja es la alta compatibilidad con las extensiones de Visual Studio Code, lo que facilita enormemente la migración para quienes vienen de ese ecosistema.

![Devin Desktop Logo|167](../assets/Logo%20de%20Devin%20Desktop.png)

### Antecedentes del cambio

Windsurf era desarrollado por **Codeium**, una empresa fundada en 2021 que inicialmente se enfocaba en virtualización de GPU antes de pivotar hacia el mercado de asistentes de programación con IA.

En **julio de 2025**, Google contrató al CEO y al equipo central de Windsurf, y posteriormente **Cognition** adquirió el resto de los activos del producto. Esta adquisición derivó en la integración del editor bajo la marca Devin, dando lugar a **Devin Desktop**, que conserva la esencia y funcionalidades de su predecesor, pero con una identidad renovada y alineada con la visión de Cognition.

### Características destacadas:

- **Cascade y Devin Local**: el editor incluye dos agentes locales de IA. **Cascade** sigue disponible temporalmente (hasta julio), mientras que **Devin Local** es el nuevo agente que lo reemplazará progresivamente. Devin Local ofrece mayor eficiencia en el uso de tokens (hasta un 30% mejor), soporte para subagentes y la misma arquitectura que Devin CLI.
- **Modelos de última generación**: utiliza modelos avanzados como Claude Sonnet para generación, corrección y documentación de código.
- **Command (Cmd/Ctrl+I)**: función para generar o editar código en línea usando lenguaje natural, sin consumir créditos premium.
- **Vista previa en vivo y despliegue con un clic** para pruebas rápidas.
- **Entorno contextual**: comprende la estructura completa del proyecto y propone mejoras en tiempo real.

### Planes disponibles (2026):

- **Gratuito**: completaciones ilimitadas, ediciones inline ilimitadas y cuota limitada de agentes.
- **Pro**: 20 USD/mes (mensual) con cuotas ampliadas y acceso a modelos de vanguardia.
- **Teams**: 80 USD/mes base + 40 USD por usuario desarrollador.
- **Enterprise**: precios personalizados con controles avanzados y despliegue dedicado.

## Instalación de Devin Desktop

1. Visita la página oficial de Devin.
2. Haz clic en **"Download for Windows"** (o elige **macOS** o **Linux** según tu sistema).
3. Ejecuta el instalador y sigue las instrucciones del asistente.
4. Abre **Devin Desktop** desde el menú de inicio o el acceso directo.
5. Inicia sesión con tu cuenta de **Google**, **GitHub** o **correo electrónico** para activar las funciones de IA.
6. Selecciona el entorno base (ej. **JavaScript/TypeScript**, **Python** o **Fullstack**).
7. Opcionalmente, activa el modo **Cascade** o el nuevo **Devin Local**.

## Extensiones recomendadas

Las mismas extensiones de VS Code son compatibles. Se recomiendan:

| Extensión                            | Función                                               |
| ------------------------------------ | ----------------------------------------------------- |
| **Prettier - Code formatter**        | Formateo automático de código                         |
| **ESLint**                           | Detección de errores y buenas prácticas en JavaScript |
| **Live Server**                      | Recarga automática del navegador al guardar cambios   |
| **JavaScript (ES6) code snippets**   | Atajos para escribir código moderno rápido            |
| **Better Comments**                  | Resalta comentarios como `TODO`, `FIXME`, `?`, `!`    |
| **Path Intellisense**                | Sugiere rutas de archivos al escribir                 |
| **Indent-rainbow**                   | Colorea los niveles de indentación                    |
| **Bracket Pair Colorizer 2**         | Colorea pares de paréntesis, corchetes y llaves       |
| **Auto Close Tag / Auto Rename Tag** | Cierra y renombra etiquetas HTML automáticamente      |

## Entorno en el navegador

JavaScript se ejecuta directamente en **cualquier navegador moderno** (Brave, Chrome, Firefox, Edge, Safari), sin necesidad de instalar software adicional.

- Todos estos navegadores incluyen **motores de JavaScript** integrados.
- Para abrir las **herramientas de desarrollo**, presiona `F12` o `Ctrl + Shift + I` (en Windows/Linux) o `Cmd + Option + I` (en Mac).
- Desde allí puedes acceder a la **Consola**, el **depurador**, y ver el **DOM** en tiempo real.

### Ejecución de JavaScript en el navegador

Puedes insertar código JavaScript directamente en un archivo HTML usando la etiqueta `<script>`:

```html
<!DOCTYPE html>
<html>
<head>
  <title>My first script</title>
</head>
<body>
  <h1>Hello from HTML</h1>

  <script>
    console.log("Hello, JavaScript in the browser");
  </script>
</body>
</html>
```

- `console.log()` imprime mensajes en la consola del navegador, muy útil para depurar.
- Para ejecutar, haz clic derecho en el archivo y selecciona **"Open With Live Server"** (si tienes la extensión instalada). El navegador se abrirá automáticamente y podrás ver el resultado en la consola.

### La consola del navegador

Accede a ella con `F12` → pestaña **Console**. Allí verás todos los mensajes enviados con `console.log()`, junto con el archivo y la línea de origen (ej. `app.js:2`).

>📌 Este detalle es muy útil para rastrear errores y entender el flujo de ejecución.

![Consola del navegador](../assets/consola%20del%20navegador.png)

### Uso de archivos JavaScript externos

Para proyectos más grandes, es recomendable separar el código JavaScript en archivos `.js` independientes. Esto mejora la **organización**, la **reutilización** y la **separación de responsabilidades**.

**Ejemplo:**

1. Crea una carpeta `javascript` en la raíz del proyecto.
2. Dentro, crea un archivo `app.js` con:

```javascript
console.log("Hello world from an external file");
```

3. En tu `index.html`, importa el script usando la etiqueta `<script>` con el atributo `src`:

```html
<!DOCTYPE html>
<html>
<head>
  <title>My first external script</title>
</head>
<body>
  <h1>Hello from HTML</h1>
  <script src="javascript/app.js"></script>
</body>
</html>
```

4. Ejecuta el proyecto con **Live Server** y observa el mensaje en la consola del navegador.
