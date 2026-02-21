# MODULE 6 – SPRING MICROSERVICES

## Topic (e): API Gateway (Spring Cloud Gateway)

---

## 1️⃣ THEORY (Beginner Friendly – Hinglish)

Microservices architecture me **multiple services** hoti hain:
- order-service
- user-service
- payment-service

👉 Agar client directly har service ko call kare:
❌ Complexity badhti hai
❌ Security weak hoti hai
❌ Cross-cutting concerns repeat hote hain

### Iska solution hai:
> **API Gateway**

Simple shabdon me:
> *Client aur microservices ke beech ek single entry point.*

---

## 2️⃣ WHAT API GATEWAY DOES

API Gateway:
- Single endpoint provide karta hai
- Routing karta hai
- Authentication / Authorization
- Rate limiting
- Logging
- Load balancing integration

👉 Industry me ye **mandatory component** hota hai

---

## 3️⃣ REAL-WORLD USE CASE

### E-Commerce Example

Client ko sirf ek URL pata hota hai:
```
https://api.shop.com
```

Behind the scene:
```
/api/orders  → Order Service
/api/users   → User Service
/api/pay     → Payment Service
```

Client ko services ka idea hi nahi hota 👍

---

## 4️⃣ FLOW DIAGRAM (ASCII)

```
Client
  |
  v
API Gateway
  |      |       |
  v      v       v
Order  User   Payment
Service Service Service
```

---

## 5️⃣ SPRING CLOUD GATEWAY

- Reactive based (Non-blocking)
- Built on Project Reactor
- Netflix Zuul ka replacement

👉 **Spring Cloud Gateway = Industry Standard**

---

## 6️⃣ PRACTICAL IMPLEMENTATION

### 🗂 Project Structure
```
api-gateway
order-service
user-service
payment-service
```

---

## 7️⃣ DEPENDENCIES (API Gateway)

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

---

## 8️⃣ APPLICATION CONFIGURATION

### application.yml

```yaml
server:
  port: 8080

spring:
  application:
    name: api-gateway

  cloud:
    gateway:
      routes:
        - id: order-service
          uri: lb://ORDER-SERVICE
          predicates:
            - Path=/api/orders/**

        - id: user-service
          uri: lb://USER-SERVICE
          predicates:
            - Path=/api/users/**

        - id: payment-service
          uri: lb://PAYMENT-SERVICE
          predicates:
            - Path=/api/payments/**


eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

---

## 9️⃣ API GATEWAY APPLICATION CLASS

```java
// @SpringBootApplication
// Purpose: Spring Boot app start
// Why: Auto config + component scan
@SpringBootApplication

// @EnableEurekaClient
// Purpose: Gateway ko Eureka se register karna
// When: Service discovery chahiye
@EnableEurekaClient
public class ApiGatewayApplication {
    public static void main(String[] args) {
        SpringApplication.run(ApiGatewayApplication.class, args);
    }
}
```

---

## 🔟 REQUEST FLOW EXAMPLE

```
Client → http://localhost:8080/api/orders/1
      → API Gateway
      → Order Service
      → Response back to Client
```

---

## 1️⃣1️⃣ COMMON FEATURES IMPLEMENTED AT GATEWAY

| Feature | Reason |
|------|-------|
| Authentication | Central security |
| Logging | Single place logging |
| Rate Limiting | DDoS protection |
| CORS | Browser access |

---

## 1️⃣2️⃣ INTERVIEW QUESTIONS (Quick)

- API Gateway is **single entry point**
- Spring Cloud Gateway is **non-blocking**
- Uses **Netty + Reactor**

---

## ✅ SUMMARY

✔ API Gateway hides microservices
✔ Simplifies client communication
✔ Central place for security & logging

---

❓ **Should I move to the next topic?**
### 👉 MODULE 6 → Topic (f): Centralized Config Server (Spring Cloud Config)

**Reply YES to continue**

