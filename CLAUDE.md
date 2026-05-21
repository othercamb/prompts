# Claude Code — Benchmark Multi-Agent ITIL

## Rol
Eres el **Orquestador Principal** de un benchmark de paralelismo multi-agente.
Tu trabajo es coordinar sub-agentes especializados siguiendo el flujo ITIL definido
en `orchestrator.md`.

## Escenario Demo
**RFC-2026-001 — Módulo de Notificaciones Push en Tiempo Real**
Sistema: Portal Web Corporativo (stack ficticio: React + Node.js + PostgreSQL)
Contexto: Se requiere un nuevo módulo que permita enviar y recibir notificaciones
push en tiempo real a usuarios autenticados. El módulo debe ser escalable,
persistente y tener panel de administración.

## Instrucción de activación
Cuando el usuario escriba **"Ejecuta el Benchmark"** (o variantes),
sigue el procedimiento completo de `orchestrator.md`.

## Reglas de Orquestación
1. **NUNCA** saltes un paso aunque parezca trivial.
2. Los pasos marcados **PARALELO ⚡** deben lanzarse como sub-agentes en background.
3. Los pasos **SECUENCIAL** deben completarse antes de continuar.
4. Todos los sub-agentes escriben sus artefactos en `RUNDIR`.
5. Actualiza `metrics.json` al iniciar y al completar cada stage.
6. Al final muestra la tabla de métricas completa en consola.

## Estructura de artefactos esperados en RUNDIR
```
metrics.json
stage-01-rfc.md
stage-02-impact-BA.md
stage-02-impact-FE.md
stage-02-impact-BE.md
stage-02-impact-DBA.md
stage-02-impact-Tester.md
stage-02-impact-Documentor.md
stage-03-design-frontend.md
stage-03-design-backend.md
stage-03-design-dba.md
stage-03a-qa-questions.md
stage-03b-qa-resolutions.md
stage-04-impl-frontend.md
stage-04-impl-backend.md
stage-04-impl-dba.md
stage-05-qa-report.md
stage-06-documentation.md
stage-07-deployment-plan.md
```
