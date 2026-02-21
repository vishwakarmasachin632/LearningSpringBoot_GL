# 📘 MODULE 1 – SPRING BASICS
## 🔹 Topic (h): Getting Started with Spring Boot

---

## 🧠 1. Spring Boot kya hai?

Spring Boot ek **opinionated framework** hai jo Spring applications ko **jaldi, easily aur production-ready** banata hai.

Simple shabdon me:
> **Spring Boot = Spring + Auto Configuration + Embedded Server**

Iska main goal hai:
- Boilerplate configuration hataana
- Application ko quickly start karna
- Production-ready defaults dena

---

## ❌ 2. Problem with Traditional Spring

Traditional Spring me:
- XML / Java config zyada hoti thi
- Server (Tomcat) alag se install karna padta
- Dependency management complex hota

👉 Beginners ke liye kaafi confusing hota tha.

---

## ✅ 3. Spring Boot ka Solution

Spring Boot automatically:
- Dependencies configure karta hai
- Embedded server deta hai (Tomcat)
- Sensible defaults apply karta hai

👉 Isliye Spring Boot **industry standard** ban chuka hai.

---

## 🧩 4. Key Features of Spring Boot

1. Auto Configuration
2. Starter Dependencies
3. Embedded Server
4. Production Ready (Actuator)
5. No XML Configuration

---

## 🚀 5. Spring Boot Project Creation (IntelliJ + Maven)

### Step 1: New Project
- IntelliJ IDEA → New Project
- Spring Initializr select karo

### Step 2: Project Settings
- Project: Maven
- Language: Java
- Spring Boot: Latest Stable
- Java: **21**

### Step 3: Dependencies Select karo
- Spring Web
- Spring Data JPA
- PostgreSQL Driver

---

## 📁 6. Project Structure (Important)

```
spring-boot-demo
│
├── src/main/java
│   └── com.example.demo
│       ├── DemoApplication.java
│       ├── controller
│       ├── service
│       └── repository
│
├── src/main/resources
│   ├── application.properties
│   └── static
│
└── pom.xml
```

---

## 🧠 7. @SpringBootApplication (Deep Explanation)

```java
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

### @SpringBootApplication kya karta hai?
Ye ek **meta-annotation** hai jo internally:
- `@Configuration`
- `@ComponentScan`
- `@EnableAutoConfiguration`

sab ko combine karta hai.

---

## 🧪 8. First Simple Controller

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello Spring Boot";
    }
}
```

👉 Browser me open karo:
```
http://localhost:8080/hello
```

---

## 🔄 9. Spring Boot Startup Flow

```
Application Start
      |
      v
@SpringBootApplication
      |
      v
Auto Configuration
      |
      v
Embedded Tomcat Start
      |
      v
Application Ready
```

---

## 🌍 10. Real World Use Case

### Enterprise Application

- Fast project bootstrap
- Microservices ready
- Cloud deployment easy

👉 Isliye almost sab companies Spring Boot use karti hain.

---

## ⚠️ 11. Common Beginner Mistakes

- Java version mismatch
- Wrong dependency selection
- Port already in use

---

## 🎯 12. Interview Focus

- Spring vs Spring Boot
- @SpringBootApplication ka role
- Embedded server kya hota hai

---

## ✅ 13. Summary

- Spring Boot Spring ka simplified version hai
- Auto-configuration sabse bada fayda
- Embedded server use hota hai
- Industry standard framework

---

## ⏭️ Next Topic

🔹 **Module 1 – Topic (i): Spring CLI**

❓ Should I move to the next topic?
👉 YES / NO likho

