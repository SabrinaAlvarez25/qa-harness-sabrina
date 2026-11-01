---
name: qa-casos-prueba
description: Genera casos de prueba trazables a partir de un análisis de requerimiento. Cubre caminos positivos, negativos y de borde, prioriza por riesgo y marca candidatos a automatizar. No ejecuta pruebas ni inventa resultados esperados.
---

# Casos de prueba

## 1. Cuándo se usa

Después de `qa-analisis-requerimiento`, cuando el análisis ya fue revisado y hay que diseñar qué
se va a probar.

## 2. Entrada

- **Obligatoria:** el análisis en `salidas/<nombre-del-requerimiento>/analisis.md`.
- **Opcional:** datos de prueba disponibles (usuarios, productos, montos), respuestas del equipo a
  las preguntas del análisis.

Si no existe el análisis, no lo saltes: corre primero `qa-analisis-requerimiento`. Los casos sin
análisis terminan probando lo que la IA supone, no lo que pide el requerimiento.

## 3. Pasos

1. **Por cada regla de negocio** (`RN-xx`), deriva casos con estas técnicas:
   - **Positivo:** la regla se cumple con datos válidos.
   - **Negativo:** datos inválidos o acciones no permitidas.
   - **Borde:** valores en el límite (mínimo, máximo, justo afuera), con análisis de valores
     límite y partición de equivalencia.
2. **Por cada riesgo de impacto Alto**, agrega al menos un caso que lo cubra, aunque ya exista
   uno por regla.
3. **Prioriza** cada caso: Alta (bloquea el flujo principal o un riesgo alto), Media, Baja.
4. **Marca si es automatizable** y por qué: se repite seguido, es estable y el resultado se
   puede verificar sin criterio humano.
5. **Arma la matriz de cobertura:** cada regla y cada riesgo alto con sus casos. Lo que quede sin
   caso se marca como hueco.

## 4. Límites

- **El resultado esperado sale del análisis.** Si depende de una ambigüedad sin respuesta, el caso
  queda como **Bloqueado — pregunta #N**. No completes el resultado con lo que "seguramente" pasa.
- **No inventes datos de prueba.** Usa los que te dieron; si faltan, deja el hueco marcado
  (`<usuario válido>`) en lugar de un valor fabricado.
- No ejecutes casos ni marques ninguno como Pass o Fail: esta skill diseña, no ejecuta.
- No agregues casos que no se puedan trazar a una regla o un riesgo. Si crees que falta algo, va
  como pregunta, no como caso suelto.

## 5. Cuándo pide decisión humana

- Cuando hay más de un caso bloqueado: muestra la lista y pregunta si se sigue igual o se espera
  la respuesta del equipo.
- Al terminar: la QA revisa la prioridad y la marca de automatización, que son propuestas.

## 6. Salida y criterio de terminado

Guarda el resultado en `salidas/<nombre-del-requerimiento>/casos.md` con esta estructura:

```markdown
# Casos de prueba — <nombre del requerimiento>

## Resumen
Total: N casos · Alta: N · Media: N · Baja: N · Bloqueados: N · Automatizables: N

## Casos

### CP-01 — <título que dice qué se verifica>
- **Traza a:** RN-01
- **Tipo:** Positivo | Negativo | Borde
- **Prioridad:** Alta | Media | Baja
- **Automatizable:** Sí | No — <motivo>
- **Precondiciones:** …
- **Datos:** …
- **Pasos:**
  1. …
- **Resultado esperado:** …

## Matriz de cobertura
| Regla / Riesgo | Casos | Estado |
|---|---|---|
| RN-01 | CP-01, CP-02 | Cubierta |
| RN-03 | — | Hueco |
```

**Está terminado cuando** cada caso traza a una regla o un riesgo, la matriz no tiene reglas
olvidadas y cada caso bloqueado nombra la pregunta que lo bloquea.
