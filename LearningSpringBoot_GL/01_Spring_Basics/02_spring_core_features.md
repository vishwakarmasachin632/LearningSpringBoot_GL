# 📘 MODULE 1 – SPRING BASICS
## 🔹 Topic (b): Spring Core Features

---

## 🧠 1. Spring Core Features – Overview

Spring ke **Core Features** woh foundation hote hain jin par poora Spring aur Spring Boot khada hota hai.

Agar ye features samajh aa gaye, to:
- Spring Boot easy lagega
- Interview clear hoga
- Real project me confident feel hoga

---

## 🧩 2. Spring Core ke Main Features

Spring Core mainly in cheezon par focus karta hai:

1. Inversion of Control (IoC)
2. Dependency Injection (DI)
3. Bean Management
4. Loose Coupling
5. Aspect Oriented Programming (AOP) Support
6. Declarative Configuration
7. POJO-based Development

Ab hum **ek-ek feature** ko simple language me samjhenge.

---

## 🔁 3. Inversion of Control (IoC)

### 📌 IoC ka matlab
> Object ka control developer se framework (Spring) ke paas chala jana

### Pehle (Without Spring):
- Developer object banata
- Developer lifecycle control karta

### Ab (With Spring):
- Spring container object banata
- Spring lifecycle manage karta

### Example (Conceptual):
```java
// Without Spring
Engine engine = new Engine();
Car car = new Car(engine);
```

```java
// With Spring
// Spring Engine aur Car dono khud banayega
```

### Fayda:
- Code flexible hota hai
- Implementation easily change hota hai
- Testing easy hoti hai

---

## 💉 4. Dependency Injection (DI)

### 📌 DI kya hai?
> Ek class ko doosri class ki dependency Spring provide karta hai

### DI ke Types:
1. Constructor Injection (Recommended)
2. Setter Injection
3. Field Injection (Avoid in real projects)

# Dependency Injection (DI) Types in Spring

---

## 1. Constructor Injection (Recommended)

* **What:** Dependencies are provided through the class constructor.
* **Why:** Makes dependencies **mandatory**, helps with **immutability**, easier to test.
* **When to use:** For **required dependencies**.

**Example:**

```java
import org.springframework.stereotype.Component;
import org.springframework.beans.factory.annotation.Autowired;

@Component
class Engine {
    public void start() {
        System.out.println("Engine started");
    }
}

@Component
class Car {

    private final Engine engine;

    // Constructor Injection
    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car is driving");
    }
}
```

**Explanation:**

* `Car` cannot exist without an `Engine`.
* Spring automatically injects `Engine` when creating `Car`.

---

## 2. Setter Injection

* **What:** Dependencies are provided through **setter methods**.
* **Why:** Useful for **optional dependencies** or when you need to **change dependency later**.
* **When to use:** For **optional or changeable dependencies**.

**Example:**

```java
import org.springframework.stereotype.Component;
import org.springframework.beans.factory.annotation.Autowired;

@Component
class MusicSystem {
    public void play() {
        System.out.println("Playing music");
    }
}

@Component
class CarWithMusic {

    private MusicSystem musicSystem;

    // Setter Injection
    @Autowired
    public void setMusicSystem(MusicSystem musicSystem) {
        this.musicSystem = musicSystem;
    }

    public void playMusic() {
        if (musicSystem != null) {
            musicSystem.play();
        } else {
            System.out.println("No music system installed");
        }
    }
}
```

**Explanation:**

* `MusicSystem` is optional.
* Spring injects it if available.

---

## 3. Field Injection (Avoid in real projects)

* **What:** Dependencies are injected **directly into fields** using `@Autowired`.
* **Why to avoid:**

  * Hard to **unit test**
  * Breaks **encapsulation**
  * Makes code **less maintainable**

**Example:**

```java
import org.springframework.stereotype.Component;
import org.springframework.beans.factory.annotation.Autowired;

@Component
class CarField {

    @Autowired
    private Engine engine;  // Field Injection

    public void drive() {
        engine.start();
        System.out.println("CarField is driving");
    }
}
```

**Explanation:**

* Works, but **not recommended** for production code.
* You **cannot easily replace Engine** in unit tests without reflection tricks.

---

### ✅ Summary Table

| DI Type               | How it works                      | Use Case                                | Pros / Cons                                                                              |
| --------------------- | --------------------------------- | --------------------------------------- | ---------------------------------------------------------------------------------------- |
| Constructor Injection | Via constructor                   | Required dependencies                   | Pros: Immutable, easy to test, recommended<br>Cons: Can be verbose if many dependencies  |
| Setter Injection      | Via setter methods                | Optional dependencies                   | Pros: Flexible, easy to change dependencies<br>Cons: Mutable, less safe than constructor |
| Field Injection       | Directly on fields (`@Autowired`) | Rarely, mostly for quick tests or demos | Pros: Less code<br>Cons: Hard to test, breaks encapsulation, not recommended             |


---

---

## 🫘 5. Spring Bean

### 📌 Bean kya hota hai?
> Spring container ke dwara banaya gaya object = Bean

### Bean ki responsibility:
- Object creation
- Dependency injection
- Lifecycle management

### Example:
```java
@Component
public class EmailService {
    public void sendMail() {
        System.out.println("Email sent");
    }
}
```

Yahan `EmailService` ek **Spring Bean** ban gaya.

---

## 🔗 6. Loose Coupling

### Tight Coupling (Bad):
```java
public class OrderService {
    private PaymentService paymentService = new PaymentService();
}
```

