# 📘 Apache Kafka – Complete Course (Beginner to Advanced)

---

## 🔷 What is Apache Kafka?

Apache Kafka is a **distributed event-streaming platform** designed to handle **high-throughput, fault-tolerant, real-time data streams**.

Kafka is widely used for:

* Real-time data pipelines
* Event-driven microservices
* Log aggregation
* Messaging systems
* Streaming analytics

### 🔑 Key Characteristics

* Distributed architecture
* Horizontal scalability
* High availability
* Fault tolerance
* Persistent storage (disk-based)

---

### 🔥 Real-Life Analogy: Railway Parcel System 🚆

Think of Kafka as a **railway parcel delivery system**:

| Kafka Component | Real-Life Meaning       |
| --------------- | ----------------------- |
| Producer        | Person sending parcel   |
| Broker          | Railway station         |
| Topic           | Destination city        |
| Partition       | Multiple railway tracks |
| Consumer        | Person receiving parcel |

This analogy highlights **loose coupling** — sender and receiver do not directly know each other.

---

# 🧩 Module A: Introduction to Apache Kafka

---

## 1️⃣ Why Kafka Was Created?

### ❌ Problems in Traditional Systems

Before Kafka, systems relied on:

* Direct service-to-service communication
* Batch-based data processing
* Centralized databases
* Tight coupling between components

This resulted in:

* Poor scalability
* Slow processing
* High failure impact
* Difficult system evolution

---

### ✅ How Kafka Solves These Problems

Kafka introduces **event-driven architecture**, where:

* Producers publish events
* Consumers independently react to events
* Data is stored durably and replayable

**Benefits:**

* Independent scaling of services
* Real-time processing
* High reliability
* System resilience

---

## 2️⃣ Core Kafka Concepts (Theory)

```
Producer  --->  Topic (Partitioned)  --->  Consumer
```

### 🔹 Producer

* Application that **publishes events** to Kafka
* Completely decoupled from consumers
* Supports asynchronous message delivery

---

### 🔹 Topic

* Logical channel for messages
* Append-only log structure
* Messages are immutable

---

### 🔹 Partition

* A topic is divided into multiple partitions
* Each partition is an ordered, immutable log
* Enables parallelism and scalability
* Ordering is guaranteed **only within a partition**

---

### 🔹 Broker

* Kafka server instance
* Stores partitions
* Handles client read/write requests
* A Kafka cluster consists of multiple brokers

---

### 🔹 Consumer Group

* Logical group of consumers
* Each partition is consumed by only one consumer per group
* Enables load balancing and fault tolerance

---

## 3️⃣ Kafka Architecture (Conceptual View)

```
          Producer
              |
              v
      -----------------
      |   Kafka       |
      |   Broker      |
      | Topic A       |
      |  P0  P1  P2   |
      -----------------
        |    |    |
     Consumer Group
```

### 🧠 Architecture Notes

* Kafka persists data to disk
* Consumers pull data (pull-based model)
* Consumers track their own offsets

---

# 🧩 Module B: Kafka Ecosystem

---

## 1️⃣ Kafka Core Components

| Component         | Description                          |
| ----------------- | ------------------------------------ |
| Kafka Broker      | Stores and serves data               |
| ZooKeeper / KRaft | Manages metadata and leader election |
| Kafka Connect     | Integrates external systems          |
| Kafka Streams     | Stream processing library            |
| Schema Registry   | Manages message schemas              |

---

## 2️⃣ Kafka Connect (Theory)

Kafka Connect is used for **data integration** between Kafka and external systems without writing custom code.

### Common Use Cases

* Database → Kafka
* Kafka → Search engine
* Kafka → Data warehouse

```
MySQL → Kafka Connect → Kafka → Elasticsearch
```

### 🧠 Why Kafka Connect?

* Zero-code integration
* Scalable and fault tolerant
* Connector-based architecture

---

## 3️⃣ Kafka Streams (Theory)

Kafka Streams is a **Java client library**, not a separate server.

Used for:

* Filtering events
* Aggregation
* Joins
* Transformations

```
Order Events → Filter FAILED Orders → Notify
```

---

# 🧩 Module C: Kafka Integration with Java

---

## Why Use Kafka with Java?

* Kafka is written in Java
* Native and efficient client APIs
* Full control over producers and consumers
* High performance and reliability

---

## 1️⃣ Kafka Producer (Java)

```java
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

KafkaProducer<String, String> producer =
        new KafkaProducer<>(props);

producer.send(new ProducerRecord<>("order-topic", "Order Created"));
producer.close();
```

