<<<<<<< HEAD
# chat_application
=======
# Java Chat Server

A lightweight WebSocket-based chat server implemented in Java (Maven). The project includes a minimal browser client for local testing and stores chat history and users in a MySQL database.

**Tech stack:** Java 17, Maven, Java-WebSocket, MySQL, SLF4J

## Features
- WebSocket server with simple AUTH-based login
- Stores messages in MySQL and serves recent history on connect
- Minimal browser client at `client/index.html` for quick testing
- Packaged as an executable JAR via the Maven Shade plugin

## Prerequisites
- Java 17 (JDK)
- Maven
- MySQL (or compatible) database

## Database setup
Create a database and the required tables. Example SQL:

```sql
CREATE DATABASE chat_app;
USE chat_app;

CREATE TABLE users (
	id INT AUTO_INCREMENT PRIMARY KEY,
	username VARCHAR(100) NOT NULL UNIQUE,
	password VARCHAR(255) NOT NULL,
	display_name VARCHAR(255)
);

CREATE TABLE messages (
	id INT AUTO_INCREMENT PRIMARY KEY,
	sender_username VARCHAR(100) NOT NULL,
	content TEXT NOT NULL,
	timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Note: This project uses the connection constants in `src/main/java/JavaFinalProject/ChatServer.java`:
- `DB_URL` (jdbc url)
- `DB_USER`
- `DB_PASS`

Update these values or provide the correct credentials before running.

## Build and run
From the project root:

```bash
mvn clean package
# the shaded JAR will be created under target/ (name may include the version)
java -jar target/*-shaded.jar
```

By default the server listens on port `9090` and the `mainClass` is `JavaFinalProject.ChatServer`.

## Client (testing)
Open [client/index.html](client/index.html) in a browser (or serve it from a static server). The client connects to `ws://localhost:9090` and expects the server AUTH protocol:

- Send: `AUTH username password`
- Server responses: `AUTH_OK <displayName>` or `AUTH_FAIL ...`

## Logging
The project uses `slf4j-simple` for basic console logging. Adjust dependencies or logging configuration as needed.

## Development notes
- The server authenticates against the `users` table (plain text password check in this sample). For production use, store hashed passwords and use secure configuration.
- The client and server use a simple text-based protocol (`MSG`, `SYS`, `HIST`, `AUTH_OK`, `AUTH_FAIL`). See `client/index.html` and `ChatServer.java` for details.

## Contributing
- Open an issue or submit a PR. For changes to DB or protocol, include migration notes and client compatibility notes.

## License
This repository includes a `LICENSE` file. Check it for license details.

---
>>>>>>> d8a519f (Added full Java chat application project)
