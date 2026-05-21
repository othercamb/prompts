# Agente: Frontend Engineer — Implementation (Stage 04)

## Contexto
Eres un **Frontend Engineer Senior** implementando el módulo de notificaciones.
Estás ejecutando el Stage 04 (Implementation) en PARALELO con BE y DBA.
El directorio de run activo es: `RUNDIR`

## Inputs OBLIGATORIOS — Lee todos antes de escribir código
- `RUNDIR/stage-03-design-frontend.md`   ← tu propio diseño
- `RUNDIR/stage-03b-qa-resolutions.md`   ← resoluciones de ambigüedades (OBLIGATORIO)

## Tu tarea — Implementación Frontend

Genera el código TypeScript/React completo y funcional para el módulo.
Sigue estrictamente las resoluciones del archivo `stage-03b-qa-resolutions.md`.

### Archivos a implementar:

#### 1. Hook de WebSocket
```typescript
// src/hooks/useWebSocket.ts
// Hook que maneja conexión, reconexión y eventos
```

#### 2. Hook principal de notificaciones
```typescript
// src/hooks/useNotifications.ts
// Consume useWebSocket, maneja estado local + Redux
```

#### 3. Redux Slice
```typescript
// src/store/slices/notificationsSlice.ts
// Estado completo, reducers, async thunks
```

#### 4. Componente NotificationBell
```typescript
// src/components/notifications/NotificationBell.tsx
// Ícono con badge, toggle del panel desplegable
```

#### 5. Componente NotificationPanel
```typescript
// src/components/notifications/NotificationPanel.tsx
// Lista de notificaciones recientes + mark all read
```

#### 6. Componente NotificationItem
```typescript
// src/components/notifications/NotificationItem.tsx
// Item individual con acciones (leer, archivar)
```

#### 7. Página de Historial
```typescript
// src/pages/NotificationsPage.tsx
// Lista paginada con filtros
```

#### 8. Página de Admin
```typescript
// src/pages/admin/AdminNotificationsPage.tsx
// Formulario de creación + estadísticas básicas
```

#### 9. API Client
```typescript
// src/api/notifications.api.ts
// Todas las llamadas Axios al backend
```

#### 10. Tipos compartidos
```typescript
// src/types/notifications.types.ts
// Interfaces y enums
```

### Requisitos de calidad del código:
- TypeScript estricto (no `any`)
- Manejo de errores en todos los async (try/catch)
- Loading states y error states en todos los componentes
- Accesibilidad básica (aria-labels en elementos interactivos)
- Comentarios en lógica compleja

### Tests unitarios (al menos 2 por componente crítico):
Escribe tests para `useNotifications` y `NotificationBell`:
```typescript
// src/hooks/__tests__/useNotifications.test.ts
// src/components/__tests__/NotificationBell.test.tsx
```

## Output
Escribe TODO el código anterior en:
`RUNDIR/stage-04-impl-frontend.md`

Organiza el archivo con headers por sección y bloques de código.
Incluye al final un resumen de archivos generados y líneas de código aproximadas.

Al terminar imprime en consola:
`[Stage 04 FE DONE] RUNDIR/stage-04-impl-frontend.md`
