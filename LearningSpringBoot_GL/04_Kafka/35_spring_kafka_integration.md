# MODULE 4 – APACHE KAFKA
## Topic (d): Spring Kafka Integration

> Language: Hinglish
> JDK: 21 | Spring Boot: Latest Stable | Build Tool: Maven | IDE: IntelliJ IDEA
> Database: PostgreSQL (later capstone me use hoga)

---

## 1️⃣ Spring Kafka kya hota hai?

**Spring Kafka** ek abstraction layer hai jo Apache Kafka ke upar banti hai aur Kafka ko **Spring Boot applications ke saath easily integrate** karne me help karti hai.

Simple shabdo me:
> Java Kafka = low-level
> Spring Kafka = high-level + production ready

---

## 2️⃣ Spring Kafka kyu use karte hain? (WHY)

Industry me Spring Kafka isliye use hota hai kyunki:
- Boilerplate code kam ho jata hai
- Annotation-based configuration
- Error handling easy
- Retry, DLQ, transactions support
- Spring ecosystem ke saath seamless integration

---

## 3️⃣ Real-World Use Case

### 🛒 E-Commerce Microservices

- Order Service → Kafka Producer
- Payment Service → Kafka Consumer
- Notification Service → Kafka Consumer

Event: `OrderCreatedEvent`

Kafka se services **loosely coupled** ho jaati hain.

---

## 4️⃣ Maven Dependencies (pom.xml)

```xml
<!-- Spring Kafka Dependency -->
<!-- Purpose: Spring Boot ke saath Kafka integrate karna -->
<!-- When to use: Jab Spring Boot application me Kafka chahiye -->
<dependency>
    <groupId>org.springframework.kafka</groupId>
    <artifactId>spring-kafka</artifactId>
</dependency>
```

---

## 5️⃣ application.yml Configuration

```yaml
spring:
  kafka:
    bootstrap-servers: localhost:9092  # Kafka broker address
    consumer:
      group-id: order-group              # Consumer group name
      auto-offset-reset: earliest        # Offset policy
      key-deserializer: org.apache.kafka.common.serialization.StringDeserializer
      value-deserializer: org.apache.kafka.common.serialization.StringDeserializer
    producer:
      key-serializer: org.apache.kafka.common.serialization.StringSerializer
      value-serializer: org.apache.kafka.common.serialization.StringSerializer
```

---

## 6️⃣ Kafka Producer using Spring Boot

```java
package com.example.kafka.producer;

import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.stereotype.Service;

// @Service
// Purpose: Is class ko Spring-managed service banana
// When to use: Business logic ya integration logic ke liye
// Why here: Kafka producer ek service layer ka part hai
@Service
public class OrderProducer {

    private final KafkaTemplate<String, String> kafkaTemplate;

    // Constructor Injection
    // Purpose: KafkaTemplate ka dependency inject karna
    public OrderProducer(KafkaTemplate<String, String> kafkaTemplate) {
        this.kafkaTemplate = kafkaTemplate;
    }

    public void sendOrderEvent(String message) {
        kafkaTemplate.send("order-events", message);
    }
}
```

---

## 7️⃣ Kafka Consumer using @KafkaListener

```java
package com.example.kafka.consumer;

import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.stereotype.Service;

// @Service
// Purpose: Kafka consumer ko Spring bean banana
// Why: Taaki Spring lifecycle & dependency injection use ho sake
@Service
public class OrderConsumer {

    // @KafkaListener
    // Purpose: Kafka topic ko listen karna
    // When to use: Jab async message consume karna ho
    // Why here: order-events topic se events receive karne ke liye
    @KafkaListener(topics = "order-events", groupId = "order-group")
    public void consume(String message) {
        System.out.println("Order Event Received: " + message);
    }
}
```

---

## 8️⃣ Flow Diagram (ASCII)

```
[REST API]
     |
     v
[OrderProducer]
     |
     v
 Kafka Topic (order-events)
     |
     v
[OrderConsumer]
```

### Step Explanation:
1. REST API order create karta hai
2. Producer Kafka me event publish karta hai
3. Consumer async event consume karta hai

---

## 9️⃣ Error Handling & Retry (Concept)

Spring Kafka support karta hai:
- Retry mechanisms
- Dead Letter Topics (DLT)
- Custom error handlers

👉 Ye capstone project me implement karenge

---

## 🔟 Interview Ready Points

- Spring Kafka = abstraction over Kafka Java API
- @KafkaListener = async consumer
- KafkaTemplate = producer helper
- Event-driven architecture backbone

---

## 1️⃣1️⃣ Summary

- Spring Kafka industry standard hai
- Microservices ke liye MUST skill
- Next step = real Kafka Capstone Project

---

✅ Topic (d) COMPLETE

❓ **Should I move to next topic?**

🔹 MODULE 4 → Topic (e): Kafka Capstone Project

👉 Sirf **YES** likho.

