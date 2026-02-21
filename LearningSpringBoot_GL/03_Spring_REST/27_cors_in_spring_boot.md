# MODULE 3 → Topic (d): CORS (Cross-Origin Resource Sharing)

> **Language:** Hinglish (Beginner Friendly)
> **JDK:** 21
> **Spring Boot:** Latest Stable
> **DB:** PostgreSQL
> **IDE:** IntelliJ IDEA

---

## 1️⃣ THEORY – CORS kya hota hai?

CORS ka full form hai **Cross-Origin Resource Sharing**.

Simple words me:
- Jab **frontend (browser)** aur **backend (API)** alag origin se hote hain
- Aur browser API call ko **block** kar deta hai
- Us problem ko solve karne ke liye **CORS** use hota hai

### 🔍 Origin kya hota hai?
Origin = **Protocol + Domain + Port**

Example:
```
http://localhost:3000   (React App)
http://localhost:8080   (Spring Boot API)
```
➡️ Dono ka **port different** hai → **Different Origin**

Browser bolega:
> ❌ "Not allowed by CORS policy"

---

## 2️⃣ REAL-WORLD USE CASE

### 🎯 Use Case: React + Spring Boot Application

- React frontend → `http://localhost:3000`
- Spring Boot backend → `http://localhost:8080`

React se API call:
```
GET http://localhost:8080/api/employees
```

Browser security ke wajah se:
- Request backend tak jaati hai
- But response **block** ho jaata hai

➡️ Solution: **Enable CORS in Spring Boot**

---

## 3️⃣ CORS KA FLOW (BEGINNER VIEW)

```
Browser (React)
    |
    |  Request (Different Origin)
    v
Browser Security Check
    |
    |  ❌ Blocked (Without CORS)
    |  ✅ Allowed (With CORS headers)
    v
Spring Boot API
```

---

## 4️⃣ METHOD 1: @CrossOrigin (Controller Level)

### EmployeeController.java

```java
// @CrossOrigin
// Purpose: Cross-origin requests allow karta hai
// When: Specific controller ya API ke liye CORS chahiye
// Why here: React frontend se calls allow karni hain
@CrossOrigin(origins = "http://localhost:3000")
@RestController
@RequestMapping("/api/employees")
public class EmployeeController {
    // APIs
}
```

### ✅ Kab use karein?
- Small project
- Single frontend
- Quick testing

### ❌ Drawback
- Har controller pe repeat karna padega

---

## 5️⃣ METHOD 2: Global CORS Configuration (RECOMMENDED)

### WebConfig.java

```java
package com.company.ems.config;

import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

// @Configuration
// Purpose: Configuration class batata hai
// When: Custom framework settings chahiye
// Why here: Global CORS define karna hai
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("http://localhost:3000")
                .allowedMethods("GET", "POST", "PUT", "DELETE")
                .allowedHeaders("*")
                .allowCredentials(true);
    }
}
```

### ✅ Kab use karein?
- Production application
- Multiple controllers
- Clean & maintainable

---

## 6️⃣ METHOD 3: CORS with Spring Security (Preview)

> ⚠️ Jab Spring Security add hota hai
> normal CORS config kaam nahi karta

```java
http.cors();
```

👉 Isko hum **Spring Security module** me deeply cover karenge.

---

## 7️⃣ COMMON CORS ERRORS (INTERVIEW FAVORITES)

### ❌ Error:
```
Access to fetch at 'http://localhost:8080' from origin 'http://localhost:3000' has been blocked by CORS policy
```

### ✅ Solution:
- @CrossOrigin
- Global WebMvcConfigurer
- Proper allowedOrigins

---

## 8️⃣ INTERVIEW QUESTIONS & ANSWERS

### Q1: CORS browser-level security hai ya server-level?
👉 **Browser-level security**

### Q2: Postman me CORS issue kyun nahi aata?
👉 Postman browser nahi hai

### Q3: Best way to configure CORS?
👉 Global configuration

---

## 9️⃣ SUMMARY

✔ CORS browser security restriction hai
✔ Frontend-backend alag origin = CORS issue
✔ @CrossOrigin quick solution
✔ Global config best practice

---

❓ **Should I move to the next topic?**

🔹 MODULE 3 → Topic (e): OpenAPI / Swagger Documentation

👉 Sirf **YES** likho.

