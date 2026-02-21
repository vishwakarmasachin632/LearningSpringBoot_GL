# MODULE 6 – SPRING MICROSERVICES

## Topic (j): Microservices Capstone Project (Industry-Ready)

---

## 🎯 PROJECT OVERVIEW (Hinglish)

**Project Name:** E-Commerce Microservices System  
**Goal:** End-to-end production-ready microservices architecture banana using Spring Boot + Spring Cloud.

### Tech Stack
- Java 21
- Spring Boot (Latest Stable)
- Spring Cloud
- Maven
- PostgreSQL
- Kafka
- Eureka
- Gateway
- Config Server
- Resilience4j
- Micrometer + Zipkin

---

## 🧩 MICROSERVICES LIST

| Service | Responsibility |
|------|---------------|
| api-gateway | Single entry point |
| eureka-server | Service registry |
| config-server | Central config |
| order-service | Order management |
| payment-service | Payment processing |
| inventory-service | Stock management |

---

## 🗂 OVERALL FOLDER STRUCTURE

```
root-project
 ├── api-gateway
 ├── eureka-server
 ├── config-server
 ├── order-service
 ├── payment-service
 ├── inventory-service
 └── config-repo
```

---

## 🔁 COMPLETE REQUEST FLOW (ASCII)

```
Client
  ↓
API Gateway
  ↓
Order Service
  ↓ (REST + Circuit Breaker)
Payment Service
  ↓ (Kafka Event)
Inventory Service

Tracing: TraceId flows everywhere
Config: Centralized via Config Server
```

---

## 1️⃣ EUREKA SERVER

### Annotations Used
```java
// @EnableEurekaServer
// Purpose: Registry banana
// When: Microservices discovery ke liye
// Why: Dynamic IP resolution
```

---

## 2️⃣ CONFIG SERVER

### Annotations Used
```java
// @EnableConfigServer
// Purpose: Central config provider
// When: Multiple services ho
// Why: No redeploy on config change
```

---

## 3️⃣ API GATEWAY

### application.yml Routes

```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: order
          uri: lb://ORDER-SERVICE
          predicates:
            - Path=/api/orders/**
```

### Why Gateway?
- Security
- Logging
- Routing
- Load balancing

---

## 4️⃣ ORDER SERVICE (CORE SERVICE)

### Package Structure
```
order-service
 └── controller
 └── service
 └── repository
 └── entity
 └── exception
```

---

### ENTITY

```java
@Entity // DB table mapping
@Table(name = "orders")
public class Order {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String productCode;
    private Integer quantity;
}
```

---

### REPOSITORY

```java
@Repository // Persistence layer
public interface OrderRepository extends JpaRepository<Order, Long> {}
```

---

### SERVICE

```java
@Service // Business logic
public class OrderService {

    @CircuitBreaker(name = "paymentService", fallbackMethod = "fallback")
    public String placeOrder() {
        // REST call to payment service
        return "Order Placed";
    }

    public String fallback(Exception ex) {
        return "Payment unavailable";
    }
}
```

---

### CONTROLLER

```java
@RestController // REST endpoints
@RequestMapping("/orders")
public class OrderController {

    @PostMapping
    public String placeOrder() {
        return "Order Created";
    }
}
```

---

## 5️⃣ PAYMENT SERVICE

### Responsibility
- Payment processing
- Failures simulate

---

## 6️⃣ INVENTORY SERVICE (KAFKA)

### Kafka Listener

```java
@KafkaListener(topics = "order-created")
public void consume(String message) {
    // Reduce stock
}
```

---

## 7️⃣ CENTRALIZED CONFIG

### config-repo/order-service.yml

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/orderdb
```

---

## 8️⃣ OBSERVABILITY

- Circuit Breaker → Resilience4j
- Tracing → Zipkin
- Metrics → Actuator

---

## 9️⃣ LOGGING PATTERN

```yaml
logging:
  pattern:
    level: "%5p [${spring.application.name},%X{traceId}]"
```

---

## 🔟 EXCEPTION HANDLING

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public String handle(Exception ex) {
        return ex.getMessage();
    }
}
```

---

## 1️⃣1️⃣ PRODUCTION CHECKLIST

✔ Service discovery
✔ Gateway
✔ Central config
✔ Circuit breaker
✔ Tracing
✔ Logging
✔ Async messaging

---

## 🎯 INTERVIEW EXPLANATION (HOW TO TELL HR)

> "I designed an end-to-end microservices system using Spring Cloud with Eureka, Gateway, Config Server, Resilience4j, Kafka and Zipkin. The system supports fault tolerance, centralized configuration, distributed tracing and asynchronous communication."

---

## ✅ SUMMARY

✔ Industry-grade microservices project
✔ All Spring Cloud components used
✔ HR + architect level explanation ready

---

❓ **Should I move to the next topic?**
### 👉 MODULE 6 → Topic (k): Microservices Self Assessment (30+ MCQs)

**Reply YES to continue**

