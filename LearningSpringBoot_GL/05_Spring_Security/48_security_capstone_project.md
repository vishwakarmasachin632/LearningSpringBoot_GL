# MODULE 5 – SPRING SECURITY
## Topic (k): Security Capstone Project (Industry‑Ready)

---

## 🎯 Project Overview

**Project Name:** Secure Banking REST API

**Goal:**
- JWT based authentication
- Role based authorization (USER / ADMIN)
- Secure REST APIs
- PostgreSQL database
- Industry standard folder structure

---

## 🧱 Architecture (Layered)

```
Controller  →  Service  →  Repository  →  Database
        ↑           ↓
     Security Filters (JWT)
```

---

## 📁 Folder Structure

```
com.example.securityapp
│
├── config        → Security + JWT config
├── controller    → REST APIs
├── service       → Business logic
├── repository    → DB access
├── entity        → JPA entities
├── security      → JWT filter, util
├── exception     → Custom exceptions
└── SecurityAppApplication.java
```

---

## 🗄️ Database Schema (PostgreSQL)

```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(50) UNIQUE,
  password VARCHAR(255),
  role VARCHAR(20)
);
```

---

## 🔐 Security Configuration

```java
@Configuration
// 👉 Security related configuration
@EnableMethodSecurity
// 👉 Method level security enable
public class SecurityConfig {

    @Bean
    // 👉 JWT + REST ke liye filter chain
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {

        http
          .csrf().disable()
          .authorizeHttpRequests(auth -> auth
             .requestMatchers("/auth/login").permitAll()
             .requestMatchers("/admin/**").hasRole("ADMIN")
             .anyRequest().authenticated()
          )
          .sessionManagement(session ->
             session.sessionCreationPolicy(SessionCreationPolicy.STATELESS)
          );

        return http.build();
    }
}
```

---

## 🔑 JWT Utility

```java
@Component
// 👉 JWT token generate & validate
public class JwtUtil {

    private final String SECRET = "secretkey";

    public String generateToken(String username) {
        return Jwts.builder()
            .setSubject(username)
            .setIssuedAt(new Date())
            .setExpiration(new Date(System.currentTimeMillis()+3600000))
            .signWith(Keys.hmacShaKeyFor(SECRET.getBytes()), SignatureAlgorithm.HS256)
            .compact();
    }
}
```

---

## 🧰 Authentication Controller

```java
@RestController
@RequestMapping("/auth")
// 👉 Login related APIs
public class AuthController {

    @PostMapping("/login")
    // 👉 Login endpoint
    public String login() {
        return "JWT_TOKEN";
    }
}
```

---

## 👤 User Controller

```java
@RestController
@RequestMapping("/user")
public class UserController {

    @GetMapping("/profile")
    // 👉 Authenticated user only
    public String profile() {
        return "User Profile";
    }
}
```

---

## 🛡️ Admin Controller

```java
@RestController
@RequestMapping("/admin")
public class AdminController {

    @GetMapping("/dashboard")
    // 👉 Only ADMIN role
    public String dashboard() {
        return "Admin Dashboard";
    }
}
```

---

## 🔄 Complete Security Flow

```
Client
 ↓ Login
Auth Controller
 ↓ JWT
Client stores token
 ↓ Authorization Header
JWT Filter
 ↓ SecurityContext
Controller → Service → DB
```

---

## 🧪 Testing Scenarios

- Login without token → ❌ 401
- USER accessing /admin → ❌ 403
- ADMIN accessing /admin → ✅ 200

---

## 🎤 Interview Talking Points

- JWT stateless kyun hota hai?
- Role vs Authority
- 401 vs 403
- Method level security kyun better hai?

---

## ✅ Project Outcome

✔ Industry ready security project
✔ Resume + GitHub ready
✔ Microservices compatible

---

❓ **Next topic move karein?**

🔹 MODULE 5 → Topic (l): Spring Security Assessment (30 MCQs)

👉 Sirf **YES** likho

