# DEVELOPMENT_AUTH_SECURITY_EDU

## Objetivo

Este skill define las reglas de autenticación y seguridad básica para un login educativo con Express, Handlebars y MySQL.

## Autenticación

El login debe realizarse comparando:

- Password ingresado por el usuario.
- Hash almacenado en MySQL.

Debe usarse:

- bcrypt
- bcrypt.compare()

No se debe comparar texto plano contra texto plano.

## Hash de contraseñas

Las contraseñas nunca deben almacenarse en texto plano.

Para crear usuarios de prueba, se debe usar:

- bcrypt.hash(password, saltRounds)

Valor recomendado para demo:

saltRounds = 10

## Sesiones

Debe usarse sesión del lado servidor.

Dependencias sugeridas:

- express-session
- express-mysql-session

Para una demo estrictamente local puede explicarse MemoryStore, pero no debe recomendarse como buena práctica.

La sesión debe guardar solo datos mínimos:

req.session.user = {
  id: user.id,
  email: user.email,
  fullName: user.full_name,
  role: user.role
}

No guardar:

- password.
- password_hash.
- datos sensibles innecesarios.

## Cookies de sesión

La cookie de sesión debe configurarse con criterios seguros.

Configuración base recomendada para desarrollo:

cookie: {
  httpOnly: true,
  secure: false,
  sameSite: "lax",
  maxAge: 1000 * 60 * 60
}

Notas:

- `httpOnly: true` evita acceso desde JavaScript del navegador.
- `secure: false` se acepta en localhost.
- En producción con HTTPS debe usarse `secure: true`.
- `sameSite: "lax"` reduce riesgos básicos de envío cross-site.

## Middleware de protección

Debe existir un middleware:

authRequired.js

Responsabilidad:

- Verificar si existe `req.session.user`.
- Si existe, permitir acceso.
- Si no existe, redirigir a `/login`.

Debe existir opcionalmente:

guestOnly.js

Responsabilidad:

- Evitar que un usuario ya autenticado vuelva a `/login`.
- Redirigir a `/dashboard` si ya tiene sesión activa.

## Logout

El logout debe destruir la sesión.

Debe usarse:

req.session.destroy()

Luego debe redirigirse a `/login`.

## Validación de entrada

El login debe validar como mínimo:

- Email requerido.
- Email con formato válido.
- Password requerido.
- Password no vacío.

Puede usarse:

- express-validator.

Regla importante:

No se debe enviar una query a MySQL si los datos básicos del formulario son inválidos.

## Mensajes de error

Para credenciales inválidas, usar un mensaje genérico:

"Credenciales inválidas"

No usar:

"El email no existe"
"La contraseña es incorrecta"

Esto evita filtrar información sobre usuarios registrados.

## Seguridad básica de Express

Agregar:

- helmet
- express.urlencoded({ extended: true })
- express.json()
- dotenv

No exponer stack traces al usuario.

Los errores técnicos pueden imprimirse en consola durante desarrollo, pero no deben mostrarse completos en la vista.

## Enfoque educativo

Cuando se explique el proyecto, mostrar el flujo:

Formulario HTML
  ↓
POST /login
  ↓
Controller
  ↓
Service
  ↓
Repository
  ↓
MySQL
  ↓
bcrypt.compare()
  ↓
session
  ↓
redirect /dashboard

También se debe explicar la diferencia entre:

- Autenticación.
- Sesión.
- Cookie de sesión.
- Ruta pública.
- Ruta protegida.
