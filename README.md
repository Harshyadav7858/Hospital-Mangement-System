# Hospital Management System (HMS)

Spring Boot 3.x, Java 17, MySQL 8, session-based authentication (HttpSession + Cookies). No JWT.

## Features
- Session auth with Spring Security and Spring Session JDBC
- CSRF enabled (Cookie token + X-CSRF-TOKEN header)
- Sample modules: Users, Doctors, Patients, Appointments
- Flyway migrations
- OpenAPI (Swagger UI at /swagger-ui/index.html)
- Docker and docker-compose

## Run locally
1. Start MySQL via docker-compose or a local instance
2. Configure `application.yml` datasource
3. Build and run
```bash
mvn spring-boot:run
```

## Session Auth
- POST /api/auth/login with JSON `{ "username":"admin", "password":"admin" }`
- Server sets `JSESSIONID` cookie
- Fetch CSRF token from `GET /api/auth/csrf` and include header `X-CSRF-TOKEN` for POST/PUT/DELETE
- Logout via `POST /api/auth/logout`

## Database
- Flyway migration `V1__init.sql` creates RBAC, domain, and Spring Session tables

## Docker
```bash
docker compose up --build
```

## Notes
- For production, set `server.servlet.session.cookie.secure=true` and use HTTPS/Reverse proxy.
