# MODULE 6 – SPRING MICROSERVICES

## Topic (g): Spring Cloud Bus (Config Refresh at Scale)

---

## 1️⃣ THEORY (Beginner Friendly – Hinglish)

Socho tumhare paas **10–20 microservices** running hain.

Config Server me tumne config change ki:
- DB password rotate
- Logging level change

👉 Problem:
❌ Har service ko manually restart karna pade
❌ Downtime aata hai

### Is problem ka solution:
> **Spring Cloud Bus**

Simple shabdon me:
> *Ek event bus jo config change ko sab microservices tak broadcast karta hai.*

---

## 2️⃣ WHAT IS SPRING CLOUD BUS?

- Spring Cloud ka component
- Distributed messaging ka use karta hai
- **RabbitMQ / Kafka** ke upar kaam karta hai

👉 Bus = **refresh events ka highway** 🚍

---

## 3️⃣ REAL-WORLD USE CASE

### E-Commerce Example

- 15 microservices
- Logging level change from INFO → DEBUG

Without Bus:
- 15 services restart ❌

With Bus:
- 1 refresh event
- Sab services update ho jaati hain ✅

---

## 4️⃣ FLOW DIAGRAM (ASCII)

```
   Git Repo
      |
      v
 Config Server
      |
  (Bus Event)
      |
 ─────────────────────────
 |     |      |          |
Order Payment User   Inventory
Svc   Svc     Svc        Svc
```

---

## 5️⃣ REQUIRED COMPONENTS

- Config Server
- Config Clients
- Message Broker (RabbitMQ / Kafka)

---

## 6️⃣ PRACTICAL IMPLEMENTATION (Using Kafka)

### 🗂 Project Setup
```
config-server
order-service
payment-service
user-service
kafka
```

---

## 7️⃣ DEPENDENCIES (ALL SERVICES)

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bus-kafka</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

---

## 8️⃣ APPLICATION CONFIG (ALL SERVICES)

```yaml
spring:
  kafka:
    bootstrap-servers: localhost:9092

management:
  endpoints:
    web:
      exposure:
        include: busrefresh
```

---

## 9️⃣ CONFIG REFRESH FLOW

```
1. Config change in Git
2. POST /actuator/busrefresh
3. Kafka topic publish
4. All services refresh config
```

---

## 🔟 ACTUATOR ENDPOINT

```http
POST http://localhost:8888/actuator/busrefresh
```

👉 Ek call → sab services update

---

## 1️⃣1️⃣ IMPORTANT ANNOTATIONS

```java
// @RefreshScope
// Purpose: Bean ko dynamic refresh enable karna
// When: Config runtime me change ho
// Why: Restart ke bina new values lene ke liye
@RefreshScope
@Service
public class OrderService {

    @Value("${order.discount}")
    private int discount;
}
```

---

## 1️⃣2️⃣ BENEFITS

✔ Zero downtime config change
✔ Centralized + scalable
✔ Production friendly

---

## 1️⃣3️⃣ COMMON PROBLEMS

| Issue | Fix |
|-----|-----|
| Config not refreshing | @RefreshScope missing |
| Bus not working | Broker down |

---

## 🎯 INTERVIEW ONE-LINERS

- Spring Cloud Bus propagates refresh events
- Uses messaging middleware
- Avoids service restart

---

## ✅ SUMMARY

✔ Cloud Bus = config refresh at scale
✔ Works with Config Server
✔ Mandatory for large systems

---

❓ **Should I move to the next topic?**
### 👉 MODULE 6 → Topic (h): Circuit Breaker (Resilience4j)

**Reply YES to continue**

