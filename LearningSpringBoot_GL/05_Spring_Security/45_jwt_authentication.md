# MODULE 5 – SPRING SECURITY
## Topic (h): JWT Authentication (Industry Standard)

---

## 1️⃣ JWT Authentication kya hota hai?

JWT (JSON Web Token) Authentication ek **stateless authentication mechanism** hai jisme:
- Server session maintain nahi karta
- Client ke paas ek **signed token** hota hai
- Har request me token send hota hai

👉 **Microservices & REST APIs ka industry standard** ✅

---

## 2️⃣ Problem with Session-Based Auth (Why JWT?)

| Session Based | JWT Based |
|---|---|
| Server memory use hoti hai | Stateless (no memory) |
| Scaling me problem | Easily scalable |
| Microservices me tough | Microservices friendly |

---

## 3️⃣ Real World Example

🛒 **E‑Commerce App**
- User login karta hai
- Server JWT generate karta hai
- Client har API call me token bhejta hai

```
Client → Login → JWT → Authorization Header → APIs
```

---

## 4️⃣ JWT Structure (VERY IMPORTANT 🔥)

```
HEADER.PAYLOAD.SIGNATURE
```

### 🔹 Header
- Algorithm + Token type

### 🔹 Payload
- User info (username, roles)

### 🔹 Signature
- Secret key se sign hota hai

👉 Payload **encrypted nahi hota**, sirf signed hota hai

---

## 5️⃣ Maven Dependencies

```xml
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-api</artifactId>
    <version>0.11.5</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-impl</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-jackson</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
```

---

## 6️⃣ JWT Utility Class (Token Generate + Validate)

```java
@Component
// 👉 JWT related utility methods ke liye
public class JwtUtil {

    private final String SECRET = "mysecretkey";

    // 👉 Token generate karne ke liye
    public String generateToken(String username) {
        return Jwts.builder()
                .setSubject(username)
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + 1000 * 60 * 60))
                .signWith(Keys.hmacShaKeyFor(SECRET.getBytes()), SignatureAlgorithm.HS256)
                .compact();
    }

    // 👉 Username extract karne ke liye
    public String extractUsername(String token) {
        return Jwts.parserBuilder()
                .setSigningKey(SECRET.getBytes())
                .build()
                .parseClaimsJws(token)
                .getBody()
                .getSubject();
    }
}
```

---

## 7️⃣ JWT Authentication Filter

```java
@Component
// 👉 Har request pe JWT validate karne ke liye
public class JwtFilter extends OncePerRequestFilter {

    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain filterChain)
            throws ServletException, IOException {

        String authHeader = request.getHeader("Authorization");

        if (authHeader != null && authHeader.startsWith("Bearer ")) {
            String token = authHeader.substring(7);
            // 👉 Token validate logic yahan hota hai
        }
        filterChain.doFilter(request, response);
    }
}
```

---

## 8️⃣ Security Configuration with JWT

```java
@Configuration
@EnableMethodSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {

        http
            .csrf().disable()
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/login").permitAll()
                .anyRequest().authenticated()
            );

        return http.build();
    }
}
```

---

## 9️⃣ JWT Authentication Flow (ASCII Diagram)

```
Client
  ↓ Login
Auth Controller
  ↓ Generate JWT
Client stores token
  ↓
Authorization: Bearer <JWT>
  ↓
JWT Filter
  ↓
SecurityContext
  ↓
Protected API
```

---

## 🔟 Common Interview Questions 🔥

- JWT stateless kyun hota hai?
- JWT vs Session difference?
- JWT me sensitive data rakhna chahiye?
- Token expire hone ke baad kya hota hai?

---

## 1️⃣1️⃣ Summary

✔ JWT = Stateless authentication
✔ Microservices & REST APIs ke liye best
✔ Token me sirf minimal info rakho
✔ Next: OAuth2 easy ho jaata hai

---

❓ **Next topic move karein?**

🔹 MODULE 5 → Topic (i): OAuth2 with Spring Boot

👉 Sirf **YES** likho

