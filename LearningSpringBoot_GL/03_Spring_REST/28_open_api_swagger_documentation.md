# MODULE 3 → Topic (e): OpenAPI / Swagger Documentation (Spring Boot)

> **Language:** Hinglish (Beginner Friendly)
> **JDK:** 21
> **Spring Boot:** Latest Stable
> **Build Tool:** Maven
> **IDE:** IntelliJ IDEA

---

## 1️⃣ THEORY – Swagger / OpenAPI kya hota hai?

Swagger (aajkal jise **OpenAPI** kehte hain) ek **API documentation tool** hai.

Simple language me:
- Tumhari REST APIs ka **live documentation**
- Browser me API dekh sakte ho
- API ko **test bhi kar sakte ho** (GET/POST/PUT/DELETE)

Socho:
> Backend dev + Frontend dev + Tester
> Sab ek hi jagah API samajh paate hain

---

## 2️⃣ REAL-WORLD USE CASE

### 🎯 Use Case: Team Project

Tumne Spring Boot me 50 APIs bana di:
- Employee API
- Department API
- Salary API

Frontend team bolegi:
❌ "POST body kya hai?"
❌ "Response structure kya hai?"

➡️ Solution:
✅ **Swagger UI**

Ek URL open karo:
```
http://localhost:8080/swagger-ui.html
```
Aur sab APIs **auto-documented** ✨

---

## 3️⃣ DEPENDENCY ADD KARNA (Maven)

### pom.xml

```xml
<!-- SpringDoc OpenAPI -->
<!-- Purpose: Swagger UI + OpenAPI support -->
<!-- When: REST APIs ka documentation chahiye -->
<!-- Why here: Manual documentation se bachne ke liye -->
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.5.0</version>
</dependency>
```

👉 Application restart karte hi Swagger ready.

---

## 4️⃣ SWAGGER UI ACCESS

Browser me open karo:
```
http://localhost:8080/swagger-ui.html
```

Ya
```
http://localhost:8080/swagger-ui/index.html
```

---

## 5️⃣ BASIC CONFIGURATION (OPTIONAL)

### OpenApiConfig.java

```java
package com.company.ems.config;

import io.swagger.v3.oas.models.OpenAPI;
import io.swagger.v3.oas.models.info.Info;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

// @Configuration
// Purpose: Configuration class batata hai
// When: Custom OpenAPI info chahiye
// Why here: Project ka proper description dikhana
@Configuration
public class OpenApiConfig {

    // @Bean
    // Purpose: Spring container me object register karta hai
    // When: Custom bean create karni ho
    // Why here: Swagger info customize karna
    @Bean
    public OpenAPI customOpenAPI() {
        return new OpenAPI()
                .info(new Info()
                        .title("Employee Management API")
                        .version("1.0")
                        .description("Spring Boot REST APIs for EMS"));
    }
}
```

---

## 6️⃣ CONTROLLER ANNOTATIONS (IMPORTANT)

### EmployeeController.java

```java
import io.swagger.v3.oas.annotations.Operation;
import io.swagger.v3.oas.annotations.tags.Tag;

// @Tag
// Purpose: Controller ko group karta hai
// When: Multiple controllers ho
// Why here: Employee APIs ek jagah dikhane ke liye
@Tag(name = "Employee APIs", description = "CRUD operations for employees")
@RestController
@RequestMapping("/api/employees")
public class EmployeeController {

    // @Operation
    // Purpose: API ka description deta hai
    // When: API explain karni ho
    // Why here: Frontend/tester ko samjhane ke liye
    @Operation(summary = "Create Employee", description = "New employee create karta hai")
    @PostMapping
    public Employee create(@RequestBody Employee employee) {
        return service.save(employee);
    }
}
```

---

## 7️⃣ SWAGGER FLOW (ASCII)

```
Developer / Tester
        |
        | Open Browser
        v
Swagger UI
        |
        | Calls API
        v
Spring Boot Controller
        |
        v
Service → Repository → DB
```

---

## 8️⃣ COMMON INTERVIEW QUESTIONS

### Q1: Swagger ka use kyun hota hai?
👉 API documentation + testing

### Q2: Swagger production me enable rakhna chahiye?
👉 ❌ No (Security risk)

### Q3: OpenAPI vs Swagger?
👉 Swagger = tool, OpenAPI = specification

---

## 9️⃣ PRODUCTION BEST PRACTICE

```yaml
springdoc:
  swagger-ui:
    enabled: false
```

👉 Production me disable kar do.

---

## 🔟 SUMMARY

✔ Live API documentation
✔ Frontend + backend coordination easy
✔ Testing without Postman
✔ Interview + industry must

---

❓ **Should I move to the next topic?**

🔹 MODULE 3 → Topic (f): API Testing with JUnit & Mockito

👉 Sirf **YES** likho.

