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

### Constructor Injection Example:
```java
@Service
public class PaymentService {

    private final PaymentGateway gateway;

    // Spring yahan PaymentGateway inject karega
    public PaymentService(PaymentGateway gateway) {
        this.gateway = gateway;
    }
}
```

### Kyun important hai?
- Loose coupling
- Immutable objects
- Easy unit testing

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

### Problem:
- Logging
- Security
- Transaction

Ye sab har method me likhna padta hai.

### Solution:
Spring AOP cross-cutting concerns ko alag layer me le jata hai.

### Example:
- Logging before method
- Transaction around method

(Detail AOP hum later topic me cover karenge)

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

- IoC vs DI difference
- Why constructor injection is best
- What is Spring Bean
- What is loose coupling

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

