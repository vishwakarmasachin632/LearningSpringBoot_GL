# MODULE 5 – SPRING SECURITY
## Topic (j): Securing REST APIs (JWT + OAuth2 + Roles)

---

## 1️⃣ REST APIs ko secure karna kyun zaroori hai?

REST APIs directly **business data expose** karti hain.

Agar security nahi ho to:
- Koi bhi data access kar sakta hai ❌
- Data leak / misuse ho sakta hai
- Legal & compliance issues

👉 Isliye **Authentication + Authorization mandatory** hai.

---

## 2️⃣ Real World Example

🏦 **Banking REST APIs**
- `/accounts` → sirf logged-in USER
- `/admin/users` → sirf ADMIN
- `/reports` → MANAGER / ADMIN

👉 Har API ka **role-based access** hota hai.

---

## 3️⃣ REST API Security Approaches

| Approach | Usage |
|---|---|
| Basic Auth | Testing only ❌ |
| Session Based | Web apps |
| JWT | REST + Microservices ✅ |
| OAuth2 | Social login / Enterprise |

---

## 4️⃣ Stateless Security Concept (IMPORTANT)

REST APIs me:
- Server **session store nahi karta**
- Har request me **token required**

```
Request → JWT → Validate → Process
```

---

## 5️⃣ SecurityFilterChain Configuration

```java
@Configuration
@EnableMethodSecurity
// 👉 Method level security enable karta hai
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {

        http
            // 👉 CSRF REST APIs ke liye disable
            .csrf().disable()

            // 👉 Authorization rules
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/auth/login").permitAll()
                .requestMatchers("/admin/**").hasRole("ADMIN")
                .requestMatchers("/user/**").hasAnyRole("USER", "ADMIN")
                .anyRequest().authenticated()
            )

            // 👉 JWT / OAuth2 ke liye stateless
            .sessionManagement(session ->
                session.sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            );

        return http.build();
    }
}
```

---

## 6️⃣ Secured REST Controller Example

```java
@RestController
@RequestMapping("/user")
// 👉 REST API expose karta hai
public class UserController {

    @GetMapping("/profile")
    // 👉 Sirf authenticated user access karega
    public String profile() {
        return "User Profile";
    }
}
```

---

## 7️⃣ Method Level Security (Best Practice)

```java
@Service
// 👉 Business logic layer
public class AdminService {

    @PreAuthorize("hasRole('ADMIN')")
    // 👉 Sirf ADMIN role
    public void deleteUser() {
        // delete logic
    }
}
```

👉 **Service layer security = industry standard**

---

## 8️⃣ REST API Security Flow (ASCII Diagram)

```
Client
 ↓ Authorization: Bearer JWT
Security Filter Chain
 ↓
JWT / OAuth2 Filter
 ↓
SecurityContextHolder
 ↓
Controller
 ↓
Service (@PreAuthorize)
 ↓
Response
```

---

## 9️⃣ HTTP Status Codes (Interview 🔥)

| Code | Meaning |
|---|---|
| 401 | Unauthorized (No/Invalid token) |
| 403 | Forbidden (No permission) |

---

## 🔟 Common Security Mistakes ❌

- CSRF enabled for REST
- Roles hardcoded in controller only
- Sensitive data in JWT payload
- No token expiration

---

## 1️⃣1️⃣ Summary

✔ REST APIs = Stateless
✔ JWT / OAuth2 preferred
✔ Role + Method security mandatory
✔ Proper HTTP status handling

---

❓ **Next topic move karein?**

🔹 MODULE 5 → Topic (k): Security Capstone Project

👉 Sirf **YES** likho

