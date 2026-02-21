# MODULE 6 – SPRING MICROSERVICES

## Topic (h): Circuit Breaker (Resilience4j)

---

## 1️⃣ THEORY (Beginner Friendly – Hinglish)

Microservices me **ek service doosri service par depend karti hai**.

👉 Agar dependent service slow ya down ho jaaye:
❌ Request hang ho jaati hai
❌ Threads block ho jaate hain
❌ Puri application slow / down ho sakti hai

### Is problem ka solution hai:
> **Circuit Breaker Pattern**

Simple shabdon me:
> *Jaise ghar ka MCB – fault aate hi supply cut kar deta hai taaki system bacha rahe.*

---

## 2️⃣ WHAT IS CIRCUIT BREAKER?

Circuit Breaker:
- Failures detect karta hai
- Calls ko temporarily block karta hai
- System ko **self-heal** karne ka time deta hai

👉 Ye **fault tolerance** ka core concept hai

---

## 3️⃣ CIRCUIT BREAKER STATES

### 🔴 CLOSED
- Normal state
- Requests allowed

### 🟡 OPEN
- Failures threshold cross
- Requests blocked

### 🟢 HALF-OPEN
- Limited test requests
- Success → CLOSED
- Failure → OPEN

---

## 4️⃣ REAL-WORLD USE CASE

### E-Commerce Example

- Order Service → Payment Service
- Payment Service down

Without Circuit Breaker:
- Order Service bhi slow ❌

With Circuit Breaker:
- Fast failure
- Fallback response

---

## 5️⃣ FLOW DIAGRAM (ASCII)

```
Order Service
     |
     v
Circuit Breaker
   /     \
  v       X
Payment   Blocked
Service   Calls
```

---

## 6️⃣ WHY RESILIENCE4J?

- Lightweight
- Functional style
- Spring Boot friendly
- Netflix Hystrix replacement

👉 **Industry standard choice**

---

## 7️⃣ PRACTICAL IMPLEMENTATION

### 🗂 Project Setup
```
order-service
payment-service
```

---

## 8️⃣ DEPENDENCIES (Order Service)

```xml
<dependency>
    <groupId>io.github.resilience4j</groupId>
    <artifactId>resilience4j-spring-boot3</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

---

## 9️⃣ APPLICATION CONFIGURATION

```yaml
resilience4j:
  circuitbreaker:
    instances:
      paymentService:
        failure-rate-threshold: 50
        minimum-number-of-calls: 5
        wait-duration-in-open-state: 10s
        permitted-number-of-calls-in-half-open-state: 2
```

---

## 🔟 SERVICE METHOD WITH CIRCUIT BREAKER

```java
// @Service
// Purpose: Business logic layer
@Service
public class OrderService {

    // @CircuitBreaker
    // Purpose: Method ko circuit breaker se protect karna
    // When: External service call ho
    // Why: Failure se system ko bachane ke liye
    @CircuitBreaker(name = "paymentService", fallbackMethod = "paymentFallback")
    public String placeOrder() {
        // REST call to Payment Service
        return "Payment Success";
    }

    // Fallback method
    // Purpose: Jab circuit open ho ya error aaye
    // Why: Graceful degradation
    public String paymentFallback(Exception ex) {
        return "Payment service unavailable. Please try later.";
    }
}
```

---

## 1️⃣1️⃣ ACTUATOR ENDPOINTS

```yaml
management:
  endpoints:
    web:
      exposure:
        include: health,info,circuitbreakers
```

---

## 1️⃣2️⃣ BENEFITS

✔ Prevents cascading failure
✔ Fast failure response
✔ Improves system stability

---

## 1️⃣3️⃣ COMMON MISTAKES

❌ Circuit breaker missing on external calls
❌ No fallback defined
❌ Wrong threshold values

---

## 🎯 INTERVIEW ONE-LINERS

- Circuit breaker prevents cascading failures
- Resilience4j replaces Hystrix
- Fallback provides graceful degradation

---

## ✅ SUMMARY

✔ Circuit breaker is mandatory in microservices
✔ Protects system from failures
✔ Improves resilience

---

❓ **Should I move to the next topic?**
### 👉 MODULE 6 → Topic (i): Distributed Tracing

**Reply YES to continue**

