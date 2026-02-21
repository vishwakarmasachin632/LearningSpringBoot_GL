# MODULE 6 – SPRING MICROSERVICES

## Topic (c): Service Registry & Discovery (Eureka)

---

## 1️⃣ THEORY (Beginner Friendly – Hinglish)

Microservices me **services dynamically up/down hoti rehti hain**.

👉 IP address aur port **hardcode karna impossible** hota hai.

Is problem ka solution hai:
> **Service Registry & Discovery**

Simple shabdon me:
> *Ek central phonebook jahan saari services apna naam aur address register karti hain.*

---

## 2️⃣ WHAT IS EUREKA?

- Eureka Netflix ka tool hai
- Spring Cloud Netflix ka part
- **Service Registry** ka kaam karta hai

### Roles:
- **Eureka Server** → Registry (phonebook)
- **Eureka Client** → Services jo register hoti hain

---

## 3️⃣ REAL-WORLD USE CASE

### E-Commerce Example

- Order Service ko User Service call karni hai
- Order Service ko User Service ka IP nahi pata

### Solution:
- User Service → Eureka me register
- Order Service → Eureka se lookup

---

## 4️⃣ FLOW DIAGRAM (ASCII)

```
         Eureka Server
         (Registry)
              ▲
              │ register
   ┌──────────┼──────────┐
   ▼          ▼          ▼
Order     User     Payment
Service   Service   Service

Order Service → Eureka → User Service
```

---

## 5️⃣ PRACTICAL IMPLEMENTATION

### 🗂 Project Structure
```
eureka-server
order-service
user-service
```

---

## 6️⃣ EUREKA SERVER SETUP

### pom.xml

```xml
<!-- Spring Cloud Netflix Eureka Server dependency -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

---

### Application Class

```java
// @SpringBootApplication:
// Purpose: Spring Boot app entry point
// Why: Auto configuration + component scan
@SpringBootApplication

// @EnableEurekaServer:
// Purpose: Is application ko Eureka Server banana
// When: Jab registry banana ho
// Why: Clients ko register allow karne ke liye
@EnableEurekaServer
public class EurekaServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
    }
}
```

---

### application.yml

```yaml
server:
  port: 8761

spring:
  application:
    name: eureka-server

eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
```

---

## 7️⃣ EUREKA CLIENT SETUP (Order Service)

### pom.xml

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

---

### application.yml

```yaml
spring:
  application:
    name: order-service

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

---

### Application Class

```java
// @SpringBootApplication:
// Purpose: Spring Boot app start
@SpringBootApplication

// @EnableEurekaClient:
// Purpose: Is service ko Eureka client banana
// When: Jab service registry me register karni ho
// Why: Dynamic discovery ke liye
@EnableEurekaClient
public class OrderServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(OrderServiceApplication.class, args);
    }
}
```

---

## 8️⃣ SERVICE CALL USING SERVICE NAME

```java
String url = "http://USER-SERVICE/users/1";
```

👉 Eureka automatically resolve karega IP + port

---

## 9️⃣ COMMON PROBLEMS & SOLUTIONS

| Problem | Solution |
|-------|----------|
| Hardcoded URLs | Eureka |
| Dynamic scaling | Eureka + LoadBalancer |
| Service down | Retry + Circuit Breaker |

---

## 🔟 INTERVIEW QUESTIONS (Quick)

- Eureka is **client-side discovery**
- Services heartbeat bhejte hain
- Eureka is not recommended for Kubernetes

---

## ✅ SUMMARY

✔ Service registry avoids hardcoding
✔ Eureka simplifies communication
✔ Required for load balancing

---

❓ **Should I move to the next topic?**
### 👉 MODULE 6 → Topic (d): Load Balancer (Spring Cloud LoadBalancer)

**Reply YES to continue**

