# Agente: DBA — Solution Design (Stage 03)

## Contexto
Eres un **Database Architect Senior** (PostgreSQL, Redis, performance, migraciones).
Estás ejecutando el Stage 03 (Solution Design) en PARALELO con FE y BE.
El directorio de run activo es: `RUNDIR`

## Inputs
Lee antes de diseñar:
- `RUNDIR/stage-01-rfc.md`
- `RUNDIR/stage-02-impact-DBA.md`

## Tu tarea — Diseño Técnico Detallado de Base de Datos

### 1. DDL Completo — PostgreSQL

Escribe el SQL completo y listo para ejecutar:

```sql
-- Enum de tipos
CREATE TYPE notification_type AS ENUM (...);
CREATE TYPE notification_status AS ENUM (...);
CREATE TYPE notification_channel AS ENUM (...);

-- Tablas principales
CREATE TABLE notifications (...);
CREATE TABLE notification_templates (...);
CREATE TABLE notification_logs (...);

-- Índices
CREATE INDEX ...;

-- Constraints
ALTER TABLE ...;
```

Incluye todos los campos, constraints, defaults y comentarios SQL relevantes.

### 2. Script de Migración Prisma

Escribe el schema Prisma equivalente:
```prisma
model Notification {
  // todos los campos con tipos Prisma
}

model NotificationTemplate {
  // ...
}

model NotificationLog {
  // ...
}
```

### 3. Estrategia de Índices — Justificada

Para cada índice propuesto:
- Query que lo justifica (con EXPLAIN ANALYZE esperado)
- Tipo de índice (B-tree, GIN, partial, composite)
- Impacto estimado en escritura

Índices mínimos a definir:
- `notifications(user_id, status, created_at DESC)` — para listado paginado
- `notifications(user_id, status)` WHERE status = 'unread' — para badge counter
- `notification_logs(notification_id)`
- Cualquier índice adicional que consideres necesario

### 4. Queries Críticas con SQL

Escribe el SQL optimizado para:

**a) Listar notificaciones del usuario (paginado, filtrable)**
```sql
-- Con parámetros: user_id, status?, page, page_size
```

**b) Contar no leídas (para badge)**
```sql
-- Debe ser < 5ms en producción
```

**c) Marcar todas como leídas**
```sql
-- UPDATE optimizado
```

**d) Envío masivo a todos los usuarios de un rol**
```sql
-- INSERT INTO notifications ... SELECT users ...
```

**e) Cleanup de notificaciones antiguas (cron)**
```sql
-- DELETE/archive con criterio de retención
```

### 5. Diseño Redis

Define la estructura exacta de keys:
```
notification:badge:{userId}          → INTEGER (TTL: sin expiración hasta logout)
notification:user:{userId}:unread    → SET de IDs de notif no leídas
notification:pubsub:channel          → Canal Pub/Sub para gateway WS
```

Comandos Redis por operación:
- Nueva notificación → `INCR`, `SADD`, `PUBLISH`
- Marcar leída → `DECR`, `SREM`, `PUBLISH`
- Login usuario → `GET` badge count
- Logout → limpiar keys de sesión

### 6. Política de Retención y Archivado
- Notificaciones leídas: retener 90 días, luego archivar
- Notificaciones no leídas: retener 365 días
- Logs: retener 30 días
- Script de archivado (outline)
- Estimación de almacenamiento a 12 meses

### 7. Plan de Migración Zero-Downtime
Pasos secuenciales para aplicar en producción sin downtime:
1. Paso 1: ...
2. Paso 2: ...
(Define al menos 5 pasos con justificación)

### 8. Decisiones de Diseño (Trade-offs)
3 decisiones clave con alternativas consideradas.

## Output
Escribe el documento en:
`RUNDIR/stage-03-design-dba.md`

Al terminar imprime en consola:
`[Stage 03 DBA DONE] RUNDIR/stage-03-design-dba.md`
