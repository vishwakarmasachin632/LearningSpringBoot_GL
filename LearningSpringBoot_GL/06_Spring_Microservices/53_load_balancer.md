# MODULE 6 – SPRING MICROSERVICES

## Topic (d): Load Balancer (Spring Cloud LoadBalancer)

---

## 1️⃣ THEORY (Beginner Friendly – Hinglish)

Microservices me **ek hi service ke multiple instances** chal rahe hote hain (scaling ke liye).

👉 Question:
> *Request kaunse instance ko jaye?*

Is problem ka answer hai:
> **Load Balancer**

### Simple shabdon me:
> *Traffic ko smart tareeke se multiple service instances me distribute karna.*

---

## 2️⃣ WHY LOAD BALANCING IS REQUIRED

❌ Single instance overload ho sakta hai
❌ Performance slow ho jaati hai
❌ Service down hone ka risk

✅ Load balancer:
- Traffic distribute karta hai
- High availability deta hai
- Fault tolerance improve karta hai

---

## 3️⃣ TYPES OF LOAD BALANCING

### 🔹 Client-Side Load Balancing
- Client khud decide karta hai
- Service registry (Eureka) se list leta hai

**Example:** Spring Cloud LoadBalancer

### 🔹 Server-Side Load Balancing
- Ek central proxy decide karta hai

**Example:** Nginx, API Gateway

---

## 4️⃣ REAL-WORLD USE CASE

### E-Commerce Example

- Order Service → Payment Service
- Payment Service ke 3 instances running

### Without Load Balancer:
```
Order Service → Payment Service (Instance-1 only)
```

### With Load Balancer:
```
Order Service → Instance-1
             → Instance-2
             → Instance-3
```

---

## 5️⃣ FLOW DIAGRAM (ASCII)

```
            Order Service
                  |
                  v
        Spring Cloud LoadBalancer
          |        |        |
          v        v        v
     Payment-1  Payment-2  Payment-3
```

---

## 6️⃣ PRACTICAL IMPLEMENTATION

### 🗂 Project Setup
```
order-service
payment-service (run multiple instances)
```

---

## 7️⃣ DEPENDENCY (Order Service)

```xml
<!-- Spring Cloud LoadBalancer dependency -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-loadbalancer</artifactId>
</dependency>
```

---

## 8️⃣ RestTemplate WITH LOAD BALANCER

```java
// @Configuration:
// Purpose: Configuration class
// Why: Beans define karne ke liye
@Configuration
public class RestTemplateConfig {

    // @Bean:
    // Purpose: RestTemplate ko Spring container me register karna
    // When: Inter-service REST call ke liye
    
    // @LoadBalanced:
    // Purpose: RestTemplate ko load balancing capability dena
    // When: Service-name based URL use ho
    // Why: Eureka ke sath instance resolve karne ke liye
    @Bean
    @LoadBalanced
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```

---

## 9️⃣ SERVICE CALL USING SERVICE NAME

```java
String url = "http://PAYMENT-SERVICE/payments/process";
```

👉 LoadBalancer automatically instance choose karega (Round Robin by default)

---

## 🔟 RUN MULTIPLE SERVICE INSTANCES

```bash
java -jar payment-service.jar --server.port=8081
java -jar payment-service.jar --server.port=8082
java -jar payment-service.jar --server.port=8083
```

---

## 1️⃣1️⃣ COMMON ALGORITHMS

- Round Robin (default)
- Random
- Weighted

---

## 1️⃣2️⃣ COMMON PROBLEMS & SOLUTIONS

| Problem | Solution |
|-------|----------|
| Single instance overload | Load Balancer |
| Instance failure | Retry + Circuit Breaker |
| Uneven traffic | Weighted LB |

---

## 🎯 INTERVIEW ONE-LINERS

- Load balancer improves availability
- Spring Cloud LoadBalancer is client-side
- Works tightly with Eureka

---

## ✅ SUMMARY

✔ Load balancing is mandatory in microservices
✔ Prevents single point of failure
✔ Spring Cloud LB is simple & effective

---

❓ **Should I move to the next topic?**
### 👉 MODULE 6 → Topic (e): API Gateway (Spring Cloud Gateway)

**Reply YES to continue**

