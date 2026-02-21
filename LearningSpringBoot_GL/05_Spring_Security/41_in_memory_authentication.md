# MODULE 5 – SPRING SECURITY
## Topic (d): In-Memory Authentication

> Language: Hinglish  
> JDK: 21 | Spring Boot: Latest Stable | Maven | IntelliJ IDEA

---

## 1️⃣ In-Memory Authentication kya hota hai?

**In-Memory Authentication** me users aur unke roles **application ke memory** me define hote hain.

Simple shabdon me:
> Users database me nahi, balki **code/configuration me hardcoded** hote hain.

Ye approach:
- Learning
- Demo
- POC
- Interviews
ke liye best hota hai.

---

## 2️⃣ Kab use karte hain? (WHEN)

✅ Use karo jab:
- Project small ho
- Database ready na ho
- Sirf security flow samajhna ho

❌ Avoid karo jab:
- Production system ho
- Dynamic users chahiye

---

## 3️⃣ Real-World Example

### Internal Admin Tool

- Sirf 2–3 fixed users
- Limited access
- No DB dependency

👉 In-memory authentication perfect fit

---

## 4️⃣ Dependency (pom.xml)

```xml
<!-- Spring Security Starter -->
<!-- Purpose: Security features enable karna -->
<!-- When: Jab authentication/authorization chahiye -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

---

## 5️⃣ Security Configuration Class

```java
package com.example.security.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.Customizer;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.web.SecurityFilterChain;

// @Configuration
// Purpose: Spring ko batata hai ki ye class configuration define karti hai
// When: Jab custom security setup likhna ho
// Why here: In-memory users define karne ke liye
@Configuration
public class SecurityConfig {

    // @Bean
    // Purpose: Security filter chain define karna
    // Why: Default security behavior ko override karna
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/admin/**").hasRole("ADMIN")
                .requestMatchers("/user/**").hasAnyRole("USER", "ADMIN")
                .anyRequest().authenticated()
            )
            .httpBasic(Customizer.withDefaults());

        return http.build();
    }

    // @Bean
    // Purpose: In-memory users define karna
    // Why: Database ke bina authentication chahiye
    @Bean
    public UserDetailsService userDetailsService(PasswordEncoder encoder) {

        // User with USER role
        UserDetails user = User.withUsername("user")
                .password(encoder.encode("user123"))
                .roles("USER")
                .build();

        // User with ADMIN role
        UserDetails admin = User.withUsername("admin")
                .password(encoder.encode("admin123"))
                .roles("ADMIN")
                .build();

        return new InMemoryUserDetailsManager(user, admin);
    }

    // @Bean
    // Purpose: Password ko encrypt karna
    // Why: Plain text password insecure hota hai
    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

---

## 6️⃣ Controller for Testing

```java
package com.example.security.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

// @RestController
// Purpose: Simple secured endpoints banana
@RestController
public class TestController {

    @GetMapping("/user/hello")
    public String userHello() {
        return "Hello USER";
    }

    @GetMapping("/admin/hello")
    public String adminHello() {
        return "Hello ADMIN";
    }
}
```

---

## 7️⃣ Flow Diagram (ASCII)

```
Client Request
   ↓
Security Filter Chain
   ↓
In-Memory User Check
   ↓
Role Verification
   ↓
Controller
```

---

## 8️⃣ Testing Scenario

| User | URL | Result |
|----|----|----|
| user | /user/hello | ✅ Allowed |
| user | /admin/hello | ❌ 403 |
| admin | /admin/hello | ✅ Allowed |

---

## 9️⃣ Interview Ready Points

- In-memory authentication DB-free hota hai
- Mostly learning/demo ke liye
- Production me JDBC/JPA use hota hai
- PasswordEncoder mandatory

---

## 🔟 Summary

- In-memory auth beginners ke liye best
- Authentication + Authorization dono clear hote hain
- Next step = JDBC authentication (real DB)

---

✅ Topic (d) COMPLETE

❓ **Should I move to next topic?**

🔹 MODULE 5 → Topic (e): JDBC Authentication

👉 Sirf **YES** likho.

