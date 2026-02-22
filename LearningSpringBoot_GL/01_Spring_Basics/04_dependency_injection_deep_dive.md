# 📘 MODULE 1 – SPRING BASICS
## 🔹 Topic (d): Dependency Injection (Deep Dive)

---

## 🧠 1. Dependency Injection (DI) kya hota hai?

Dependency Injection ka matlab hai:
> **Ek class ko jis object ki zarurat hai, woh object Spring automatically provide kare**

Simple shabdon me:
- Class khud dependency **create nahi karti**
- Spring container dependency **inject** karta hai

👉 Isse code **loose coupled**, **testable** aur **maintainable** banta hai.

---

## ❌ 2. Problem Without Dependency Injection

### Tight Coupling Example:
```java
public class OrderService {
    private PaymentService paymentService = new PaymentService();
}
```

### Problems:
- `OrderService` directly `PaymentService` pe depend hai
- PaymentService change = OrderService modify
- Unit testing mushkil

---

## ✅ 3. With Dependency Injection (Spring Way)

```java
public class OrderService {
    private final PaymentService paymentService;

    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

👉 Ab Spring `PaymentService` inject karega.

---

## 🧩 4. Types of Dependency Injection

Spring mainly **3 types** ka DI support karta hai:

1. Constructor Injection (Best Practice ✅)
2. Setter Injection
3. Field Injection (Avoid in real projects ❌)

---

## 🥇 5. Constructor Injection (Recommended)

### Kyun best hai?
- Immutable objects
- Mandatory dependencies
- Easy unit testing

### Example:
```java
@Service
public class UserService {

    private final UserRepository userRepository;

    // Spring automatically UserRepository inject karega
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
}
```

---

## 🪜 6. Setter Injection

### Kab use hota hai?
- Optional dependency

### Example:
```java
@Service
public class NotificationService {

    private EmailService emailService;

    @Autowired
    public void setEmailService(EmailService emailService) {
        this.emailService = emailService;
    }
}
```

---

## ⚠️ 7. Field Injection (Avoid)

```java
@Service
public class ReportService {

    @Autowired
    private PdfService pdfService;
}
```

### Problems:
- Unit testing hard
- Hidden dependencies
- Reflection use hota hai

👉 Interviews me bolo: **Avoid field injection**

---

## 🧠 8. @Autowired Annotation

### Purpose:
- Spring ko batata hai dependency inject karni hai

### Kab use kare?
- Constructor / Setter / Field

### Note:
- Spring 4.3+ me **single constructor** ho to `@Autowired` optional hai

---

## 🔄 9. Dependency Injection Flow (ASCII Diagram)

```
Application Start
      |
      v
Spring Container
      |
      |-- Scan Components
      |-- Create Beans
      |-- Resolve Dependencies
      |-- Inject Dependencies
      |
      v
Application Ready
```

---

## 🌍 10. Real World Use Case

### E-Commerce Application

- OrderService
- PaymentService
- InventoryService

Spring kya karta hai?
- Services ko inject karta hai
- Implementation easily change hoti hai
- Mock services se testing possible

---

## 🎯 11. Interview Questions Focus

## 🎯 Dependency Injection – Interview Notes

---

## ❓ What is Dependency Injection (DI)?

### ✅ What

**Dependency Injection (DI)** is a technique where **Spring provides required objects (dependencies) to a class instead of the class creating them itself**.

### 👉 In simple words

*A class does not create its dependency; Spring gives it.*

### ✅ Why we use DI

* To achieve **loose coupling**
* To make code **easy to test and maintain**
* To let **Spring manage object creation**

### ✅ When we use DI

* In almost **every Spring / Spring Boot application**
* Whenever one class depends on another class

### 📝 One-liner (Interview)

👉 *Dependency Injection allows Spring to supply required objects to a class automatically.*

---

## ❓ Constructor Injection vs Setter Injection

### 🔹 Constructor Injection

#### What

Dependencies are provided through the **constructor**.

#### Why

* Makes dependencies **mandatory**
* Ensures **object is always in valid state**

#### When

* When dependency is **required** and must not be null

```java
@Component
class Car {
    private final Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

---

### 🔹 Setter Injection

#### What

Dependencies are provided through **setter methods**.

#### Why

* Allows **optional dependencies**
* Dependency can be changed later

#### When

* When dependency is **optional**

```java
@Component
class Car {
    private Engine engine;

    @Autowired
    public void setEngine(Engine engine) {
        this.engine = engine;
    }
}
```

---

### ✅ Comparison Table

| Point        | Constructor Injection | Setter Injection |
| ------------ | --------------------- | ---------------- |
| Dependency   | Mandatory             | Optional         |
| Null safety  | High                  | Low              |
| Immutability | Yes                   | No               |
| Recommended  | ✅ Yes                 | ⚠️ Sometimes     |

---

## ❓ Why Field Injection is Bad?

### What

Dependencies are injected **directly into fields** using `@Autowired`.

### Why it is bad

* ❌ Hard to **unit test**
* ❌ Breaks **encapsulation**
* ❌ Dependencies are **hidden**
* ❌ Cannot make fields `final`

### When it is used

* Only for **quick demos or learning**
* ❌ Avoid in real projects

```java
@Component
class Car {
    @Autowired
    private Engine engine; // Field Injection (Not recommended)
}
```

### 📝 One-liner

👉 *Field injection is bad because it hides dependencies and makes testing difficult.*

---

## ❓ Role of @Autowired

### What

`@Autowired` tells Spring to **automatically inject the required dependency**.

### Why

* Removes need for manual object creation
* Enables **Dependency Injection**

### When

* When Spring needs to inject a bean
* Used with **constructor, setter, or field injection**

```java
@Autowired
private Engine engine;
```

### 📝 One-liner (Interview)

👉 *@Autowired tells Spring to inject the required dependency automatically.*

---


---

## ✅ 12. Summary

- DI = Dependency Spring provide karta hai
- Constructor Injection best practice
- Setter optional dependencies ke liye
- Field injection avoid karo
- DI se loose coupling milti hai

---

## ⏭️ Next Topic

🔹 **Module 1 – Topic (e): Spring Bean Lifecycle and Scope**

❓ Should I move to the next topic?
👉 YES / NO likho

