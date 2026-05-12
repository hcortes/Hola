# DEVELOPMENT_EXPRESS_HANDLEBARS

## Stack base

El proyecto debe usar:

- Node.js.
- Express.
- express-handlebars.
- dotenv.
- nodemon para desarrollo.
- middlewares nativos de Express.

## Reglas de Express

El archivo `server.js` debe encargarse solo de iniciar el servidor.

El archivo `app.js` debe encargarse de:

- Crear la aplicación Express.
- Configurar middlewares globales.
- Configurar Handlebars.
- Configurar archivos estáticos.
- Registrar rutas.
- Registrar middlewares de error.

## Motor de vistas

Se debe configurar Handlebars como motor de plantillas.

Configuración esperada:

- Carpeta de vistas: `src/views`.
- Layout principal: `main.handlebars`.
- Partials: `src/views/partials`.
- Vistas separadas por dominio:
  - `auth/login.handlebars`.
  - `pages/home.handlebars`.
  - `pages/dashboard.handlebars`.

## Rutas esperadas

Rutas públicas:

- GET `/`
- GET `/login`
- POST `/login`

Rutas protegidas:

- GET `/dashboard`
- POST `/logout` o GET `/logout` en modo educativo simple.

## Reglas para controllers

Los controllers deben:

- Recibir `req`, `res` y `next`.
- Validar datos mínimos.
- Delegar lógica al service correspondiente.
- Renderizar vistas o redirigir.
- No contener consultas SQL directamente.
- No contener comparación directa de passwords si existe un service.

## Reglas para vistas

Las vistas deben ser simples y didácticas.

La vista de login debe incluir:

- Formulario con método POST.
- Campo email.
- Campo password.
- Mensaje de error si las credenciales son inválidas.
- Mensaje visual claro para el alumno.

La vista dashboard debe mostrar:

- Nombre o email del usuario autenticado.
- Mensaje indicando que es una ruta protegida.
- Botón o enlace para cerrar sesión.

## Estilo didáctico

Cuando se genere código, incluir:

1. Estructura de carpetas.
2. Código completo por archivo.
3. Comandos de instalación.
4. Comandos de ejecución.
5. Explicación del flujo HTTP.
6. Prueba manual desde navegador.

## Buenas prácticas

- Usar `res.redirect()` después de un login correcto.
- No reenviar formularios al refrescar la página.
- No mostrar detalles internos de errores en la vista.
- Usar mensajes simples para credenciales inválidas.
- No indicar si falló el email o la contraseña por separado.
