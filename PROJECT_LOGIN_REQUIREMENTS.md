# PROJECT_LOGIN_REQUIREMENTS

## Objetivo del proyecto

Se debe desarrollar un proyecto demo educativo de login usando:

- Node.js.
- Express.
- Handlebars como motor de plantillas.
- MySQL como base de datos.
- Sesiones del lado servidor.
- Buenas prácticas básicas de seguridad.

El objetivo principal es que el alumno comprenda el flujo completo:

1. Usuario ingresa email y password.
2. El servidor recibe los datos por POST.
3. Se busca el usuario en MySQL.
4. Se compara la contraseña ingresada contra un hash almacenado.
5. Si las credenciales son correctas, se crea una sesión.
6. El usuario accede a una ruta protegida.
7. El usuario puede cerrar sesión.

## Alcance educativo

El proyecto debe ser simple, claro y ejecutable en clase.

Debe priorizarse:

- Claridad del flujo.
- Separación de responsabilidades.
- Código legible.
- Buenas prácticas mínimas.
- Facilidad para explicar cada archivo.

No se debe generar una solución sobredimensionada.

## Estructura esperada

La estructura base sugerida es:

src/
  app.js
  server.js
  config/
    db.js
    env.js
  routes/
    auth.routes.js
    page.routes.js
  controllers/
    auth.controller.js
    page.controller.js
  services/
    auth.service.js
  repositories/
    user.repository.js
  middlewares/
    authRequired.js
    guestOnly.js
    errorHandler.js
  views/
    layouts/
      main.handlebars
    auth/
      login.handlebars
    pages/
      home.handlebars
      dashboard.handlebars
    partials/
      navbar.handlebars

## Reglas generales

- Las rutas no deben contener lógica de negocio.
- Los controllers deben manejar request y response.
- Los services deben contener la lógica de autenticación.
- Los repositories deben acceder a MySQL.
- La conexión a la base debe estar centralizada.
- Las vistas Handlebars no deben contener lógica compleja.
- El proyecto debe incluir comandos de instalación y ejecución.
- El proyecto debe incluir un script SQL inicial.
- El proyecto debe incluir un usuario de prueba.

## Variables por defecto

Si no se especifica otra cosa, usar:

- Puerto: 3000.
- Base de datos: login_demo.
- Tabla principal: users.
- Motor de vistas: express-handlebars.
- Gestor de paquetes: npm.
- Estilo de módulos: CommonJS o ES Modules, pero mantener consistencia en todo el proyecto.

## Resultado esperado

Al finalizar, el proyecto debe permitir:

- Abrir `/`.
- Ir a `/login`.
- Iniciar sesión con un usuario existente.
- Acceder a `/dashboard` solo si hay sesión activa.
- Cerrar sesión desde `/logout`.
- Bloquear acceso no autenticado a rutas protegidas.
