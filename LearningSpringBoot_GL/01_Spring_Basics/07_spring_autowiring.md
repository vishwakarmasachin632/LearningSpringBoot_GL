# 📘 MODULE 1 – SPRING BASICS
## 🔹 Topic (g): Spring Auto-Wiring

---

## 🧠 1. Spring Auto-Wiring kya hota hai?

Spring Auto-Wiring ka matlab hai:
> **Spring automatically decide karta hai ki kaunsi dependency kis bean me inject karni hai**

Developer ko:
- `new` keyword use nahi karna padta
- Manually dependency set nahi karni padti

👉 Spring container smartly dependency resolve karta hai.

---

## ❌ 2. Without Auto-Wiring (Manual Wiring)

```java
@Configuration
public class AppConfig {

    @Bean
    public OrderService orderService() {
        return new OrderService(paymentService());
    }

    @Bean
    public PaymentService paymentService() {
        return new PaymentService();
    }
}
```

👉 Ye kaam karta hai, lekin **manual** hai.

---

## ✅ 3. With Auto-Wiring (Spring Way)

Spring khud decide karega kaunsa bean inject karna hai.

```java
@Service
public class OrderService {

    private final PaymentService paymentService;

    // Spring automatically PaymentService inject karega
    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

---

## 🧩 4. Auto-Wiring ke Types

Spring auto-wiring ko **4 ways** me karta hai:

1. By Type (Most Common ✅)
2. By Name
3. By Constructor
4. By @Qualifier

---

## 🥇 5. Auto-Wiring by Type (Default)

Spring type match karta hai.

```java
@Service
public class BillingService {

    private final PaymentGateway gateway;

    public BillingService(PaymentGateway gateway) {
        this.gateway = gateway;
    }
}
```

👉 Agar sirf **ek PaymentGateway bean** hai → No issue.

---

## ⚠️ 6. Problem: Multiple Beans of Same Type

```java
@Component
public class PaypalGateway implements PaymentGateway {}

@Component
public class StripeGateway implements PaymentGateway {}
```

❌ Error aayega:
```
NoUniqueBeanDefinitionException
```

---

## 🏷️ 7. @Primary Annotation

### Purpose:
- Default bean select karna

### Kab use kare?
- Jab multiple beans ho aur ek ko default banana ho

```java
@Primary
@Component
public class PaypalGateway implements PaymentGateway {}
```

👉 Spring PaypalGateway ko choose karega.

---

## 🎯 8. @Qualifier Annotation

### Purpose:
- Exact bean specify karna

### Kab use kare?
- Jab specific implementation chahiye

```java
@Service
public class BillingService {

    private final PaymentGateway gateway;

    public BillingService(@Qualifier("stripeGateway") PaymentGateway gateway) {
        this.gateway = gateway;
    }
}
```

👉 Spring sirf `stripeGateway` inject karega.

---

## 🔁 9. @Autowired Annotation (Revisit)

### Purpose:
- Dependency inject karna

### Important Points:
- Constructor injection me optional
- Field / Setter me required

```java
@Autowired
private PaymentService paymentService;
```

---

## 🔄 10. Auto-Wiring Resolution Flow

```
Spring Container
      |
      |-- Find Dependency Type
      |-- Check @Primary
      |-- Check @Qualifier
      |
      v
Inject Bean
```

---

## 🌍 11. Real World Use Case

### Payment System

- Multiple gateways (UPI, Card, Wallet)
- @Qualifier se specific gateway choose

👉 Clean & flexible architecture

---

## ⚠️ 12. Common Mistakes

- Multiple beans without @Qualifier
- Field injection ka overuse
- Bean name mismatch

---

## 🎯 13. Interview Focus

- @Autowired vs @Qualifier
- @Primary ka role
- Multiple beans handling

---

## ✅ 14. Summary

- Auto-wiring dependency injection ka smart version
- By Type default hota hai
- @Primary default choose karta hai
- @Qualifier exact control deta hai

---

## ⏭️ Next Topic

🔹 **Module 1 – Topic (h): Getting Started with Spring Boot**

❓ Should I move to the next topic?
👉 YES / NO likho