### 🧠 Theory

* Producer sends messages asynchronously
* Serialization converts objects to bytes
* `bootstrap.servers` is used for initial broker discovery

---

## 2️⃣ Kafka Consumer (Java)

```java
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("group.id", "order-group");
props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");

KafkaConsumer<String, String> consumer =
        new KafkaConsumer<>(props);

consumer.subscribe(Arrays.asList("order-topic"));

while (true) {
    ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
    for (ConsumerRecord<String, String> record : records) {
        System.out.println(record.value());
    }
}
```

### 🧠 Theory

* Consumers pull data from Kafka
* Offset tracks consumption progress
* Consumers are stateful

---

# 🧩 Module D: Kafka Integration with Spring Boot

---

## Why Spring Kafka?

* Simplifies Kafka configuration
* Reduces boilerplate code
* Production-ready abstractions
* Seamless microservices integration

---

## 1️⃣ Maven Dependency

```xml
<dependency>
  <groupId>org.springframework.kafka</groupId>
  <artifactId>spring-kafka</artifactId>
</dependency>
```

---

## 2️⃣ Kafka Producer (Spring Boot)

```java
@Service
public class OrderProducer {

    @Autowired
    private KafkaTemplate<String, String> kafkaTemplate;

    public void sendOrder(String order) {
        kafkaTemplate.send("order-topic", order);
    }
}
```

### 🧠 Theory

* `KafkaTemplate` is a high-level abstraction
* Manages retries, serialization, and producer lifecycle

---

## 3️⃣ Kafka Consumer (Spring Boot)

```java
@Service
public class OrderConsumer {

    @KafkaListener(topics = "order-topic", groupId = "order-group")
    public void consume(String message) {
        System.out.println("Order Received: " + message);
    }
}
```

### 🧠 Theory

* `@KafkaListener` handles polling automatically
* Offset commits can be auto or manual

---

## 4️⃣ application.yml

```yaml
spring:
  kafka:
    bootstrap-servers: localhost:9092
    consumer:
      group-id: order-group
```

---

# 🧩 Module E: Capstone Project

---

## 🎯 Project: Online Order Processing System

### 🔥 Business Use Case

* Asynchronous communication
* Decoupled microservices
* High scalability
* Fault tolerance

---

## 🏗 Architecture (Event-Driven)

```
Order Service → Kafka → Inventory Service
                     → Notification Service
```

### 🧠 Design Explanation

* Order service publishes events
* Inventory and Notification services react independently
* Kafka acts as the event backbone

---

## Order Producer (Order Service)

```java
@RestController
public class OrderController {

    @Autowired
    private KafkaTemplate<String, String> kafkaTemplate;

    @PostMapping("/order")
    public String placeOrder(@RequestBody String order) {
        kafkaTemplate.send("order-topic", order);
        return "Order Placed";
    }
}
```

---

## Inventory Consumer

```java
@KafkaListener(topics = "order-topic", groupId = "inventory-group")
public void updateInventory(String order) {
    System.out.println("Inventory updated for: " + order);
}
```

---

## Notification Consumer

```java
@KafkaListener(topics = "order-topic", groupId = "notification-group")
public void sendNotification(String order) {
    System.out.println("Notification sent for: " + order);
}
```

---

# 🧩 Module F:  MCQ Assessment
# 📘 Apache Kafka – Interview MCQ Assessment (Beginner to Advanced)

---

## 📌 Instructions

* Each question has **4 options**
* Correct answer is marked with **✅**
* Explanation is provided for interview clarity

---

## 🧩 Section 1: Kafka Basics (Beginner)

### 1️⃣ What is Apache Kafka?

A. Traditional Database
B. Message Queue only
C. Distributed Event Streaming Platform
D. Web Server

✅ **Correct Answer:** C
**Explanation:** Kafka is designed to publish, store, and process event streams in real time.

---

### 2️⃣ Kafka stores messages in which structure?

A. Queue
B. Table
C. Topic
D. File System

✅ **Correct Answer:** C
**Explanation:** Topics are logical categories where Kafka stores messages.

---

### 3️⃣ Which component sends data to Kafka?

A. Broker
B. Consumer
C. Producer
D. Zookeeper

✅ **Correct Answer:** C
**Explanation:** Producers publish messages to Kafka topics.

---

### 4️⃣ Kafka guarantees message ordering at which level?

A. Across all topics
B. Across all partitions
C. Within a partition
D. Across the cluster

✅ **Correct Answer:** C
**Explanation:** Ordering is guaranteed only within a single partition.

