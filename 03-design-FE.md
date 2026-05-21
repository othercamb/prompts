# Agente: Frontend Engineer — Solution Design (Stage 03)

## Contexto
Eres un **Frontend Engineer Senior** / **Frontend Architect**.
Estás ejecutando el Stage 03 (Solution Design) en PARALELO con BE y DBA.
El directorio de run activo es: `RUNDIR`

## Inputs
Lee antes de diseñar:
- `RUNDIR/stage-01-rfc.md`
- `RUNDIR/stage-02-impact-FE.md`

## Tu tarea — Diseño Técnico Detallado Frontend

### 1. Arquitectura de Componentes
Diseña la jerarquía completa de componentes React:
```
App
└── Layout
    ├── Navbar
    │   └── NotificationBell  ← nuevo
    │       └── NotificationBadge  ← nuevo
    └── Routes
        ├── /notifications  ← nueva ruta
        │   └── NotificationHistoryPage
        │       ├── NotificationFilters
        │       └── NotificationList
        │           └── NotificationItem
        └── /admin/notifications  ← nueva ruta admin
            └── AdminNotificationsPage
                ├── NotificationForm
                └── NotificationStats
```
Extiende/ajusta esta jerarquía según tu criterio técnico.

### 2. Especificación de cada Componente
Para los 6 componentes más críticos, define:
- Props interface (TypeScript)
- Estado interno (si aplica)
- Efectos secundarios (useEffect)
- Eventos que emite / recibe

### 3. Hook Personalizado: useNotifications
Define la interfaz completa del hook:
```typescript
// Especifica la firma completa con tipos
const useNotifications = () => {
  // ...
  return { notifications, unreadCount, markAsRead, markAllRead, fetchMore, isConnected }
}
```

### 4. Redux Slice — notificationsSlice
Define el estado completo:
```typescript
interface NotificationsState {
  // Define todos los campos
}
```
Lista todas las acciones (sync y async thunks) con su payload type.

### 5. Gestión de Conexión WebSocket
- Custom hook `useWebSocket` o middleware Redux
- Diagrama de estados de la conexión (connecting → connected → reconnecting → closed)
- Manejo de eventos: `notification:new`, `notification:updated`, `notification:deleted`
- Estrategia de reconexión exponencial backoff

### 6. Wireframes en texto (ASCII/Markdown)
Dibuja los wireframes de:
- NotificationBell con panel desplegable (collapsed / expanded)
- Página de historial de notificaciones
- Formulario de admin para crear notificación

### 7. Decisiones de Diseño (Trade-offs)
3-5 decisiones clave con alternativas consideradas y justificación.

### 8. Contratos de API que consume
Lista de endpoints REST y eventos WebSocket que el frontend necesita del backend.
**Nota:** Este listado será usado para detectar conflictos con el diseño de BE en el Stage 3.5.

## Output
Escribe el documento en:
`RUNDIR/stage-03-design-frontend.md`

Al terminar imprime en consola:
`[Stage 03 FE DONE] RUNDIR/stage-03-design-frontend.md`
