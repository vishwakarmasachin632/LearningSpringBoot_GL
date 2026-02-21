# MODULE 4 – APACHE KAFKA
## Topic (c): Java Integration with Kafka

> Language: Hinglish
> JDK: 21 | Build Tool: Maven | IDE: IntelliJ IDEA

---

## 1️⃣ Java + Kafka Integration ka overview

Java integration ka matlab hai **plain Java application** se Kafka ke saath **producer aur consumer** banana — bina Spring Boot ke.

Iska fayda:
- Kafka internals samajh aate hain
- Interview me low-level clarity aati hai
- Debugging easy hoti hai

> 👉 Industry me zyada tar **Spring Kafka** use hota hai, lekin base yahi hai.

---

## 2️⃣ Real-World Use Case

### 📦 Order Processing System

- Order Service → Kafka Producer (OrderCreated event)
- Inventory Service → Kafka Consumer (stock reduce)

Event-driven communication → **loose coupling + scalability**

---

## 3️⃣ Maven Dependencies (pom.xml)

```xml
<!-- Apache Kafka client library -->
<!-- Purpose: Kafka ke saath Java application ko connect karna -->
<!-- When to use: Jab Spring ke bina Kafka use karna ho -->
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-clients</artifactId>
    <version>3.7.0</version>
</dependency>
```

---

## 4️⃣ Kafka Producer – Java Code

```java
package com.example.kafka.producer;

import org.apache.kafka.clients.producer.KafkaProducer;
import org.apache.kafka.clients.producer.ProducerRecord;
import org.apache.kafka.clients.producer.ProducerConfig;
import org.apache.kafka.common.serialization.StringSerializer;

import java.util.Properties;

public class OrderProducer {

    public static void main(String[] args) {

        // Kafka configuration properties
        Properties props = new Properties();

        // Kafka broker address
        // Purpose: Kafka server ka location batata hai
        props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");

        // Key serializer
        // Purpose: Message key ko byte me convert karta hai
        props.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());

        // Value serializer
        // Purpose: Message value ko byte me convert karta hai
        props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());

        // Kafka producer create
        KafkaProducer<String, String> producer = new KafkaProducer<>(props);

        // Record create
        ProducerRecord<String, String> record =
                new ProducerRecord<>("order-events", "order-101", "Order Created");

        // Message send
        producer.send(record);

        System.out.println("Order event sent to Kafka");

        // Resource close
        producer.close();
    }
}
```

---

## 5️⃣ Kafka Consumer – Java Code

```java
package com.example.kafka.consumer;

import org.apache.kafka.clients.consumer.KafkaConsumer;
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.kafka.common.serialization.StringDeserializer;

import java.time.Duration;
import java.util.Collections;
import java.util.Properties;

public class OrderConsumer {

    public static void main(String[] args) {

        Properties props = new Properties();

        // Kafka broker address
        props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");

        // Consumer group id
        // Purpose: Load balancing aur offset tracking
        props.put(ConsumerConfig.GROUP_ID_CONFIG, "order-consumer-group");

        // Key deserializer
        props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());

        // Value deserializer
        props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());

        // Offset reset policy
        // Purpose: Agar offset na mile to starting se read kare
        props.put(ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, "earliest");

        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);

        // Topic subscribe
        consumer.subscribe(Collections.singletonList("order-events"));

        System.out.println("Waiting for messages...");

        // Infinite poll loop
        while (true) {
            ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));

            for (ConsumerRecord<String, String> record : records) {
                System.out.println("Key: " + record.key());
                System.out.println("Value: " + record.value());
                System.out.println("Offset: " + record.offset());
            }
        }
    }
}
```

---

## 6️⃣ Execution Flow (ASCII Diagram)

```
[Java Producer]
      |
      v
  Kafka Broker
      |
      v
[Java Consumer]
```

### Step-by-step Flow:
1. Producer message bhejta hai
2. Kafka broker message store karta hai
3. Consumer poll karke message read karta hai

---

## 7️⃣ Important Configuration Concepts

- bootstrap.servers → Kafka address
- group.id → Consumer coordination
- serializers/deserializers → Data conversion
- poll() → Kafka se data read

---

## 8️⃣ Interview Tips

- Java Kafka = low-level API
- Spring Kafka = abstraction layer
- Consumer group se scalability aati hai
- Offset Kafka nahi, **consumer maintain karta hai**

---

## 9️⃣ Summary

- Java integration se Kafka fundamentals clear hote hain
- Producer + Consumer ka base samajhna mandatory hai
- Next step → Spring Kafka (real industry usage)

---

✅ Topic (c) COMPLETE

❓ **Should I move to next topic?**

🔹 MODULE 4 → Topic (d): Spring Kafka Integration

👉 Sirf **YES** likho.

