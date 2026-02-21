# MODULE 6 – SPRING MICROSERVICES

## Topic (b): Inter‑Service Communication (REST, Sync & Async)

---

## 1️⃣ THEORY (Beginner Friendly – Hinglish)

Microservices architecture me **har service independent hoti hai**, apna khud ka database aur business logic hota hai.

👉 Lekin **real applications me services ko ek‑dusre se baat karni hi padti hai**.

Is process ko kehte hain:
> **Inter‑Service Communication**

### Simple line me:
> *Ek microservice ka doosri microservice se data ya action mangna.*

---

## 2️⃣ TYPES OF INTER‑SERVICE COMMUNICATION

### 🔹 1. Synchronous Communication (REST)
- Request bhejo
- Response ka wait karo
- Blocking nature

**Example:**
- Order Service → User Service
- "Is user valid hai ya nahi?"

### 🔹 2. Asynchronous Communication (Event‑Based)
- Message bhejo
- Response ka wait nahi
- Non‑blocking

**Example:**
- Order placed → Kafka topic publish
- Inventory & Email services listen karte hain

---

## 3️⃣ REAL‑WORLD USE CASE (E‑Commerce)

### Scenario:
- User places order

### Flow:
```
Client
  ↓
Order Service
  ↓ (REST Call)
User Service (validate user)
  ↓
Order Confirmed
  ↓ (Event)
Kafka Topic: order-created
  ↓                ↓
Inventory Service   Email Service
```

---

## 4️⃣ FLOW DIAGRAM (ASCII)

### 🔁 Synchronous (REST)
```
Order Service ──HTTP──▶ User Service
      │                    │
      ◀────Response────────┘
```

### 🔁 Asynchronous (Event)
```
Order Service ──▶ Kafka Topic
                     │
         ┌───────────┴───────────┐
         ▼                       ▼
Inventory Service        Email Service
```

---

## 5️⃣ PRACTICAL IMPLEMENTATION (Spring Boot – REST Based)

### 🗂 Project Structure
```
order-service
 └── controller
 └── service
 └── client

user-service
 └── controller
 └── service
```

---

## 6️⃣ REST CALL USING RestTemplate

### 📌 Order Service – UserClient

```java
// @Component: Spring container me is class ko bean banane ke liye
// Kyunki ye dependency injection ke through use hogi
@Component
public class UserClient {

    // @Autowired: Spring automatically RestTemplate ka object inject karega
    // When: jab multiple beans ho
    // Why: manual object creation avoid karne ke liye
    @Autowired
    private RestTemplate restTemplate;

    public Boolean isUserValid(Long userId) {
        String url = "http://USER-SERVICE/users/" + userId + "/validate";
        return restTemplate.getForObject(url, Boolean.class);
    }
}
```

---

## 7️⃣ RestTemplate Bean Configuration

```java
// @Configuration: batata hai ye configuration class hai
@Configuration
public class RestTemplateConfig {

    // @Bean: method ke return object ko Spring container me bean bana deta hai
    // When: jab third‑party class ho
    // Why: RestTemplate ko manage karne ke liye
    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```

---

## 8️⃣ Order Service Logic

```java
// @Service: business logic layer define karta hai
@Service
public class OrderService {

    @Autowired
    private UserClient userClient;

    public String placeOrder(Long userId) {
        Boolean isValid = userClient.isUserValid(userId);

        if (!isValid) {
            throw new RuntimeException("Invalid User");
        }
        return "Order Placed Successfully";
    }
}
```

---

## 9️⃣ COMMON PROBLEMS (Interview Important)

❌ Tight coupling
❌ Service down → cascading failure
❌ Network latency

### Solution:
- Service Discovery
- Load Balancer
- Circuit Breaker (Resilience4j)
- Async messaging

---

## 🔟 WHEN TO USE WHAT?

| Scenario | Use |
|--------|-----|
| Immediate response | REST (Sync) |
| High scalability | Async (Kafka) |
| Critical flow | REST + Retry |
| Loose coupling | Event Driven |

---

## 🎯 INTERVIEW ONE‑LINERS

- REST is **blocking**, Kafka is **non‑blocking**
- Sync = tight coupling
- Async = eventual consistency

---

## ✅ SUMMARY

✔ Inter‑service communication is backbone of microservices
✔ REST = simple but risky
✔ Async = scalable but complex
✔ Industry uses **hybrid approach**

---

❓ **Should I move to the next topic?**
### 👉 MODULE 6 → Topic (c): Service Registry & Discovery (Eureka)

**Reply YES to continue**

