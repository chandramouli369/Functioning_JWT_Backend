**Spring Boot JWT Authentication Backend - File Explanations and Responsibilities**

---

###  README.md for the Project

####  Project Title: JWT Auth API with Spring Boot

####  Description:

This project is a Spring Boot backend application that provides user authentication and authorization using JWT (JSON Web Tokens). It includes secure signup and login endpoints and validates each request using a token-based approach.

####  Features:

* User Signup with role assignment
* User Login with JWT issuance
* Role-based access control
* Secure API using Spring Security
* Token validation for all protected endpoints

####  Technologies Used:

* Spring Boot
* Spring Security
* JWT (JJWT library)
* JPA (Hibernate)
* MySQL
* Maven

####  Project Structure:

* `controller/` – API endpoints (e.g. signup, login)
* `dto/` – Request payload classes
* `model/` – JPA entity (User)
* `repository/` – Data access layer for User entity
* `service/` – JWT generation and validation logic
* `filter/` – JWT filter to intercept and verify token on each request
* `config/` – Spring Security configuration
* `application.properties` – App configuration

####  How Authentication & Authorization Work:

* Authentication is done when a user logs in. If credentials are valid, a JWT token is generated.
* Authorization is done by intercepting each HTTP request using `JwtFilter`, verifying the token, and checking user roles in `SecurityConfig`.

####  API Endpoints:

```http
POST /api/auth/signup
Content-Type: application/json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password",
  "role": "USER"
}

POST /api/auth/login
Content-Type: application/json
{
  "email": "john@example.com",
  "password": "password"
}
```

####  Run Locally:

1. Clone the repository
2. Configure DB in `application.properties`
3. Run using your IDE or `mvn spring-boot:run`
4. Test using Postman or connect to frontend

---

###  Authentication & Authorization Explained:

* **Authentication** happens in:

  * `AuthController.login(...)` — verifies email/password and issues a JWT if credentials are valid.
  * `JwtService.generateToken(...)` — creates a signed JWT token using user info.

* **Authorization** happens in:

  * `JwtFilter.doFilterInternal(...)` — intercepts requests, validates JWT, sets authentication in Spring Security context.
  * `SecurityConfig` — restricts access to protected endpoints based on roles and authenticated users.

---

###  Project Structure and File Purpose:

#### `JwtauthNagaApplication.java`

* **Purpose:** Entry point of the Spring Boot application.
* **Why Needed:** Bootstraps the app using `@SpringBootApplication`.

---

#### `controller/AuthController.java`

* **Purpose:** Handles `/signup` and `/login` API endpoints.
* **Why Needed:** Exposes auth endpoints for user registration and login.

---

#### `dto/SignupRequest.java` & `LoginRequest.java`

* **Purpose:** DTO classes to encapsulate user input data for signup and login.
* **Why Needed:** Cleanly separates request body mapping from domain model (`User`).

---

#### `model/User.java`

* **Purpose:** Entity class mapped to the `user` table in the database.
* **Why Needed:** Represents authenticated users, used in security and DB persistence.

---

#### `repository/UserRepository.java`

* **Purpose:** Extends `JpaRepository` to allow CRUD operations on `User` entity.
* **Why Needed:** To fetch/save user data from/to database.

---

#### `service/JwtService.java`

* **Purpose:** Generates, parses, and validates JWT tokens.
* **Why Needed:** Core utility for JWT-based authentication.

---

#### `service/UserService.java` (if present)

* **Purpose:** Implements `UserDetailsService` for Spring Security.
* **Why Needed:** Provides user detail fetching logic for authentication.

---

#### `filter/JwtFilter.java`

* **Purpose:** Intercepts HTTP requests, extracts JWT, validates it, and sets authentication.
* **Why Needed:** Ensures only authenticated users can access secured endpoints.

---

#### `config/SecurityConfig.java`

* **Purpose:** Defines Spring Security rules (which endpoints are secured, JWT filter setup, etc).
* **Why Needed:** Customizes and secures the web application endpoints.

---

#### `application.properties`

* **Purpose:** Holds configuration such as DB credentials and server port.
* **Why Needed:** Allows externalizing config values for different environments.

---
