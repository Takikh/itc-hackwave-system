# ITC Hackwave System

> Spring Boot backend for the **Hackwave** kiosk & event management system — built by **ITC**.

---

## Overview

ITC Hackwave System is a RESTful backend application designed to power kiosk-based event management. The project is built on **Spring Boot 3.5.4** with **Java 24**, using **MariaDB** for persistence and **Spring Data JPA** (Hibernate) for ORM.

The system is currently in its **initial scaffolding phase** — the core project structure, database connectivity, and build pipeline are in place and ready for feature development.

---

## Tech Stack

| Layer        | Technology                        |
|--------------|-----------------------------------|
| Language     | Java 24                           |
| Framework    | Spring Boot 3.5.4                 |
| ORM          | Spring Data JPA (Hibernate)       |
| Database     | MariaDB                           |
| Validation   | Spring Boot Starter Validation    |
| Build Tool   | Maven (with Maven Wrapper)        |
| Testing      | JUnit 5 / Spring Boot Test        |

---

## Project Structure

```
src/
├── main/
│   ├── java/itc/tech/projects/hackwave/
│   │   └── HackwaveApplication.java      # Application entry point
│   └── resources/
│       ├── application.yaml               # App & DB configuration
│       └── banner.txt                     # Custom startup banner
└── test/
    └── java/itc/tech/projects/hackwave/
        └── HackwaveApplicationTests.java  # Context load test
```

---

## Getting Started

### Prerequisites

- **Java 24** (JDK)
- **Maven 3.9+** (or use the included Maven Wrapper)
- **MariaDB 10.6+** running on `localhost:3306`

### 1. Set Up the Database

```sql
CREATE DATABASE `itc-hackwave` CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
-- The default config uses root/root credentials.
-- For production, create a dedicated user:
CREATE USER 'hackwave'@'%' IDENTIFIED BY 'hackwave';
GRANT ALL ON `itc-hackwave`.* TO 'hackwave'@'%';
FLUSH PRIVILEGES;
```

### 2. Configure the Application

Database settings are in `src/main/resources/application.yaml`:

```yaml
spring:
  datasource:
    url: jdbc:mariadb://localhost:3306/itc-hackwave
    username: root
    password: root
```

> **Note:** `ddl-auto` is set to `drop-and-create` for development. Change to `update` or `validate` before production use.

### 3. Build & Run

```bash
# Using the Maven Wrapper (no Maven install needed)
./mvnw spring-boot:run

# Or build a JAR and run it
./mvnw clean package
java -jar target/hackwave-0.0.1-SNAPSHOT.jar
```

On Windows:

```cmd
mvnw.cmd spring-boot:run
```

### 4. Run Tests

```bash
./mvnw test
```

---

## Planned Features (Roadmap)

The following features are planned for upcoming development:

- **Authentication** — JWT-based auth with access & refresh tokens
- **QR Code Validation** — Validate QR data with kiosk logging
- **Event Management** — CRUD endpoints for events
- **Check-in System** — Log attendee check-ins per event/kiosk
- **CORS Configuration** — Support for Electron-based kiosk clients
- **Database Migrations** — Flyway for versioned schema management
- **Structured Logging** — JSON logging via Logback

### Planned API Endpoints

| Method | Endpoint              | Description                          |
|--------|-----------------------|--------------------------------------|
| GET    | `/api/health`         | Health check                         |
| POST   | `/api/auth/register`  | Register a new user                  |
| POST   | `/api/auth/login`     | Login and receive JWT tokens         |
| POST   | `/api/auth/refresh`   | Refresh an expired access token      |
| POST   | `/api/qr/validate`    | Validate a QR code                   |
| GET    | `/api/events`         | List all events                      |
| GET    | `/api/events/{id}`    | Get event details                    |
| POST   | `/api/checkins`       | Log a check-in (authenticated)       |

---

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/my-feature`)
3. Commit your changes (`git commit -m "feat: add my feature"`)
4. Push to the branch (`git push origin feature/my-feature`)
5. Open a Pull Request

---

## License

This project is proprietary to **ITC**.
