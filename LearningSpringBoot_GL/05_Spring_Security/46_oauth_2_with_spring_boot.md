# MODULE 5 – SPRING SECURITY
## Topic (i): OAuth2 with Spring Boot (Industry Standard)

---

## 1️⃣ OAuth2 kya hota hai? (Simple Hindi)

OAuth2 ek **authorization framework** hai jo kisi third‑party application ko **user ka password diye bina** limited access deta hai.

👉 Example:
- "Login with Google"
- "Login with GitHub"

Tum apna password **Google ko dete ho**, app ko nahi ❌

---

## 2️⃣ OAuth2 vs JWT (CONFUSION CLEAR 🔥)

| OAuth2 | JWT |
|------|-----|
| Authorization framework | Token format |
| 3rd party login | Self login |
| Google, GitHub | Custom auth |
| Social login | Internal APIs |

👉 OAuth2 **JWT use karta hai**, but dono same nahi hain

---

## 3️⃣ Real World Example

🧑‍💼 **Company HR Portal**
- Employee → Login with Google
- Google verifies identity
- HR app ko token milta hai
- App user ko access deta hai

```
User → App → Google → Token → App → Access
```

---

## 4️⃣ OAuth2 Roles

| Role | Description |
|---|---|
| Resource Owner | User |
| Client | Your App |
| Authorization Server | Google |
| Resource Server | Your Backend API |

---

## 5️⃣ OAuth2 Grant Types (Interview 🔥)

| Grant Type | Usage |
|---|---|
| Authorization Code | Web apps (MOST USED) |
| Client Credentials | Service to service |
| Password | Deprecated ❌ |

---

## 6️⃣ Maven Dependencies

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-client</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

---

## 7️⃣ application.yml (Google OAuth2)

```yaml
spring:
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: YOUR_CLIENT_ID
            client-secret: YOUR_CLIENT_SECRET
            scope: profile, email
```

---

## 8️⃣ Security Configuration

```java
@Configuration
// 👉 Security config class
@EnableMethodSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {

        http
            .authorizeHttpRequests(auth -> auth
                .anyRequest().authenticated()
            )
            // 👉 OAuth2 login enable
            .oauth2Login();

        return http.build();
    }
}
```

---

## 9️⃣ OAuth2 Login Flow (ASCII Diagram)

```
User
 ↓ Click Login with Google
App
 ↓ Redirect
Google Login Page
 ↓ Consent
Authorization Code
 ↓
Access Token
 ↓
App Backend
```

---

## 🔟 OAuth2 Resource Server (JWT Validate)

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-resource-server</artifactId>
</dependency>
```

```java
http
  .oauth2ResourceServer()
  .jwt();
```

---

## 1️⃣1️⃣ Common Interview Questions 🔥

- OAuth2 kya problem solve karta hai?
- OAuth2 vs JWT difference?
- Authorization Code flow explain karo
- OAuth2 me password kahan jata hai?

---

## 1️⃣2️⃣ Summary

✔ OAuth2 = Secure 3rd party login
✔ Password sharing nahi hota
✔ Authorization Code flow most used
✔ Industry standard for social login

---

❓ **Next topic move karein?**

🔹 MODULE 5 → Topic (j): Securing REST APIs

👉 Sirf **YES** likho

