# MODULE 6 – SPRING MICROSERVICES

## Topic (f): Centralized Config Server (Spring Cloud Config)

---

## 1️⃣ THEORY (Beginner Friendly – Hinglish)

Microservices architecture me **har service ka alag configuration** hota hai:
- DB URL
- Username / Password
- Server port
- Feature flags

👉 Agar har service me alag‑alag config file ho:
❌ Maintain karna mushkil
❌ Change ke liye redeploy
❌ Environment mismatch (dev / qa / prod)

### Is problem ka solution hai:
> **Centralized Config Server**

Simple shabdon me:
> *Ek central jagah jahan saari services ka configuration store hota hai.*

---

## 2️⃣ WHAT IS SPRING CLOUD CONFIG

- Spring Cloud ka component
- External configuration manage karta hai
- Git / File system / Vault support

### Components:
- **Config Server** → Config provide karta hai
- **Config Client** → Config consume karta hai

---

## 3️⃣ REAL‑WORLD USE CASE

### E‑Commerce Example

- Order Service
- Payment Service
- User Service

Sab services:
- Same DB config
- Same logging config

👉 Config ek jagah change karo → sab services update

---

## 4️⃣ FLOW DIAGRAM (ASCII)

```
        Git Repository
             |
             v
     Config Server (8888)
             |
     -------------------
     |        |        |
 Order   Payment    User
 Service  Service   Service
```

---

## 5️⃣ PRACTICAL IMPLEMENTATION

### 🗂 Project Structure
```
config-server
order-service
payment-service
user-service
config-repo (Git)
```

---

## 6️⃣ CONFIG SERVER SETUP

### pom.xml

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```

---

### Application Class

```java
// @SpringBootApplication
// Purpose: Spring Boot application entry point
// Why: Auto configuration + component scan
@SpringBootApplication

// @EnableConfigServer
// Purpose: Is app ko Config Server banana
// When: Centralized config chahiye
// Why: Clients ko config provide karne ke liye
@EnableConfigServer
public class ConfigServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

---

### application.yml (Config Server)

```yaml
server:
  port: 8888

spring:
  application:
    name: config-server

  cloud:
    config:
      server:
        git:
          uri: https://github.com/your-org/config-repo
          clone-on-start: true
```

---

## 7️⃣ CONFIG REPOSITORY STRUCTURE

```
config-repo
 ├── order-service.yml
 ├── payment-service.yml
 ├── user-service.yml
```

---

## 8️⃣ SAMPLE CONFIG FILE (order-service.yml)

```yaml
server:
  port: 8081

spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/orderdb
    username: postgres
    password: postgres
```

---

## 9️⃣ CONFIG CLIENT SETUP (Order Service)

### pom.xml

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```

---

### bootstrap.yml

```yaml
spring:
  application:
    name: order-service

  cloud:
    config:
      uri: http://localhost:8888
```

---

## 🔟 CONFIG FETCH FLOW

```
Order Service start
  ↓
Config Server call
  ↓
Git repo se config
  ↓
Config Order Service ko milta hai
```

---

## 1️⃣1️⃣ BENEFITS

✔ Single source of truth
✔ No redeploy for config change
✔ Environment specific config

---

## 1️⃣2️⃣ COMMON PROBLEMS & SOLUTIONS

| Problem | Solution |
|------|---------|
| Config server down | Fail‑fast disabled |
| Wrong config | Profiles (dev/prod) |

---

## 🎯 INTERVIEW ONE‑LINERS

- Config Server externalizes configuration
- Uses Git as backend
- bootstrap.yml loads before application.yml

---

## ✅ SUMMARY

✔ Centralized config is mandatory in microservices
✔ Avoids duplication
✔ Improves consistency

---

❓ **Should I move to the next topic?**
### 👉 MODULE 6 → Topic (g): Spring Cloud Bus

**Reply YES to continue**

