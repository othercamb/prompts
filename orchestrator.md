# Procedimiento: Ejecuta el Benchmark (Claude Code Multi-Agent ITIL)

Cuando el usuario diga **"Ejecuta el Benchmark"** (o variantes como "run benchmark", "ejecuta el benchmark"), sigue>

---

## Paso 0: Inicialización

1. Crear directorio del run: `benchmark-claude/runs/{YYYY-MM-DD_HH-MM-SS}/`
2. Inicializar `metrics.json` con timestamp de inicio
3. En todos los prompts de subagentes, reemplazar `RUNDIR` con el nombre del directorio creado

## Paso 1 — RFC Capture (SECUENCIAL)
**Agente:** BusinessAnalyst
**Tiempo estimado:** 2-3 min

Lanzar 1 subagente foreground con el prompt de `prompts/01-business-analyst-rfc.md`.
Esperar resultado. Registrar tiempo inicio/fin en metrics.json.

## Paso 2 — Impact Assessment (PARALELO ⚡)
**Agentes:** BA + FE + BE + DBA + Tester + Documentor (6 en paralelo)
**Tiempo estimado:** 3-5 min (paralelo)

Lanzar 6 subagentes en BACKGROUND simultáneamente, cada uno con su sección del prompt `prompts/02-impact-ROLE.md`.
Esperar a que todos completen. Registrar tiempos individuales.

## Paso 3 — Solution Design (PARALELO ⚡)
**Agentes:** FE + BE + DBA (3 en paralelo)
**Tiempo estimado:** 4-6 min (paralelo)

Lanzar 3 subagentes en BACKGROUND. Esperar resultados.

## Paso 3.5 — Technical Q&A (SECUENCIAL — CLAVE)
**Orquestador:** Yo (Claude Code principal)

1. Leer los 3 diseños: `stage-03-design-frontend.md`, `stage-03-design-backend.md`, `stage-03-design-dba.md`
2. Identificar ambigüedades y conflictos técnicos entre los diseños
3. Generar 5-8 preguntas técnicas críticas con contexto
4. Escribir preguntas en `stage-03a-qa-questions.md`
5. Resolver cada pregunta (consultar a agentes específicos si es necesario, o resolver con arquitectura propia)
6. Escribir resoluciones en `stage-03b-qa-resolutions.md` — **este archivo es OBLIGATORIO para implementación**

## Paso 4 — Implementation (PARALELO ⚡)
**Agentes:** FE + BE + DBA (3 en paralelo)
**Tiempo estimado:** 6-10 min (paralelo)

Lanzar 3 subagentes en BACKGROUND, cada uno con su prompt de implementación que incluye el archivo de resoluciones >

## Paso 5 — Quality Assurance (SECUENCIAL)
**Agente:** Tester
**Tiempo estimado:** 3-4 min

Lanzar 1 subagente foreground.

## Paso 6 — Documentation (SECUENCIAL)
**Agente:** Documentor
**Tiempo estimado:** 3-4 min

Lanzar 1 subagente foreground.

## Paso 7 — Deployment Plan (SECUENCIAL)
**Agente:** BusinessAnalyst
**Tiempo estimado:** 2-3 min

Lanzar 1 subagente foreground.

## Paso 8 — Métricas Finales

Compilar y mostrar tabla de métricas:
- Duración de cada stage (wall clock)
- Duración de cada agente
- Tiempo ahorrado por paralelismo
- Tamaño de cada artefacto
- Número de preguntas Q&A generadas y resueltas
- Total del proceso end-to-end