---

### 5️⃣ What is a Kafka Broker?

A. Message Sender
B. Message Receiver
C. Kafka Server Instance
D. Load Balancer

✅ **Correct Answer:** C
**Explanation:** A broker is a Kafka server that stores and serves data.

---

## 🧩 Section 2: Kafka Architecture & Internals (Intermediate)

### 6️⃣ What is the purpose of partitions in Kafka?

A. Security
B. Parallelism & Scalability
C. Encryption
D. Compression

✅ **Correct Answer:** B
**Explanation:** Partitions allow Kafka to scale horizontally and process data in parallel.

---

### 7️⃣ What does Kafka use to track message position?

A. Index
B. Timestamp
C. Offset
D. Key

✅ **Correct Answer:** C
**Explanation:** Offset uniquely identifies a message's position in a partition.

---

### 8️⃣ What is a Consumer Group?

A. Multiple producers sending data
B. Multiple consumers sharing load
C. Multiple brokers in cluster
D. Multiple topics combined

✅ **Correct Answer:** B
**Explanation:** Consumer groups ensure load balancing and fault tolerance.

---

### 9️⃣ Which Kafka feature provides fault tolerance?

A. Compression
B. Replication
C. Partitioning
D. Serialization

✅ **Correct Answer:** B
**Explanation:** Replication ensures data is copied across brokers.

---

### 🔟 What happens if a consumer fails?

A. Messages are lost
B. Topic is deleted
C. Another consumer takes over
D. Producer stops

✅ **Correct Answer:** C
**Explanation:** Kafka rebalances partitions among remaining consumers.

---

## 🧩 Section 3: Kafka with Java & Spring (Intermediate)

### 1️⃣1️⃣ Which Java API is used to send messages?

A. KafkaConsumer
B. KafkaBroker
C. KafkaProducer
D. KafkaClient

✅ **Correct Answer:** C
**Explanation:** `KafkaProducer` is the official Kafka client API used to publish records to Kafka topics.

---

### 1️⃣2️⃣ Which annotation is used to consume messages in Spring Kafka?

A. @Listener
B. @EventListener
C. @KafkaListener
D. @Consumer

✅ **Correct Answer:** C
**Explanation:** `@KafkaListener` tells Spring to subscribe a method to a Kafka topic and consume messages.

---

### 1️⃣3️⃣ KafkaTemplate is used for?

A. Consuming messages
B. Topic creation
C. Producing messages
D. Broker configuration

✅ **Correct Answer:** C
**Explanation:** `KafkaTemplate` is a high-level Spring abstraction used to send messages to Kafka.

---

### 1️⃣4️⃣ Which property defines Kafka server address?

A. kafka.url
B. broker.url
C. bootstrap.servers
D. kafka.server

✅ **Correct Answer:** C
**Explanation:** `bootstrap.servers` provides the initial list of Kafka brokers for client connection.

---

### 1️⃣5️⃣ group.id is used for?

A. Producer grouping
B. Broker grouping
C. Consumer grouping
D. Topic grouping

✅ **Correct Answer:** C
**Explanation:** `group.id` identifies a consumer group so Kafka can distribute partitions among consumers.

---

### 1️⃣2️⃣ Which annotation is used to consume messages in Spring Kafka?

A. @Listener
B. @EventListener
C. @KafkaListener
D. @Consumer

✅ **Correct Answer:** C

---

### 1️⃣3️⃣ KafkaTemplate is used for?

A. Consuming messages
B. Topic creation
C. Producing messages
D. Broker configuration

✅ **Correct Answer:** C

---

### 1️⃣4️⃣ Which property defines Kafka server address?

A. kafka.url
B. broker.url
C. bootstrap.servers
D. kafka.server

✅ **Correct Answer:** C

---

### 1️⃣5️⃣ group.id is used for?

A. Producer grouping
B. Broker grouping
C. Consumer grouping
D. Topic grouping

✅ **Correct Answer:** C

---

## 🧩 Section 4: Advanced & Scenario-Based (Advanced)

### 1️⃣6️⃣ Kafka follows which architecture style?

A. Monolithic
B. Layered
C. Event-Driven
D. Client-Server

✅ **Correct Answer:** C
**Explanation:** Kafka is based on event-driven architecture where producers publish events and consumers react to them.

---

### 1️⃣7️⃣ What happens if replication factor is 3?

A. Data stored in 3 topics
B. Data stored on 3 brokers
C. Data stored 3 times in same broker
D. Data is encrypted

