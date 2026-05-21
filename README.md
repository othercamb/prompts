# 🤖 Claude Code Multi-Agent ITIL Benchmark

Demo de paralelismo multi-agente usando **Claude Code** como orquestador.

## Escenario
**RFC-2026-001 — Módulo de Notificaciones Push en Tiempo Real**
Stack ficticio: React + Node.js + PostgreSQL + Redis

## Arquitectura del Benchmark

```
Orchestrator (Claude Code principal)
│
├── Stage 01 — RFC Capture              [SECUENCIAL] BusinessAnalyst
│
├── Stage 02 — Impact Assessment        [PARALELO x6]
│   ├── BusinessAnalyst
│   ├── Frontend Engineer
│   ├── Backend Engineer
│   ├── DBA
│   ├── QA Tester
│   └── Documentor
│
├── Stage 03 — Solution Design          [PARALELO x3]
│   ├── Frontend Engineer
│   ├── Backend Engineer
│   └── DBA
│
├── Stage 3.5 — Technical Q&A           [SECUENCIAL] Orquestador
│
├── Stage 04 — Implementation           [PARALELO x3]
│   ├── Frontend Engineer
│   ├── Backend Engineer
│   └── DBA
│
├── Stage 05 — Quality Assurance        [SECUENCIAL] Tester
├── Stage 06 — Documentation            [SECUENCIAL] Documentor
├── Stage 07 — Deployment Plan          [SECUENCIAL] BusinessAnalyst
│
└── Stage 08 — Métricas Finales         [Orquestador]
```

## Tiempo estimado total
- Secuencial hipotético: ~30-40 minutos
- Con paralelismo: ~20-25 minutos
- **Ahorro estimado: 35-45%**

## Pre-requisitos

```bash
# Claude Code instalado
npm install -g @anthropic-ai/claude-code   # o la versión disponible

# API key configurada
export ANTHROPIC_API_KEY="sk-ant-..."
```

## Cómo ejecutar

```bash
# 1. Clona el repo
git clone https://github.com/othercamb/prompts.git
cd prompts

# 2. Abre Claude Code en este directorio
claude

# 3. En el prompt de Claude Code, escribe:
> Ejecuta el Benchmark
```

Claude Code leerá el `CLAUDE.md` y seguirá el `orchestrator.md` automáticamente.

## Estructura de Artefactos Generados

```
benchmark-claude/
└── runs/
    └── 2026-05-21_14-30-00/
        ├── metrics.json
        ├── stage-01-rfc.md
        ├── stage-02-impact-BA.md
        ├── stage-02-impact-FE.md
        ├── stage-02-impact-BE.md
        ├── stage-02-impact-DBA.md
        ├── stage-02-impact-Tester.md
        ├── stage-02-impact-Documentor.md
        ├── stage-03-design-frontend.md
        ├── stage-03-design-backend.md
        ├── stage-03-design-dba.md
        ├── stage-03a-qa-questions.md
        ├── stage-03b-qa-resolutions.md
        ├── stage-04-impl-frontend.md
        ├── stage-04-impl-backend.md
        ├── stage-04-impl-dba.md
        ├── stage-05-qa-report.md
        ├── stage-06-documentation.md
        └── stage-07-deployment-plan.md
```

## Archivos del Repo

| Archivo | Propósito |
|---------|-----------|
| `CLAUDE.md` | System prompt del orquestador — leído automáticamente por Claude Code |
| `orchestrator.md` | Procedimiento de 8 stages que sigue el orquestador |
| `prompts/01-business-analyst-rfc.md` | Prompt Stage 1 |
| `prompts/02-impact-*.md` | Prompts Stage 2 (6 agentes) |
| `prompts/03-design-*.md` | Prompts Stage 3 (3 agentes) |
| `prompts/04-impl-*.md` | Prompts Stage 4 (3 agentes) |
| `prompts/05-qa-tester.md` | Prompt Stage 5 |
| `prompts/06-documentation.md` | Prompt Stage 6 |
| `prompts/07-deployment-BA.md` | Prompt Stage 7 |

## Métricas que se miden

Al final del benchmark, el orquestador muestra:

| Stage | Agentes | Modo | Duración | Ahorro |
|-------|---------|------|----------|--------|
| 01 RFC | 1 | Secuencial | Xm Ys | — |
| 02 Impact | 6 | **Paralelo** | Xm Ys | ~5x |
| 03 Design | 3 | **Paralelo** | Xm Ys | ~3x |
| 3.5 Q&A | 1 | Secuencial | Xm Ys | — |
| 04 Impl | 3 | **Paralelo** | Xm Ys | ~3x |
| 05 QA | 1 | Secuencial | Xm Ys | — |
| 06 Docs | 1 | Secuencial | Xm Ys | — |
| 07 Deploy | 1 | Secuencial | Xm Ys | — |
| **TOTAL** | **17** | | **~20m** | **~40%** |
