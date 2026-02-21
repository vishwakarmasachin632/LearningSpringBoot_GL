# MODULE 4 – APACHE KAFKA
## Topic (e): Kafka Capstone Project (Industry Ready)

> Language: Hinglish
> JDK: 21 | Spring Boot: Latest | Maven | IntelliJ IDEA
> Database: PostgreSQL

---

## 1️⃣ Project Overview

### 🎯 Project Name: **Order Event Processing System**

Ye project ek **real-world microservice-style Kafka implementation** hai jahan:
- Order create hota hai (REST API)
- Kafka event publish hota hai
- Multiple consumers async process karte hain

Industry me ye pattern:
> E-commerce, Banking, Logistics, Notification systems

---

## 2️⃣ Real-World Business Scenario

🛒 **E-Commerce Platform**

Flow:
1. User order place karta hai
2. Order Service → Kafka Producer
3. Kafka Topic → `order-events`
4. Consumers:
   - Payment Service
   - Inventory Service
   - Notification Service

👉 Loose coupling + high scalability

---

## 3️⃣ Project Architecture

```
Controller
   ↓
Service (Business Logic)
   ↓
Kafka Producer  ─────▶ Kafka Topic ◀───── Kafka Consumer(s)
                                    ↓
                               Processing / DB / Logs
```

---

## 4️⃣ Folder Structure (Industry Standard)

```
kafka-capstone
│
├── controller
│   └── OrderController.java
├── service
│   ├── OrderService.java
│   └── OrderEventProducer.java
├── consumer
│   └── OrderEventConsumer.java
├── model
│   └── OrderEvent.java
├── config
│   └── KafkaConfig.java
├── exception
│   ├── GlobalExceptionHandler.java
│   └── OrderNotFoundException.java
└── KafkaCapstoneApplication.java
```

---

## 5️⃣ Order Event Model

```java
package com.example.kafka.model;

// Simple POJO representing Kafka message
public class OrderEvent {
    private Long orderId;
    private String status;

    // getters & setters
}
```

---

## 6️⃣ Kafka Producer Service

```java
package com.example.kafka.service;

import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.stereotype.Service;

// @Service
// Purpose: Producer ko Spring bean banana
// Why: Kafka publishing business logic ka part hai
@Service
public class OrderEventProducer {

    private final KafkaTemplate<String, OrderEvent> kafkaTemplate;

    public OrderEventProducer(KafkaTemplate<String, OrderEvent> kafkaTemplate) {
        this.kafkaTemplate = kafkaTemplate;
    }

    public void publishOrderEvent(OrderEvent event) {
        kafkaTemplate.send("order-events", event);
    }
}
```

---

## 7️⃣ REST Controller

```java
package com.example.kafka.controller;

import com.example.kafka.model.OrderEvent;
import com.example.kafka.service.OrderEventProducer;
import org.springframework.web.bind.annotation.*;

// @RestController
// Purpose: REST APIs expose karna
// Why: Order create karne ke liye entry point
@RestController
@RequestMapping("/orders")
public class OrderController {

    private final OrderEventProducer producer;

    public OrderController(OrderEventProducer producer) {
        this.producer = producer;
    }

    @PostMapping
    public String createOrder(@RequestBody OrderEvent event) {
        producer.publishOrderEvent(event);
        return "Order Event Published";
    }
}
```

---

## 8️⃣ Kafka Consumer

```java
package com.example.kafka.consumer;

import com.example.kafka.model.OrderEvent;
import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.stereotype.Service;

// @Service
// Purpose: Kafka consumer ko Spring bean banana
@Service
public class OrderEventConsumer {

    // @KafkaListener
    // Purpose: Kafka topic se messages listen karna
    @KafkaListener(topics = "order-events", groupId = "order-group")
    public void consume(OrderEvent event) {
        System.out.println("Processing Order: " + event.getOrderId());
    }
}
```

---

## 9️⃣ Kafka Configuration (Serializer)

```java
package com.example.kafka.config;

import org.springframework.context.annotation.Configuration;

// @Configuration
// Purpose: Kafka related beans define karna
@Configuration
public class KafkaConfig {
    // Serializer / Deserializer beans (conceptual)
}
```

---

## 🔟 Global Exception Handling

```java
package com.example.kafka.exception;

import org.springframework.web.bind.annotation.*;

// @ControllerAdvice
// Purpose: Centralized exception handling
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public String handleException(Exception ex) {
        return ex.getMessage();
    }
}
```

---

## 1️⃣1️⃣ Flow Diagram (ASCII)

```
Client
  ↓
REST Controller
  ↓
Kafka Producer
  ↓
Kafka Topic
  ↓
Kafka Consumer
```

---

## 1️⃣2️⃣ Logging (Concept)

- SLF4J + Logback
- Kafka events log karna
- Consumer processing logs

---

## 1️⃣3️⃣ Resume Ready Points

- Implemented event-driven architecture using Spring Kafka
- Built async producer-consumer flow
- Designed scalable Kafka-based microservice

---

## 1️⃣4️⃣ Summary

- Ye complete **industry-grade Kafka project** hai
- Spring Kafka ka real usage samajh aata hai
- Next = assessment (MCQs)

---

✅ Topic (e) COMPLETE

❓ **Should I move to next topic?**

🔹 MODULE 4 → Topic (f): Kafka Assessment (MIN 30 MCQs)

👉 Sirf **YES** likho.