### Loose Coupling (Spring Way):
```java
public class OrderService {
    private final PaymentService paymentService;

    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

👉 Implementation change karna easy ho jata hai.

---

## ✂️ 7. Aspect Oriented Programming (AOP) Support

# Aspect-Oriented Programming (AOP) in Spring

---

## What is AOP?

**Aspect-Oriented Programming (AOP)** is a programming approach that allows you to **separate common (cross-cutting) concerns** like logging, security, and transactions from the main business logic.

In simple words:
**AOP helps you write common code once and apply it automatically to many places.**

---

## Why do we use AOP?

We use AOP to:

* ❌ Avoid **duplicate code** (same logic written again and again)
* ✅ Keep **business logic clean and readable**
* 🔧 Make the application **easy to maintain and update**
* 🔁 Apply common behavior **across the application automatically**

Without AOP, logging or security code would be repeated in every method.

---

## When do we use AOP?

AOP is used when a functionality is **common to many modules**, such as:

* Logging
* Security / Authorization
* Transaction Management
* Performance Monitoring
* Exception Handling
* Auditing

These are called **cross-cutting concerns**.

---

## Simple Example (Conceptual)

Imagine this code written in many methods:

```java
System.out.println("Method execution started");
```

With AOP:

* You write this code **only once**
* Spring automatically runs it **before or after required methods**

Your business code stays clean.

---

## One-Line Summary

> **AOP allows applying common features like logging and security across the application without modifying business code.**

---

## Where AOP fits in Spring?

* Spring AOP is **proxy-based**
* Works mainly with **methods**
* Commonly used internally by Spring for:

  * `@Transactional`
  * Security checks
  * Logging


---

## 🧾 8. Declarative Configuration

Spring me configuration likhne ke tareeke:

1. XML (Old)
2. Java Annotations (Most Used)
3. Java Config Classes

### Example:
```java
@Configuration
public class AppConfig {

    @Bean
    public PaymentService paymentService() {
        return new PaymentService();
    }
}
```

👉 Ab XML ki need nahi.

---

## 🧱 9. POJO-based Development

### POJO ka matlab:
> Plain Old Java Object (No special inheritance required)

Spring force nahi karta:
- Extend any class
- Implement any interface

### Fayda:
- Simple Java code
- Easy testing
- Framework independent

---

## 🌍 10. Real World Use Case

### E-Commerce Application

- OrderService
- PaymentService
- NotificationService

Spring kya karta hai?
- Services ko inject karta hai
- Dependencies manage karta hai
- Application scalable banata hai

---

## 🔄 11. Spring Core Flow

```
Application Start
      |
      v
Spring Container
      |
      |-- Scan Classes
      |-- Create Beans
      |-- Inject Dependencies
      |
      v
Application Ready
```

---

## 🎯 12. Interview Notes

---

## 🔹 IoC vs DI Difference

| Point        | IoC (Inversion of Control)                           | DI (Dependency Injection)              |
| ------------ | ---------------------------------------------------- | -------------------------------------- |
| What it is   | A **design principle**                               | A **design pattern / technique**       |
| Meaning      | Control of object creation is given to the framework | Dependencies are injected into a class |
| Focus        | **Who controls object creation**                     | **How dependencies are provided**      |
| Role         | High-level concept                                   | Practical implementation of IoC        |
| How it works | Framework manages objects                            | Framework injects required objects     |
| Used by      | Spring container                                     | Spring container                       |
| Example idea | “Spring creates objects”                             | “Spring passes objects to classes”     |

---

### ✅ Simple Explanation

**IoC says:**
👉 *“Don’t create objects yourself, let Spring do it.”*

**DI says:**
👉 *“Spring will give you the objects you need.”*

---

### 🔑 Relationship (Very Important for Interviews)

> **DI is a way to achieve IoC**

So:

* **IoC = Concept**
* **DI = Implementation of that concept**

---

## 🔹 Why Constructor Injection Is Best

**Constructor Injection is best because:**

* Dependencies are **mandatory** (object can’t be created without them)
* Makes code **immutable and safe**
* **Easy to test** (dependencies can be passed manually)
* Prevents **NullPointerException**
* Recommended by **Spring best practices**

**One-liner:**
👉 *Constructor injection makes dependencies required, safe, and easy to test.*

---

## 🔹 What Is Spring Bean

**Spring Bean** is an object that is **created, managed, and controlled by the Spring container**.

### In simple words:

👉 *Any object whose lifecycle is managed by Spring is called a Spring Bean.*

### Example idea:

When you annotate a class with `@Component`, `@Service`, or `@Bean`, Spring creates its object — that object is a **Spring Bean**.

**One-liner (for exams/interviews):**
👉 *A Spring Bean is an object managed by the Spring IoC container.*

---

## 🔹 What Is Loose Coupling

**Loose coupling** means **classes depend as little as possible on each other**.

### In simple words:

👉 *One class does not care about the exact implementation of another class.*

### Why it is important:

* Easy to **change or replace** code
* Easy to **test and maintain**
* Makes applications **flexible and scalable**

### Example idea:

If a class depends on an **interface** instead of a concrete class, it is loosely coupled.

**One-liner:**
👉 *Loose coupling allows changing one class without affecting others.*

---


## ✅ 13. Summary

- Spring Core = Foundation
- IoC & DI sabse important
- Bean management Spring karta hai
- Loose coupling se maintainable code
- AOP cross-cutting problems solve karta hai

---

## ⏭️ Next Topic

🔹 **Module 1 – Topic (c): Spring Context**

❓ Should I move to the next topic?
👉 YES / NO likho

