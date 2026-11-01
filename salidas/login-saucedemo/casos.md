# Casos de prueba — Login de Swag Labs

> Generado con la skill `qa-casos-prueba` a partir de [analisis.md](analisis.md).
> Diseño, no ejecución: ningún caso está marcado como Pass o Fail.

## Resumen

Total: 12 casos · Alta: 4 · Media: 5 · Baja: 3 · Bloqueados: 4 · Automatizables: 8

**Pendiente de decisión de la QA:** hay 4 casos bloqueados por preguntas sin responder (#1, #3 y
#4). Los otros 8 se pueden ejecutar ya.

## Casos

### CP-01 — La pantalla de login muestra usuario, contraseña y botón Login
- **Traza a:** RN-01
- **Tipo:** Positivo
- **Prioridad:** Media
- **Automatizable:** Sí — es estable y se verifica sin criterio humano.
- **Precondiciones:** Sesión cerrada.
- **Datos:** —
- **Pasos:**
  1. Abrir https://www.saucedemo.com.
- **Resultado esperado:** Se ven el campo de usuario, el campo de contraseña y el botón "Login".

### CP-02 — Un usuario válido ingresa y llega al catálogo
- **Traza a:** RN-02 · Riesgo "Un usuario válido no puede entrar"
- **Tipo:** Positivo
- **Prioridad:** Alta
- **Automatizable:** Sí — es el flujo principal y se repite en cada regresión.
- **Precondiciones:** Sesión cerrada.
- **Datos:** usuario `standard_user` y la contraseña publicada en la pantalla de login.
- **Pasos:**
  1. Abrir la pantalla de login.
  2. Ingresar el usuario y la contraseña.
  3. Presionar "Login".
- **Resultado esperado:** El usuario llega al catálogo de productos.

### CP-03 — Los demás usuarios no bloqueados también ingresan
- **Traza a:** RN-02 · Riesgo "Un usuario válido no puede entrar"
- **Tipo:** Positivo
- **Prioridad:** Media
- **Automatizable:** Sí — es el mismo flujo de CP-02 con otros datos.
- **Precondiciones:** Sesión cerrada.
- **Datos:** usuarios `problem_user`, `performance_glitch_user`, `error_user` y `visual_user`,
  con la contraseña publicada.
- **Pasos:**
  1. Repetir los pasos de CP-02 con cada usuario.
- **Resultado esperado:** Cada usuario llega al catálogo de productos.

### CP-04 — Sin usuario, el error indica que falta el usuario
- **Traza a:** RN-03
- **Tipo:** Negativo
- **Prioridad:** Media
- **Automatizable:** Sí — validación estable.
- **Precondiciones:** Sesión cerrada.
- **Datos:** usuario vacío y la contraseña publicada.
- **Pasos:**
  1. Dejar el usuario vacío.
  2. Ingresar la contraseña.
  3. Presionar "Login".
- **Resultado esperado:** No ingresa y se muestra un error que indica que falta el usuario.

### CP-05 — Sin contraseña, el error indica que falta la contraseña
- **Traza a:** RN-03
- **Tipo:** Negativo
- **Prioridad:** Media
- **Automatizable:** Sí — validación estable.
- **Precondiciones:** Sesión cerrada.
- **Datos:** usuario `standard_user` y contraseña vacía.
- **Pasos:**
  1. Ingresar el usuario.
  2. Dejar la contraseña vacía.
  3. Presionar "Login".
- **Resultado esperado:** No ingresa y se muestra un error que indica que falta la contraseña.

### CP-06 — Con los dos campos vacíos se informa el error correcto
- **Traza a:** RN-03
- **Tipo:** Borde
- **Prioridad:** Baja
- **Automatizable:** Pendiente — se decide cuando se desbloquee.
- **Estado:** **Bloqueado — pregunta #3**
- **Precondiciones:** Sesión cerrada.
- **Datos:** usuario y contraseña vacíos.
- **Pasos:**
  1. Presionar "Login" sin completar nada.
- **Resultado esperado:** No ingresa. Qué campo se informa depende de la respuesta a la pregunta #3.

### CP-07 — Con contraseña incorrecta no ingresa
- **Traza a:** RN-04
- **Tipo:** Negativo
- **Prioridad:** Alta
- **Automatizable:** Sí — validación estable y crítica.
- **Precondiciones:** Sesión cerrada.
- **Datos:** usuario `standard_user` y contraseña `clave_incorrecta`.
- **Pasos:**
  1. Ingresar el usuario y la contraseña incorrecta.
  2. Presionar "Login".
- **Resultado esperado:** No ingresa y se muestra un mensaje de error.

### CP-08 — Con un usuario inexistente no ingresa
- **Traza a:** RN-04
- **Tipo:** Negativo
- **Prioridad:** Alta
- **Automatizable:** Sí — validación estable y crítica.
- **Precondiciones:** Sesión cerrada.
- **Datos:** usuario `usuario_inexistente` y la contraseña publicada.
- **Pasos:**
  1. Ingresar el usuario inexistente y la contraseña.
  2. Presionar "Login".
- **Resultado esperado:** No ingresa y se muestra un mensaje de error.

### CP-09 — El usuario escrito con otras mayúsculas
- **Traza a:** RN-04
- **Tipo:** Borde
- **Prioridad:** Baja
- **Automatizable:** Pendiente — se decide cuando se desbloquee.
- **Estado:** **Bloqueado — pregunta #4**
- **Precondiciones:** Sesión cerrada.
- **Datos:** usuario `Standard_User` y la contraseña publicada.
- **Pasos:**
  1. Ingresar el usuario con mayúsculas y la contraseña.
  2. Presionar "Login".
- **Resultado esperado:** Depende de la respuesta a la pregunta #4.

### CP-10 — El usuario con espacios al final
- **Traza a:** RN-04
- **Tipo:** Borde
- **Prioridad:** Baja
- **Automatizable:** Pendiente — se decide cuando se desbloquee.
- **Estado:** **Bloqueado — pregunta #4**
- **Precondiciones:** Sesión cerrada.
- **Datos:** usuario `standard_user ` (con un espacio al final) y la contraseña publicada.
- **Pasos:**
  1. Ingresar el usuario con el espacio y la contraseña.
  2. Presionar "Login".
- **Resultado esperado:** Depende de la respuesta a la pregunta #4.

### CP-11 — Un usuario bloqueado no ingresa y se le avisa que está bloqueado
- **Traza a:** RN-05 · Riesgo "Un usuario bloqueado logra entrar"
- **Tipo:** Negativo
- **Prioridad:** Alta
- **Automatizable:** Sí — riesgo alto y verificación estable.
- **Precondiciones:** Sesión cerrada.
- **Datos:** usuario `locked_out_user` y la contraseña publicada.
- **Pasos:**
  1. Ingresar el usuario bloqueado y la contraseña.
  2. Presionar "Login".
- **Resultado esperado:** No ingresa y se muestra un mensaje que indica que el usuario está
  bloqueado.

### CP-12 — El login responde en el tiempo acordado
- **Traza a:** RN-06 · Riesgo "El login tarda demasiado"
- **Tipo:** Borde
- **Prioridad:** Media
- **Automatizable:** Pendiente — se decide cuando se desbloquee.
- **Estado:** **Bloqueado — pregunta #1**
- **Precondiciones:** Sesión cerrada.
- **Datos:** usuario `performance_glitch_user` y la contraseña publicada.
- **Pasos:**
  1. Ingresar el usuario y la contraseña.
  2. Medir el tiempo desde que se presiona "Login" hasta que aparece el catálogo.
- **Resultado esperado:** El tiempo medido no supera el máximo que defina la pregunta #1.

## Matriz de cobertura

| Regla / Riesgo | Casos | Estado |
|---|---|---|
| RN-01 | CP-01 | Cubierta |
| RN-02 | CP-02, CP-03 | Cubierta |
| RN-03 | CP-04, CP-05, CP-06 | Cubierta (CP-06 bloqueado) |
| RN-04 | CP-07, CP-08, CP-09, CP-10 | Cubierta (CP-09 y CP-10 bloqueados) |
| RN-05 | CP-11 | Cubierta |
| RN-06 | CP-12 | Bloqueada — pregunta #1 |
| Riesgo: un usuario válido no puede entrar | CP-02, CP-03 | Cubierto |
| Riesgo: un usuario bloqueado logra entrar | CP-11 | Cubierto |
