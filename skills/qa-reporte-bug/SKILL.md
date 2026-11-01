---
name: qa-reporte-bug
description: Convierte lo que la QA observó al probar en un reporte de bug claro y reproducible, trazado al caso y a la regla que falla. Separa severidad de prioridad. No inventa evidencia, no adivina la causa y no decide si algo es bug cuando el requerimiento es ambiguo.
---

# Reporte de bug

## 1. Cuándo se usa

Cuando, al ejecutar un caso o explorando la app, el comportamiento no coincide con lo esperado y
hay que reportarlo al equipo.

## 2. Entrada

- **Obligatoria:** qué hiciste, qué esperabas y qué pasó.
- **Opcional pero muy recomendada:** el caso que fallaba (`CP-xx`), ambiente, navegador, datos
  usados, captura, video o log.

Si no queda claro qué se esperaba, pregunta antes de redactar: sin resultado esperado no hay bug,
hay una observación.

## 3. Pasos

1. **¿Es un bug?** Busca de dónde sale lo esperado: un caso (`CP-xx`), una regla (`RN-xx`) o el
   requerimiento. Si no sale de ningún lado o el requerimiento es ambiguo, no es un bug todavía:
   repórtalo como **Observación** con la pregunta para el equipo.
2. **¿Ya está reportado?** Revisa los bugs en `salidas/*/bugs/`. Si es el mismo, avisa y no
   dupliques.
3. **Título** con la fórmula: *dónde* + *qué pasa* + *en qué condición*. Ejemplo: "Checkout: el
   total no suma el impuesto cuando el carrito tiene un solo producto".
4. **Pasos para reproducir:** los mínimos, numerados, con los datos concretos. Alguien que no
   estuvo ahí tiene que poder repetirlos.
5. **Esperado vs. obtenido:** lado a lado, con la fuente de lo esperado.
6. **Severidad y prioridad, por separado:**
   - **Severidad** (impacto técnico): Crítica, Alta, Media, Baja.
   - **Prioridad** (urgencia para el negocio): Alta, Media, Baja. Es una propuesta: la decide el
     equipo.
7. **Reproducibilidad:** cuántas veces lo intentaste y cuántas falló (por ejemplo, 3 de 3).

## 4. Límites

- **No inventes evidencia.** Si no hay captura o log, el campo dice "Sin evidencia adjunta". Nunca
  describas una captura que no viste.
- **No adivines la causa.** El reporte dice qué pasa, no por qué. Si tienes una hipótesis, va
  aparte y marcada como hipótesis.
- No cambies el resultado esperado para que coincida con lo que la app hace.
- No reportes en Jira ni en ninguna herramienta externa: el reporte queda en el repo y lo publica
  la QA.

## 5. Cuándo pide decisión humana

- Cuando no está claro si es bug o comportamiento esperado: muestra las dos lecturas y pregunta.
- Cuando la severidad es Crítica: confirma con la QA antes de guardar.
- Al terminar: la QA revisa el reporte antes de enviarlo al equipo.

## 6. Salida y criterio de terminado

Guarda cada bug en `salidas/<nombre-del-requerimiento>/bugs/BUG-NN.md` con esta estructura:

```markdown
# BUG-NN — <dónde: qué pasa en qué condición>

- **Tipo:** Bug | Observación
- **Caso / regla:** CP-xx · RN-xx
- **Severidad:** Crítica | Alta | Media | Baja
- **Prioridad propuesta:** Alta | Media | Baja
- **Ambiente:** <URL, navegador, versión>
- **Reproducibilidad:** N de N intentos

## Pasos para reproducir
1. …

## Resultado esperado
… (fuente: CP-xx / RN-xx)

## Resultado obtenido
…

## Evidencia
<captura, video, log o "Sin evidencia adjunta">

## Hipótesis (opcional)
…
```

**Está terminado cuando** otra persona puede reproducir el bug solo con el reporte, el resultado
esperado nombra su fuente y la evidencia es real o está marcada como faltante.
