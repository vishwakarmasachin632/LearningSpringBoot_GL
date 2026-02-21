# MODULE 5 – SPRING SECURITY
## Topic (e): JDBC Authentication (Database Based Authentication)

---

## 1️⃣ JDBC Authentication kya hota hai?

JDBC Authentication ka matlab hota hai **user credentials (username, password, roles)** ko **database (PostgreSQL / MySQL)** me store karke authenticate karna.

👉 Real projects me **In-Memory auth use nahi hota**, kyunki:
- Users dynamic hote hain
- Passwords secure way me store hote hain
- Roles change hote rehte hain

Isliye **Database based authentication = Industry standard** ✅

---

## 2️⃣ Real World Example

🏦 **Banking Application**
- Users table me customer login details
- Roles table me `ROLE_USER`, `ROLE_ADMIN`
- Login ke time Spring Security DB se data uthata hai

Flow:
```
User → Login API → Spring Security → DB → Authentication Success/Fail
```

---

## 3️⃣ Required Database Tables (PostgreSQL)

### 🔹 users table
```sql
CREATE TABLE users (
    username VARCHAR(50) PRIMARY KEY,
    password VARCHAR(100) NOT NULL,
    enabled BOOLEAN NOT NULL
);
```

### 🔹 authorities table
```sql
CREATE TABLE authorities (
    username VARCHAR(50),
    authority VARCHAR(50)
);
```

👉 Ye **Spring Security ka default schema** hai

---

## 4️⃣ Maven Dependencies

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>

<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
</dependency>
```

---

## 5️⃣ application.yml Configuration

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/securitydb
    username: postgres
    password: postgres
  sql:
    init:
      mode: always
```

---

## 6️⃣ Security Configuration Class

```java
@Configuration
// 👉 Ye class security related beans define karegi
public class SecurityConfig {

    @Bean
    // 👉 Password ko encrypt/decrypt karne ke liye
    // 👉 JDBC auth me mandatory hai
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    @Bean
    // 👉 Spring Security ka core configuration
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {

        http
            // 👉 Authorization rules define karte hain
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/admin").hasRole("ADMIN")
                .requestMatchers("/user").hasAnyRole("USER", "ADMIN")
                .anyRequest().authenticated()
            )
            // 👉 Form based login enable
            .formLogin()
            // 👉 CSRF disable (REST / testing ke liye)
            .and().csrf().disable();

        return http.build();
    }
}
```

---

## 7️⃣ How Spring Security JDBC Authentication Works (Flow)

```
Client
  ↓
Login Request
  ↓
Authentication Filter
  ↓
JDBC UserDetailsService
  ↓
Users Table + Authorities Table
  ↓
PasswordEncoder (BCrypt)
  ↓
Authentication Success / Failure
```

---

## 8️⃣ Important Interview Points 🔥

- JDBC auth uses **UserDetailsService internally**
- Default queries:
  - users table → username, password, enabled
  - authorities table → username, authority
- Password **plain text kabhi nahi** ❌
- BCrypt recommended encoder

---

## 9️⃣ In-Memory vs JDBC Authentication

| Feature | In-Memory | JDBC |
|------|---------|------|
| Users | Hardcoded | Database |
| Scalability | ❌ | ✅ |
| Production | ❌ | ✅ |
| Dynamic Roles | ❌ | ✅ |

---

## 🔟 Summary

✔ JDBC Authentication = Real world authentication
✔ Database se user + role load hota hai
✔ Spring Security internally sab handle karta hai
✔ Foundation for JWT, OAuth2, Microservices Security

---

❓ **Next topic move karein?**

🔹 MODULE 5 → Topic (f): Password Encoding & BCrypt

👉 Sirf **YES** likho

