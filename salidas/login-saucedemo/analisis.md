# Análisis — Login de Swag Labs

> Generado con la skill `qa-analisis-requerimiento` a partir de
> [requerimiento.md](requerimiento.md). Revisado por la QA antes de pasar a los casos.

## Resumen

Pantalla de login con usuario y contraseña. Con credenciales válidas, el usuario llega al catálogo.
Si falta un campo, las credenciales son incorrectas o el usuario está bloqueado, el sistema muestra
un error y no deja entrar.

## Reglas de negocio

| ID | Regla | Fuente (frase del requerimiento) |
|---|---|---|
| RN-01 | La pantalla tiene campo de usuario, campo de contraseña y botón "Login". | "tiene un campo de usuario, un campo de contraseña y un botón 'Login'" |
| RN-02 | Con credenciales válidas, el usuario llega al catálogo de productos. | "lleva al usuario al catálogo de productos" |
| RN-03 | Si falta el usuario o la contraseña, se muestra un error que indica qué campo falta. | "muestra un mensaje de error indicando qué campo falta" |
| RN-04 | Con credenciales incorrectas se muestra un error y no se permite el ingreso. | "muestra un mensaje de error y no permite el ingreso" |
| RN-05 | Un usuario bloqueado no puede ingresar y ve un mensaje que le indica que está bloqueado. | "no puede ingresar y ve un mensaje que le indica que está bloqueado" |
| RN-06 | El login debe ser rápido. | "El login debe ser rápido" |

## Ambigüedades

1. **"Rápido" no tiene número (RN-06).** Sin un tiempo máximo, RN-06 no se puede verificar: no hay
   forma de decir si pasa o falla.
2. **Textos de error (RN-03, RN-04, RN-05).** No se define el texto de cada mensaje, así que no se
   puede comparar contra un resultado esperado exacto.
3. **Ambos campos vacíos (RN-03).** No dice qué campo se informa primero, o si se informan los dos.
4. **Mayúsculas y espacios.** No se define si el usuario distingue mayúsculas (`Standard_User`) ni
   si se recortan espacios al inicio o al final.
5. **Error de credenciales (RN-04).** No dice si el mensaje revela cuál de los dos datos está mal.
   Por seguridad, lo habitual es un mensaje genérico.
6. **Intentos fallidos.** No hay límite de intentos ni bloqueo automático. No queda claro si
   RN-05 aplica solo a usuarios ya bloqueados o también a quien falla varias veces.
7. **Contraseña oculta.** No se pide que el campo de contraseña oculte lo que se escribe.

## Riesgos

| Riesgo | Impacto | Probabilidad | Por qué |
|---|---|---|---|
| Un usuario válido no puede entrar | Alta | Baja | Bloquea la compra: sin login no hay ventas. |
| Un usuario bloqueado logra entrar | Alta | Baja | Es una falla de seguridad y de negocio. |
| El login tarda demasiado | Media | Media | El requerimiento lo pide pero no lo mide (ambigüedad 1). |
| El mensaje de credenciales incorrectas revela qué dato está mal | Media | Media | Facilita adivinar usuarios válidos (ambigüedad 5). |
| La contraseña se ve en pantalla al escribirla | Media | Baja | Expone la credencial a quien mira la pantalla (ambigüedad 7). |

## Preguntas para el equipo

| # | Pregunta | Para |
|---|---|---|
| 1 | ¿Cuál es el tiempo máximo aceptable para el login, en segundos? | Producto |
| 2 | ¿Cuál es el texto exacto de cada mensaje de error? | Producto / Diseño |
| 3 | Si los dos campos están vacíos, ¿qué mensaje se muestra? | Producto |
| 4 | ¿El usuario distingue mayúsculas? ¿Se recortan los espacios? | Desarrollo |
| 5 | ¿El error de credenciales incorrectas debe ser genérico? | Producto / Seguridad |
| 6 | ¿Hay un límite de intentos fallidos antes de bloquear al usuario? | Producto |
| 7 | ¿El campo de contraseña debe ocultar los caracteres? | Diseño |
| 8 | ¿Los usuarios de prueba son los que publica la pantalla de login? | Desarrollo |

## Alcance

**Dentro:** RN-01 a RN-05, la validación de campos vacíos y los usuarios de prueba que publica el
sitio en su pantalla de login.

**Fuera:**
- RN-06 (velocidad), hasta que se responda la pregunta 1: sin un número no hay resultado esperado.
- Cierre de sesión y recuperación de contraseña: el requerimiento no los menciona.
- Lo que pasa dentro del catálogo después del login: es otra historia de usuario.

## Supuestos

- Los usuarios y la contraseña válidos son los que muestra el propio sitio en la pantalla de
  login. Se confirma con la pregunta 8 y no se inventan otros.

## Observado en la app (2026-11-01)

Revisión rápida de la pantalla, sin iniciar sesión. Sirve de contexto, no reemplaza las respuestas
del equipo:

- Enviar el formulario vacío muestra `Epic sadface: Username is required`.
- Enviar solo el usuario muestra `Epic sadface: Password is required`.
- La pantalla publica la lista de usuarios aceptados y la contraseña común: es un sitio de
  práctica. En una tienda real, esto sería un hallazgo de seguridad.
