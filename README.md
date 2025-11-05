# WebRTC-Server 🎥

Servidor WebSocket para señalización WebRTC con soporte para múltiples clientes.

## 📋 Requisitos

- Node.js 12+
- pnpm (recomendado) o npm

## 🚀 Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/seph-25/WebRTC-Server.git
cd WebRTC-Server
```

### 2. Instalar dependencias

```bash
pnpm install
# o con npm
npm install
```

### 3. Configurar variables de entorno

Copia el archivo `.env.example` a `.env`:

```bash
cp .env.example .env
```

Edita `.env` según tu configuración:

```env
# Puerto del servidor
PORT=8000

# Ambiente (development, production)
NODE_ENV=development

# CORS - Orígenes permitidos (separa múltiples con comas)
CORS_ORIGIN=http://localhost:3000,http://localhost:5173

# Intervalo de heartbeat en ms (por defecto 30000)
HEARTBEAT_INTERVAL=30000

# Nivel de logging
LOG_LEVEL=info
```

### 4. Iniciar el servidor

```bash
pnpm start
# o con npm
npm start
```

El servidor estará disponible en `http://localhost:8000`

## 📡 API

### Endpoints HTTP

#### GET `/status`

Obtiene el estado del servidor.

**Respuesta:**

```json
{
  "status": "running",
  "environment": "development",
  "connections": 5,
  "uptime": 1234.56
}
```

### WebSocket

Conéctate a `ws://localhost:8000`

#### Mensajes soportados

##### `assign-id` (servidor → cliente)

Asigna un ID único al cliente.

```json
{
  "type": "assign-id",
  "userId": "uuid-string"
}
```

##### `user-joined` (servidor → clientes)

Notifica cuando un nuevo usuario se conecta.

```json
{
  "type": "user-joined",
  "userId": "uuid-string"
}
```

##### `existing-users` (servidor → cliente)

Lista de usuarios existentes al conectarse.

```json
{
  "type": "existing-users",
  "userIds": ["uuid1", "uuid2", "uuid3"]
}
```

##### `user-left` (servidor → clientes)

Notifica cuando un usuario se desconecta.

```json
{
  "type": "user-left",
  "userId": "uuid-string"
}
```

## 🔒 Seguridad

- ✅ Todas las configuraciones sensibles están en `.env` (gitignored)
- ✅ CORS configurables según ambiente
- ✅ `.env` nunca se sube al repositorio
- ✅ Heartbeat automático para detectar conexiones inactivas
- ✅ Validación de mensajes JSON

## 📝 Variables de Entorno

| Variable             | Default               | Descripción                       |
| -------------------- | --------------------- | --------------------------------- |
| `PORT`               | 8000                  | Puerto del servidor               |
| `NODE_ENV`           | development           | Ambiente (development/production) |
| `CORS_ORIGIN`        | http://localhost:3000 | Orígenes CORS permitidos          |
| `HEARTBEAT_INTERVAL` | 30000                 | Intervalo heartbeat en ms         |
| `LOG_LEVEL`          | info                  | Nivel de logging                  |

## 🏗️ Estructura del Proyecto

```
├── server.js           # Punto de entrada principal
├── httpServer.js       # Configuración del servidor HTTP
├── signaling.js        # Lógica de señalización WebRTC
├── package.json        # Dependencias del proyecto
├── pnpm-lock.yaml      # Lock file de pnpm
├── .env.example        # Plantilla de variables de entorno
├── .gitignore          # Archivos ignorados por Git
└── README.md           # Este archivo
```

## 📚 Tecnologías

- **ws**: WebSocket server
- **uuid**: Generador de IDs únicos
- **dotenv**: Carga de variables de entorno

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Por favor:

1. Fork el repositorio
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📄 Licencia

ISC

## 🔗 Enlaces

- [Repositorio](https://github.com/seph-25/WebRTC-Server)
- [Issues](https://github.com/seph-25/WebRTC-Server/issues)

---

**Nota importante**: Nunca compartas tu archivo `.env` con información sensible. Siempre usa `.env.example` como plantilla.
