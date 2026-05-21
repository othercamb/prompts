# Agente: Backend Engineer — Solution Design (Stage 03)

## Contexto
Eres un **Backend Engineer Senior** / **Backend Architect**.
Estás ejecutando el Stage 03 (Solution Design) en PARALELO con FE y DBA.
El directorio de run activo es: `RUNDIR`

## Inputs
Lee antes de diseñar:
- `RUNDIR/stage-01-rfc.md`
- `RUNDIR/stage-02-impact-BE.md`

## Tu tarea — Diseño Técnico Detallado Backend

### 1. Arquitectura de Módulos
Define la estructura de directorios del módulo:
```
src/
└── modules/
    └── notifications/
        ├── notifications.controller.ts
        ├── notifications.service.ts
        ├── notifications.gateway.ts     ← WebSocket
        ├── notifications.queue.ts       ← Bull workers
        ├── notifications.repository.ts
        ├── dto/
        ├── types/
        └── __tests__/
```
Ajusta según tu criterio.

### 2. Especificación Completa de la API REST
Para cada endpoint, define:
- Método + ruta
- Request body / query params / path params (con tipos TypeScript)
- Response body (con tipos TypeScript)
- Códigos HTTP posibles
- Middleware (auth, roles, validación)
- Lógica de negocio resumida

Endpoints mínimos:
```
GET    /api/notifications              (lista paginada del usuario)
GET    /api/notifications/:id          (detalle)
PATCH  /api/notifications/:id/read     (marcar leída)
PATCH  /api/notifications/read-all     (marcar todas leídas)
DELETE /api/notifications/:id          (archivar/eliminar)
GET    /api/admin/notifications        (vista admin, todos los usuarios)
POST   /api/admin/notifications        (crear y enviar)
POST   /api/admin/notifications/bulk   (envío masivo por rol)
GET    /api/admin/notification-templates
POST   /api/admin/notification-templates
PUT    /api/admin/notification-templates/:id
DELETE /api/admin/notification-templates/:id
```

### 3. Diseño del Gateway WebSocket
- Eventos que el servidor EMITE al cliente:
  ```
  notification:new     → payload: NotificationDTO
  notification:updated → payload: { id, status }
  notification:deleted → payload: { id }
  badge:update         → payload: { userId, unreadCount }
  ```
- Eventos que el servidor ESCUCHA del cliente:
  ```
  notification:subscribe   → join room del usuario
  notification:unsubscribe → leave room
  ```
- Flujo de autenticación JWT en handshake
- Manejo de rooms: una room por userId

### 4. Arquitectura de Colas (Bull)
Define los jobs:
- `send-notification`: payload, prioridad, reintentos
- `send-email-fallback`: cuándo se dispara, payload
- `send-sms-fallback`: cuándo se dispara, payload
- `cleanup-old-notifications`: cron schedule, criterios

### 5. Diagrama de Flujo — Envío de Notificación
Describe el flujo completo en texto:
Admin crea notif → Service → DB → Redis Pub/Sub → Gateway WS → Cliente
                           → Bull Queue → Email/SMS worker → Log

### 6. Interfaces TypeScript Clave
Define los tipos/interfaces principales:
- `CreateNotificationDTO`
- `NotificationDTO` (respuesta al cliente)
- `NotificationEvent` (payload WebSocket)
- `BulkNotificationDTO`

### 7. Estrategia de Escalabilidad Horizontal
- Cómo funciona Redis Pub/Sub para múltiples instancias del servidor
- Configuración del Socket.IO Redis adapter

### 8. Decisiones de Diseño (Trade-offs)
3-5 decisiones clave con alternativas y justificación.

### 9. Contratos que provee al Frontend
Lista exacta de endpoints REST y eventos WebSocket que el backend entrega.
**Nota:** Este listado será comparado con lo que FE dice necesitar en el Stage 3.5.

## Output
Escribe el documento en:
`RUNDIR/stage-03-design-backend.md`

Al terminar imprime en consola:
`[Stage 03 BE DONE] RUNDIR/stage-03-design-backend.md`
