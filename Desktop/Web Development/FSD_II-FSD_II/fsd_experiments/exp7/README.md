# Exp_7: Spring Security with JWT and RBAC

A full-stack web application demonstrating Spring Security with JWT (JSON Web Tokens) authentication and Role-Based Access Control (RBAC). The project includes a Spring Boot backend API and a React frontend.

**Author:** Satvik Sharma

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Setup & Installation](#setup--installation)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [Authentication](#authentication)
- [Frontend Usage](#frontend-usage)
- [Configuration](#configuration)
- [Security Details](#security-details)

## Features

✅ **JWT Authentication** - Secure token-based authentication  
✅ **Role-Based Access Control (RBAC)** - User roles and permissions  
✅ **Spring Security** - Industry-standard security framework  
✅ **React Frontend** - Modern, responsive UI with Vite  
✅ **RESTful API** - Clean API design with proper HTTP methods  
✅ **Protected Resources** - Role-based endpoint access  

## Tech Stack

### Backend
- **Java 17**
- **Spring Boot 3.2.3**
- **Spring Security**
- **JWT (jjwt 0.11.5)**
- **Maven**

### Frontend
- **React 19.2.4**
- **Vite 8.0.4**
- **Axios 1.15.0**
- **Lucide React 1.8.0**
- **ESLint 9.39.4**

## Project Structure

```
exp7/
├── pom.xml                          # Maven configuration
├── README.md                        # This file
├── .gitignore                       # Git ignore rules
├── src/
│   └── main/
│       └── java/
│           └── com/fsd/exp7/
│               ├── Exp7Application.java         # Spring Boot entry point
│               ├── config/
│               │   └── SecurityConfig.java      # Spring Security configuration
│               ├── controller/
│               │   ├── AuthController.java      # Authentication endpoints
│               │   └── ResourceController.java  # Protected resource endpoints
│               └── security/
│                   ├── JwtAuthenticationFilter.java  # JWT filter
│                   └── JwtUtils.java                 # JWT utility methods
└── frontend/
    ├── package.json                 # NPM dependencies
    ├── vite.config.js              # Vite configuration
    ├── index.html                  # HTML entry point
    ├── src/
    │   ├── main.jsx                # React entry point
    │   ├── App.jsx                 # Main App component
    │   ├── AuthDashboard.jsx       # Auth UI component
    │   ├── App.css                 # Application styles
    │   └── index.css               # Global styles
    └── public/                     # Static assets
```

## Prerequisites

- **Java 17** or higher
- **Node.js 16** or higher
- **npm 8** or higher
- **Maven 3.6** or higher

## Setup & Installation

### Backend Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/Satvik995/Exp_7.git
   cd Exp_7
   ```

2. **Install backend dependencies**
   ```bash
   mvn clean install
   ```

3. **Build the project**
   ```bash
   mvn clean package
   ```

### Frontend Setup

1. **Navigate to frontend directory**
   ```bash
   cd frontend
   ```

2. **Install Node dependencies**
   ```bash
   npm install
   ```

## Running the Application

### Start Backend Server

```bash
# From project root
mvn spring-boot:run
```

The backend will start on `http://localhost:8080`

### Start Frontend Development Server

```bash
# From frontend directory
npm run dev
```

The frontend will start on `http://localhost:5173`

## API Endpoints

### Authentication Endpoints

| Method | Endpoint | Description | Authentication |
|--------|----------|-------------|-----------------|
| POST | `/api/auth/register` | Register new user | None |
| POST | `/api/auth/login` | Login user | None |
| POST | `/api/auth/refresh` | Refresh JWT token | Bearer Token |
| POST | `/api/auth/logout` | Logout user | Bearer Token |

### Protected Endpoints

| Method | Endpoint | Description | Required Role |
|--------|----------|-------------|----------------|
| GET | `/api/resources/admin` | Admin-only resource | ADMIN |
| GET | `/api/resources/user` | User resource | USER, ADMIN |
| GET | `/api/resources/public` | Public resource | None |

## Authentication

### Login Flow

1. User sends credentials to `/api/auth/login`
2. Server validates credentials and returns JWT token
3. Client stores token (typically in localStorage or sessionStorage)
4. Client includes token in Authorization header for protected requests

### JWT Token Structure

```
Authorization: Bearer <jwt-token>
```

### Token Claims

- `sub` - Subject (username)
- `iat` - Issued at timestamp
- `exp` - Expiration timestamp
- `roles` - User roles (ADMIN, USER, etc.)

## Frontend Usage

### Login Page
- Enter username and password
- Click "Login" to authenticate
- Token is automatically stored upon successful login

### Dashboard
- View user information
- Access role-based resources
- Logout functionality

### Error Handling
- Invalid credentials display error messages
- Expired tokens trigger re-authentication
- 403 Forbidden errors for insufficient permissions

## Configuration

### Application Properties

Create `application.properties` in `src/main/resources/`:

```properties
spring.application.name=Exp_7
server.port=8080

# JWT Configuration
jwt.secret=your-secret-key-here
jwt.expiration=3600000

# Database (if applicable)
spring.datasource.url=jdbc:mysql://localhost:3306/exp7
spring.datasource.username=root
spring.datasource.password=password

# JPA/Hibernate
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

## Security Details

### Password Security
- Passwords are encrypted using BCrypt
- Never store plain-text passwords
- Use strong passwords (minimum 8 characters)

### JWT Security
- Tokens are signed with a secret key
- Tokens have an expiration time
- Refresh tokens can be used to get new access tokens
- Tokens should be stored securely on the client

### CORS Configuration
- Configure allowed origins in `SecurityConfig`
- Restrict API access to trusted domains

### Role-Based Access Control
- Users are assigned roles (e.g., USER, ADMIN)
- Endpoints check user roles before granting access
- Custom annotations can be used for role checking

## Build for Production

### Backend
```bash
mvn clean package -DskipTests
java -jar target/Exp_7-0.0.1-SNAPSHOT.jar
```

### Frontend
```bash
cd frontend
npm run build
```

The optimized build will be in `frontend/dist/`

## Development

### Running Tests

```bash
# Backend tests
mvn test

# Frontend linting
cd frontend && npm run lint
```

### Code Format

Maintain consistent code style:
- Java: Follow Spring conventions
- JavaScript/React: Follow ESLint rules

## Contributing

When contributing to this project:
1. Create a feature branch
2. Make your changes
3. Test thoroughly
4. Commit with clear messages
5. Push and create a pull request

## License

This project is part of an educational experiment series.

## Support

For issues or questions, please create an issue on GitHub: https://github.com/Satvik995/Exp_7/issues

---

**Happy Coding!** 🚀
