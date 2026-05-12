# DEVELOPMENT_MYSQL_ACCESS

## Objetivo

Este skill define cómo debe integrarse MySQL en el proyecto demo.

## Dependencia recomendada

Usar:

- mysql2
- mysql2/promise

El acceso a MySQL debe realizarse usando promesas y async/await.

## Configuración

La configuración de conexión debe leerse desde variables de entorno.

Archivo `.env` esperado:

DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=
DB_NAME=login_demo

SESSION_SECRET=change_this_secret
PORT=3000

## Pool de conexiones

La conexión debe centralizarse en:

src/config/db.js

Debe usarse un pool de conexiones, no una conexión aislada por request.

Ejemplo conceptual:

- Crear pool.
- Exportar pool.
- Reutilizarlo desde repositories.

## Reglas de acceso a datos

- No escribir SQL directamente dentro de routes.
- No escribir SQL directamente dentro de controllers.
- Las consultas deben estar en repositories.
- Usar prepared statements.
- Nunca concatenar datos del usuario dentro de una query SQL.
- Usar placeholders `?`.

Correcto:

SELECT * FROM users WHERE email = ?

Incorrecto:

SELECT * FROM users WHERE email = '${email}'

## Tabla principal

La tabla `users` debe tener como mínimo:

- id
- full_name
- email
- password_hash
- role
- is_active
- created_at
- updated_at

Schema sugerido:

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  full_name VARCHAR(100) NOT NULL,
  email VARCHAR(150) NOT NULL UNIQUE,
  password_hash VARCHAR(255) NOT NULL,
  role VARCHAR(50) DEFAULT 'student',
  is_active BOOLEAN DEFAULT TRUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

## Usuario de prueba

El proyecto debe incluir un modo claro para crear un usuario de prueba.

Puede resolverse con:

- Script SQL.
- Script Node.js de seed.
- Instrucciones para insertar usuario con password hasheado.

No debe insertarse una contraseña en texto plano dentro de la tabla.

## Repository esperado

El archivo:

src/repositories/user.repository.js

Debe incluir funciones como:

- findUserByEmail(email)
- findUserById(id)

Estas funciones deben devolver datos mínimos necesarios.

## Datos sensibles

El campo `password_hash` solo debe usarse dentro del proceso de autenticación.

No debe enviarse a vistas.

No debe guardarse completo en la sesión.

No debe imprimirse por consola.
