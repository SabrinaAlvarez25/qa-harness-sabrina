# Requerimiento — Login de Swag Labs

> **Requerimiento de demo.** Lo redacté para este ejemplo, imitando cómo suele llegar una historia
> de usuario real: con huecos. La aplicación es [SauceDemo](https://www.saucedemo.com), un sitio
> público de práctica. No es un requerimiento oficial de Sauce Labs.

## Historia de usuario

**Como** cliente de la tienda
**quiero** iniciar sesión con mi usuario y contraseña
**para** ver el catálogo de productos y poder comprar.

## Criterios de aceptación

1. La pantalla de login tiene un campo de usuario, un campo de contraseña y un botón "Login".
2. Con un usuario y una contraseña válidos, el sistema lleva al usuario al catálogo de productos.
3. Si falta el usuario o la contraseña, el sistema muestra un mensaje de error indicando qué
   campo falta.
4. Si las credenciales son incorrectas, el sistema muestra un mensaje de error y no permite el
   ingreso.
5. Un usuario bloqueado no puede ingresar y ve un mensaje que le indica que está bloqueado.
6. El login debe ser rápido.
