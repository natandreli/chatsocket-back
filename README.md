# My ChatSocket — Backend

This is the **backend** of the `My ChatSocket` real-time messaging application. It's a lightweight Spring Boot service that enables full-duplex communication via **WebSocket (STOMP over SockJS)**, allowing multiple users to exchange messages within shared rooms.

👉 The **frontend** (Angular) for this project is available [here](https://github.com/natandreli/chatsocket-front).

## 🔧 Tech Stack

- Java 17
- Spring Boot 3
- Spring WebSocket (STOMP)
- SockJS
- Maven
- Lombok

## 📡 How It Works

- WebSocket endpoint exposed at:  
  `ws://localhost:3000/chat-socket`

- Clients connect using SockJS + STOMP protocol.
- Messages sent to `/app/chat/{roomId}`.
- The server broadcasts messages to `/topic/{roomId}`.

### WebSocket Flow

```text
Client → /app/chat/room1 → Controller → /topic/room1 → All clients
```

## 📁 Key Files

| File | Purpose |
|------|---------|
| `WebSocketConfiguration.java` | Sets up endpoint, message broker, and allowed origins. |
| `WebSocketController.java`    | Handles incoming chat messages and broadcasts them. |
| `ChatMessage.java`            | DTO representing a message (id, text, user). |
| `application.properties`      | Configures server to run on port `3000`. |


## ▶️ Running Locally

### Prerequisites

- Java 17
- Maven

### Run the app

```bash
git clone https://github.com/natandreli/chatsocket-back.git
cd chatsocket-back
./mvnw spring-boot:run
```

Once running, WebSocket endpoint is available at:
```
http://localhost:3000/chat-socket
```

### CORS

The backend accepts connections only from:
```
http://localhost:4200
```

Ensure the frontend is served from that origin.

## 📦 Dependencies (in `pom.xml`)

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-websocket</artifactId>
</dependency>
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
  <groupId>org.projectlombok</groupId>
  <artifactId>lombok</artifactId>
  <optional>true</optional>
</dependency>
```

## 🔗 Related Repositories

- [My ChatSocket Frontend](https://github.com/natandreli/chatsocket-front)
