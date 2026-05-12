# SKILL_BACKEND_EXPRESS.md

## PURPOSE
Este skill debe activarse cuando la tarea esté relacionada con backend Node.js, Express, APIs HTTP, cookies, sesiones, middlewares o persistencia del lado servidor.

## ACTIVATION RULE
Usar este documento solamente si en la tabla de activación aparece:

| SKILL                    | ACTIVATION |
|--------------------------|------------|
| SKILL_BACKEND_EXPRESS.md | true       |

Si ACTIVATION es false, este documento debe ignorarse completamente.

## RESPONSE STYLE
Cuando este skill esté activo, las respuestas deben priorizar:

- arquitectura backend clara;
- separación de responsabilidades;
- rutas Express;
- middlewares;
- manejo de errores con try/catch;
- seguridad básica;
- ejemplos ejecutables en Node.js.

## TECHNICAL RULES

1. Usar Express como framework principal.
2. Separar el código en capas cuando sea razonable:
   - routes
   - controllers
   - services
   - repositories
3. Evitar mezclar lógica de negocio dentro de las rutas.
4. Usar `async/await` para operaciones asíncronas.
5. Incluir manejo de errores básico.
6. Cuando se usen cookies:
   - explicar cuándo conviene `httpOnly: true`;
   - explicar cuándo debe usarse `httpOnly: false`;
   - incluir `sameSite`;
   - incluir `maxAge`.

## DEFAULT STACK

```txt
Node.js
Express
cookie-parser
JavaScript ES Modules
```

## EXAMPLE OUTPUT EXPECTED

Ante una consigna como:

> Crear un servidor que plante una cookie con datos del alumno.

La respuesta debe incluir código similar a:

```js
import express from "express";
import cookieParser from "cookie-parser";

const app = express();
app.use(express.json());
app.use(cookieParser());

app.get("/set-cookie", (req, res) => {
  const alumno = {
    apellido: "Cortes",
    matricula: "12345",
  };

  res.cookie("alumno", JSON.stringify(alumno), {
    maxAge: 60 * 60 * 1000,
    sameSite: "lax",
    httpOnly: false,
  });

  res.send("Cookie creada");
});

app.listen(3000, () => {
  console.log("Servidor activo en http://localhost:3000");
});
```

## DO NOT
- No priorizar HTML o diseño visual.
- No responder como si la tarea fuera frontend salvo que se solicite explícitamente.
- No usar Tailwind como foco principal.
