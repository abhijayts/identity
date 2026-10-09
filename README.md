# Identity

A small identity service that manages people and authenticates them. Other applications can use it to answer two questions: *who is this person?* and *are they allowed in?*

> **Status:** early development. The project skeleton, database setup and package layout are in place. The features below describe what the system is meant to do and are not all implemented yet.

## What it does

### Basic authentication

- **Register** a person with a unique identifier (username or email) and a password.
- **Log in** with those credentials and receive proof of authentication for later requests.
- **Verify** that proof so other services can trust who is calling.
- **Log out** to end a session.

Passwords are never stored in plain text. Only a salted hash is persisted.

### Features

- **Person management**: create, read, update and delete person records.
- **Credential management**: change a password and reset a forgotten one.
- **Account state**: accounts can be enabled or disabled, so a disabled person cannot log in.
- **Failed-login handling**: repeated failed attempts are limited to protect against guessing.

## Endpoints

All endpoints are served under the context path `/auth`.

| Method | Path | Purpose |
| ------ | ---- | ------- |
| POST | `/auth/register` | Create a new person (planned) |
| POST | `/auth/login` | Authenticate a person (planned) |
| POST | `/auth/logout` | End the current session (planned) |

## Tech stack

- Java 26
- Spring Boot 4.1.1
- Hibernate through Spring Data JPA
- PostgreSQL
- Maven (wrapper included)
- Lombok

## Getting started

### Prerequisites

- JDK 26
- A running PostgreSQL instance with a database named `identity`

### Configuration

The app reads these environment variables, defined in `src/main/resources/application.properties`:

| Variable | Default | Description |
| -------- | ------- | ----------- |
| `DB_URL` | `jdbc:postgresql://localhost:5432/identity` | JDBC connection URL |
| `DB_USERNAME` | `postgres` | Database user |
| `DB_PASSWORD` | none, required | Database password |

### Run

```bash
# macOS / Linux
export DB_PASSWORD=your-password
./mvnw spring-boot:run
```

```powershell
# Windows PowerShell
$env:DB_PASSWORD = "your-password"
.\mvnw.cmd spring-boot:run
```

The service is then available at `http://localhost:8080/auth`.

### Test

```bash
./mvnw test
```

## Project layout

```
src/main/java/com/ats/identity
├── IdentityApplication.java     application entry point
├── controller/                  HTTP endpoints (e.g. LoginController)
└── entity/                      JPA entities (e.g. PersonEntity)
```
