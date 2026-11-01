---
name: qa-analisis-requerimiento
description: Analiza un requerimiento o historia de usuario antes de probar. Devuelve reglas de negocio, ambigüedades, riesgos y preguntas para el equipo. No genera casos de prueba ni inventa reglas.
---

# Análisis de requerimiento

## 1. Cuándo se usa

Antes de escribir casos de prueba, cuando llega un requerimiento nuevo: una historia de usuario,
una descripción funcional, un mensaje del equipo o una captura de pantalla.

Si lo que se pide es directamente generar casos, primero se hace este análisis: los casos se
apoyan en él.

## 2. Entrada

- **Obligatoria:** el texto del requerimiento (o la captura).
- **Opcional:** criterios de aceptación, URL de la app, contexto del negocio.

Si falta el requerimiento, pídelo y detente. No analices sobre lo que "probablemente" dice.

## 3. Pasos

1. **Resume** en dos o tres líneas qué entiendes que hay que construir. Si no puedes resumirlo,
   el requerimiento no está listo: dilo.
2. **Reglas de negocio:** lista las reglas que el texto dice de forma explícita, numeradas
   (`RN-01`, `RN-02`…). Cada una cita la frase de donde sale.
3. **Ambigüedades:** lo que el texto no define y cambia el resultado de una prueba. Por ejemplo:
   límites (¿cuántos caracteres?), mensajes de error, qué pasa con datos vacíos, permisos.
4. **Riesgos:** qué podría fallar y a quién le dolería. Cada riesgo lleva impacto y
   probabilidad (Alta / Media / Baja) y una línea de por qué.
5. **Preguntas para el equipo:** una por ambigüedad, redactada para que se pueda responder en
   una línea. Indica a quién va (producto, desarrollo, diseño).
6. **Alcance:** qué entra en las pruebas y qué queda afuera, con el motivo.

## 4. Límites

- **No inventes reglas.** Si algo no está en el texto, va a ambigüedades o a preguntas, nunca a
  reglas de negocio.
- Si necesitas asumir algo para avanzar, márcalo como **Supuesto** y agrégalo a las preguntas.
- No generes casos de prueba: eso lo hace `qa-casos-prueba`, a partir de este análisis.
- No des el requerimiento por aprobado: el análisis señala, no decide.

## 5. Cuándo pide decisión humana

- Cuando una ambigüedad bloquea el alcance: pregunta antes de seguir.
- Cuando el requerimiento contradice otro conocido: muestra las dos fuentes y pregunta cuál
  manda.
- Al terminar: la QA revisa el análisis antes de pasar a los casos.

## 6. Salida y criterio de terminado

Guarda el resultado en `salidas/<nombre-del-requerimiento>/analisis.md` con esta estructura:

```markdown
# Análisis — <nombre del requerimiento>

## Resumen
## Reglas de negocio
| ID | Regla | Fuente (frase del requerimiento) |
## Ambigüedades
## Riesgos
| Riesgo | Impacto | Probabilidad | Por qué |
## Preguntas para el equipo
| # | Pregunta | Para |
## Alcance
**Dentro:** …
**Fuera:** … (motivo)
## Supuestos
```

**Está terminado cuando** cada regla cita su fuente, cada ambigüedad tiene su pregunta y el
alcance dice qué queda afuera y por qué.
