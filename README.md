# 💬 Real-Time Chat Application

A real-time chat application built using **Spring Boot**, **WebSocket**, **STOMP**, and **SockJS**.  
It allows multiple users to chat instantly through a simple and responsive UI.

---

## 🚀 Features

- 🔌 Real-time messaging via WebSockets  
- 👥 Multi-user chat support  
- 🌐 STOMP protocol with SockJS fallback  
- 🖥 Simple Bootstrap 5 UI  
- 📡 Publish/Subscribe model using topics  
- ⚙ Fully integrated frontend and backend  

---

## 🛠 Tech Stack

### Backend
- Spring Boot  
- Spring WebSocket  
- STOMP  
- SockJS  
- Java 17+  

### Frontend
- HTML5  
- Bootstrap 5  
- JavaScript  
- SockJS Client  
- STOMP.js  

---

## 📁 Project Structure

```
src/
 ├─ main/java/com/chat/app/
 │   ├─ config/
 │   │   └─ WebSocketConfig.java
 │   ├─ controller/
 │   │   └─ ChatController.java
 │   ├─ model/
 │   │   └─ ChatMessage.java
 │   └─ ChatApplication.java
 └─ main/resources/templates/
     └─ chat.html
```

---

## ⚙ WebSocket Flow

### Frontend
- Connects to endpoint: `/chat`
- Sends messages to: `/app/sendMessage`
- Subscribes to: `/topic/messages`

### Backend
- WebSocket endpoint: `/chat`
- Application prefix: `/app`
- MessageMapping: `/sendMessage`
- Broadcast topic: `/topic/messages`

---

## 🧩 Configuration Overview

### WebSocketConfig.java
```java
registry.addEndpoint("/chat")
        .setAllowedOrigins("http://localhost:8080")
        .withSockJS();

registry.enableSimpleBroker("/topic");
registry.setApplicationDestinationPrefixes("/app");
```

---

## 📥 Sending a Message (Frontend)

```javascript
stompClient.send("/app/sendMessage", {}, JSON.stringify({
    sender: "User",
    content: "Hello!"
}));
```

---

## 📤 Backend Message Handler

```java
@MessageMapping("/sendMessage")
@SendTo("/topic/messages")
public ChatMessage sendMessage(ChatMessage message) {
    return message;
}
```

---

## ▶️ How to Run the Project

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd chat-app
```

### 2. Run the Spring Boot Application
```bash
mvn spring-boot:run
```

### 3. Open in Browser
```
http://localhost:8080/chat
```

### 4. Start Chatting 🎉

---

## 📝 ChatMessage Model

```java
public class ChatMessage {
    private String sender;
    private String content;

    // getters and setters
}
```

---

## 🎯 Future Enhancements

- User online/offline status  
- Private (one-to-one) chat  
- Message timestamps  
- Chat persistence using database  
- JWT-based authentication  
- Cloud deployment  

---

## 🤝 Contributing

Contributions are welcome!  
For major changes, please open an issue first to discuss what you want to improve.

---

## 📜 License

This project is open-source and free to use.

