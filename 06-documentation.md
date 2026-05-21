# Agente: Technical Writer — Documentation (Stage 06)

## Contexto
Eres un **Technical Writer Senior** documentando el módulo de notificaciones.
Estás ejecutando el Stage 06 (Documentation) de forma SECUENCIAL.
El directorio de run activo es: `RUNDIR`

## Inputs — Lee todos antes de documentar
- `RUNDIR/stage-01-rfc.md`
- `RUNDIR/stage-03-design-backend.md`
- `RUNDIR/stage-03-design-frontend.md`
- `RUNDIR/stage-03-design-dba.md`
- `RUNDIR/stage-04-impl-backend.md`
- `RUNDIR/stage-05-qa-report.md`

## Tu tarea — Documentación Completa del Módulo

### Sección 1: API Reference (OpenAPI 3.0 — YAML)
Escribe la especificación OpenAPI completa:
```yaml
openapi: 3.0.3
info:
  title: Notifications Module API
  version: 1.0.0
paths:
  /api/notifications:
    get: ...
  # Todos los endpoints REST
components:
  schemas:
    Notification: ...
    NotificationTemplate: ...
  securitySchemes:
    bearerAuth: ...
```

### Sección 2: WebSocket Events Reference
Tabla completa de eventos:
| Evento | Dirección | Payload | Descripción | Cuándo ocurre |
|--------|-----------|---------|-------------|---------------|
| notification:new | Server → Client | `{id, title, body, type, createdAt}` | ... | ... |
| ... | | | | |

Incluye ejemplos de payload JSON para cada evento.

### Sección 3: Guía de Usuario Final
Redacta una guía amigable (no técnica) que explique:
- Cómo ver las notificaciones (ícono de campana)
- Qué significa el badge rojo con número
- Cómo marcar como leída / archivar
- Cómo acceder al historial completo
- Tipos de notificaciones que puede recibir

### Sección 4: Guía de Administrador
Para usuarios con rol de administrador:
- Cómo crear una notificación individual
- Cómo enviar notificación masiva por rol
- Cómo usar plantillas de notificación
- Cómo ver el historial y estado de entregas
- Cómo monitorear fallos de entrega

### Sección 5: Runbook Operacional — Troubleshooting
```
## Problema: Los usuarios no reciben notificaciones en tiempo real

Síntomas: Badge no actualiza, panel no muestra nuevas notificaciones
Diagnóstico:
  1. Verificar estado del servidor WebSocket: ...
  2. Verificar Redis Pub/Sub: ...
  3. Verificar logs del gateway: ...
Resolución:
  - Si Redis está caído: ...
  - Si el gateway WS está saturado: ...
  - Si es problema de CORS: ...

## Problema: Badge counter incorrecto
...

## Problema: Notificaciones duplicadas
...

## Problema: Email fallback no se envía
...
```

### Sección 6: ADR (Architecture Decision Records)
Escribe 3 ADRs para las decisiones más importantes:
```markdown
# ADR-001: Uso de Socket.IO sobre WebSocket nativo

## Estado: Aceptado
## Contexto: ...
## Decisión: ...
## Consecuencias: ...
## Alternativas consideradas: ...
```

### Sección 7: README del Módulo (para developers)
```markdown
# Notifications Module

## Descripción
## Arquitectura
## Setup local (variables de entorno necesarias)
## Ejecutar tests
## Guía de contribución
## Changelog
```

## Output
Escribe toda la documentación en:
`RUNDIR/stage-06-documentation.md`

Al terminar imprime en consola:
`[Stage 06 Docs DONE] RUNDIR/stage-06-documentation.md`
