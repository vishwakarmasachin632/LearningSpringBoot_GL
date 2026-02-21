# MODULE 6 – SPRING MICROSERVICES

## Topic (i): Distributed Tracing (Micrometer + Zipkin)

---

## 1️⃣ THEORY (Beginner Friendly – Hinglish)

Microservices me **ek user request multiple services se hoke guzarti hai**.

👉 Problem:
- Error aaya, lekin **kis service me?**
- Request slow hai, lekin **kaun responsible?**

Monolith me logs dekhna easy hota tha ❌
Microservices me ye bahut hard ho jaata hai ❌

### Is problem ka solution hai:
> **Distributed Tracing**

Simple shabdon me:
> *Ek request ko end-to-end track karna across all microservices.*

---

## 2️⃣ WHAT IS DISTRIBUTED TRACING?

Distributed Tracing:
- Har request ko **unique Trace ID** deta hai
- Har service usi Trace ID ke saath logs likhti hai
- Poora request flow visible ho jaata hai

👉 Result:
✔ Faster debugging
✔ Performance bottleneck identify
✔ Production issues easy resolve

---

## 3️⃣ REAL-WORLD USE CASE

### E-Commerce Example

User places order:
```
Client → API Gateway → Order Service → Payment Service → Inventory Service
```

Agar payment slow ho:
- Trace ID se directly pata chal jaata hai
- Payment Service me delay dikhega

---

## 4️⃣ FLOW DIAGRAM (ASCII)

```
Client
  |
  v
API Gateway (TraceId: abc123)
  |
  v
Order Service (abc123)
  |
  v
Payment Service (abc123)
  |
  v
Inventory Service (abc123)
```

---

## 5️⃣ TOOLS USED (Spring Boot 3+)

- Micrometer Tracing
- Brave (Tracing library)
- Zipkin (UI + storage)

👉 Sleuth deprecated ho chuka hai

---

## 6️⃣ PRACTICAL IMPLEMENTATION

### 🗂 Project Setup
```
api-gateway
order-service
payment-service
zipkin-server
```

---

## 7️⃣ DEPENDENCIES (ALL SERVICES)

```xml
<dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-tracing-bridge-brave</artifactId>
</dependency>

<dependency>
    <groupId>io.zipkin.reporter2</groupId>
    <artifactId>zipkin-reporter-brave</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

---

## 8️⃣ APPLICATION CONFIGURATION

```yaml
management:
  tracing:
    sampling:
      probability: 1.0  # 100% requests trace

  zipkin:
    tracing:
      endpoint: http://localhost:9411/api/v2/spans
```

---

## 9️⃣ ZIPKIN SETUP

### Run Zipkin using Docker

```bash
docker run -d -p 9411:9411 openzipkin/zipkin
```

👉 UI Access:
```
http://localhost:9411
```

---

## 🔟 TRACE ID IN LOGS

### application.yml

```yaml
logging:
  pattern:
    level: "%5p [${spring.application.name},%X{traceId},%X{spanId}]"
```

### Sample Log
```
INFO [order-service,abc123,def456] Order placed successfully
```

---

## 1️⃣1️⃣ HOW IT WORKS (STEP BY STEP)

```
1. Client sends request
2. Gateway generates Trace ID
3. Trace ID propagated via headers
4. All services log same Trace ID
5. Zipkin visualizes complete flow
```

---

## 1️⃣2️⃣ BENEFITS

✔ End-to-end visibility
✔ Faster RCA (Root Cause Analysis)
✔ Production debugging easy

---

## 1️⃣3️⃣ COMMON MISTAKES

❌ Sampling too low (missed traces)
❌ Zipkin not reachable
❌ Logs without traceId pattern

---

## 🎯 INTERVIEW ONE-LINERS

- Distributed tracing tracks request across services
- TraceId remains same across services
- Micrometer replaced Sleuth in Spring Boot 3

---

## ✅ SUMMARY

✔ Distributed tracing is mandatory in microservices
✔ Helps debug & monitor production systems
✔ Zipkin provides visual trace flow

---

❓ **Should I move to the next topic?**
### 👉 MODULE 6 → Topic (j): Microservices Capstone Project

**Reply YES to continue**

