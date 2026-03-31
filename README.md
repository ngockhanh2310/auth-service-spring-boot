# Demo Spring Identity Service

A robust and scalable Identity and Access Management (IAM) service built with **Spring Boot 3**, **Java 21**, and **Spring Security**. This service provides comprehensive user authentication, authorization, and role-based access control (RBAC) using JWT (JSON Web Tokens).

## Features

- **User Management**: Creating, updating, and retrieving user profiles.
- **Role & Permission Management**: Dynamic assignment of roles and permissions to users.
- **Authentication**: JWT-based login and token issuance.
- **Authorization**: Role-based and Permission-based access control for API endpoints.
- **Token Management**: Token introspection, refreshing, and secure logout mechanisms.
- **Data Mapping**: Seamless conversion between Entities and DTOs using **MapStruct**.
- **Validation**: Automatic request validation using Spring Boot Validation.
- **Testing**: Includes unit and integration tests with H2 Database, plus code coverage reports using **JaCoCo**.

## Tech Stack

- **Language**: Java 21
- **Framework**: Spring Boot 3.5.x
- **Security**: Spring Security 6.5.x, OAuth2 Resource Server (JWT)
- **Database**: 
  - MySQL 8.x (Production/Development)
  - H2 Database (Testing)
  - Spring Data JPA (Hibernate)
- **Utilities**: 
  - Lombok (Boilerplate reduction)
  - MapStruct (Object mapping)
- **Build Tool**: Maven

## Project Architecture

The project follows a standard layered architecture:
- `controller`: Exposes RESTful APIs (User, Role, Permission, Authentication).
- `service`: Contains the core business logic.
- `repository`: Interfaces with the database via Spring Data JPA.
- `entity`: Represents the database tables (JPA entities).
- `dto`: Data Transfer Objects for API requests and responses.
- `mapper`: MapStruct interfaces for mapping between Entities and DTOs.
- `exception`: Global exception handling and custom exception definitions.
- `config`: Security and standard application configurations.

## ⚙️ Configuration & Setup

### Requirements
- JDK 21 or higher
- Maven 3.x
- MySQL Database

### Database Configuration

Make sure your MySQL server is running. Update the database connection settings in `src/main/resources/application.yaml`:

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/identity_service
    username: root
    password: mysql_pw
```

### Running the Application

You can use Maven Wrapper to run the application directly from the root directory:

```bash
./mvnw spring-boot:run
```

The server will start on default port `8080` with the context path `/demo_identity`.

## Authentication & Authorization Flow

1. **User Creation**: Admin or User creates an account.
2. **Login**: User logs in providing `username` and `password` via `/auth/token`.
3. **Token Issuance**: The server verifies credentials and returns a signed `JWT` token containing the user's roles and permissions.
4. **API Access**: The client sends the token in the `Authorization: Bearer <token>` header to access protected resources.
5. **Token Introspection/Refresh/Logout**: Dedicated endpoints allow for validating a token's state, refreshing an expired token, or logging a user out securely.

## Testing

The project includes test configurations using an in-memory **H2 Database** to prevent interference with the local MySQL data.

To run tests and generate a code coverage report with **JaCoCo**:

```bash
./mvnw clean test
```

Coverage reports will be generated in `target/site/jacoco`.