✅ **Correct Answer:** B
**Explanation:** Replication factor 3 means each partition has one leader and two replicas on different brokers.

---

### 1️⃣8️⃣ Which Kafka component is used for stream processing?

A. Kafka Connect
B. Kafka Streams
C. Zookeeper
D. Schema Registry

✅ **Correct Answer:** B
**Explanation:** Kafka Streams is a client library used to process and transform streaming data.

---

### 1️⃣9️⃣ Kafka is best suited for?

A. CRUD applications
B. Batch processing only
C. Real-time data pipelines
D. Authentication systems

✅ **Correct Answer:** C
**Explanation:** Kafka is designed for high-throughput, low-latency real-time data streaming.

---

### 2️⃣0️⃣ Exactly-once semantics is achieved using?

A. Offsets only
B. Transactions
C. Replication
D. Compression

✅ **Correct Answer:** B
**Explanation:** Kafka transactions ensure messages are processed exactly once, even during failures.

---

### 1️⃣7️⃣ What happens if replication factor is 3?

A. Data stored in 3 topics
B. Data stored on 3 brokers
C. Data stored 3 times in same broker
D. Data is encrypted

✅ **Correct Answer:** B

---

### 1️⃣8️⃣ Which Kafka component is used for stream processing?

A. Kafka Connect
B. Kafka Streams
C. Zookeeper
D. Schema Registry

✅ **Correct Answer:** B

---

### 1️⃣9️⃣ Kafka is best suited for?

A. CRUD applications
B. Batch processing only
C. Real-time data pipelines
D. Authentication systems

✅ **Correct Answer:** C

---

### 2️⃣0️⃣ Exactly-once semantics is achieved using?

A. Offsets only
B. Transactions
C. Replication
D. Compression

✅ **Correct Answer:** B

---

## 🧩 Section 5: Additional Interview MCQs

### 2️⃣1️⃣ What happens when a topic has more consumers than partitions?

A. Messages are duplicated
B. Extra consumers remain idle
C. Kafka creates new partitions
D. Broker crashes

✅ **Correct Answer:** B
**Explanation:** A partition can be consumed by only one consumer in a group.

---

### 2️⃣2️⃣ Which configuration controls message retention?

A. retention.ms / retention.bytes
B. cleanup.policy
C. segment.bytes
D. log.dir

✅ **Correct Answer:** A

---

### 2️⃣3️⃣ cleanup.policy=compact means?

A. Delete messages by time
B. Delete messages by size
C. Keep latest value per key
D. Compress messages

✅ **Correct Answer:** C

---

### 2️⃣4️⃣ Which serializer is used for String messages?

A. StringEncoder
B. StringSerializer
C. JsonSerializer
D. ByteSerializer

✅ **Correct Answer:** B

---

### 2️⃣5️⃣ What causes consumer rebalancing?

A. Producer restart
B. New topic creation
C. Consumer join/leave
D. Message failure

✅ **Correct Answer:** C

---

### 2️⃣6️⃣ Which Kafka API supports exactly-once processing?

A. Kafka Consumer API
B. Kafka Producer API
C. Kafka Transactions API
D. Kafka Connect API

✅ **Correct Answer:** C

---

### 2️⃣7️⃣ What is the role of Schema Registry?

A. Store messages
B. Manage brokers
C. Store and validate schemas
D. Monitor consumers

✅ **Correct Answer:** C

---

### 2️⃣8️⃣ Kafka Connect is mainly used for?

A. Stream processing
B. Data integration
C. Monitoring
D. Security

✅ **Correct Answer:** B

---

### 2️⃣9️⃣ Which command creates a topic?

A. kafka-topic-create.sh
B. kafka-topics.sh
C. kafka-create-topic.sh
D. kafka-admin.sh

✅ **Correct Answer:** B

---

### 3️⃣0️⃣ Kafka is horizontally scalable because of?

A. Replication
B. Partitions
C. Offsets
D. Brokers

✅ **Correct Answer:** B

---

## 🧠 Final Notes (Interview Tip)

* Focus on **Partitions, Offsets, Consumer Groups**
* Understand **Rebalancing & Replication** clearly
* Be ready with **real-world Kafka use cases**

---

## 🎯 Course Completion Outcome

After completing this course, you will be able to:

* Design event-driven architectures
* Use Kafka with Java and Spring Boot
* Build scalable, fault-tolerant systems
* Explain Kafka internals confidently in interviews
* Implement real-world Kafka-based solutions

---

✅ **End of Apache Kafka Complete Course**
