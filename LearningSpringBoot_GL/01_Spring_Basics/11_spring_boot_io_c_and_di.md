# 11) Spring Boot IoC & DI (Inversion of Control & Dependency Injection)

> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Build Tool:** Maven  
> **DB Context:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ IoC (Inversion of Control) kya hota hai? (Theory)
Normally hum Java me **object khud banate** hain using `new` keyword.

```java
PaymentService service = new PaymentService();
```

Is approach me **control developer ke paas** hota hai.

### Inversion of Control ka matlab:
> Object ka control **developer se le kar Spring container ko de dena**.

Simple language me:
- Tum object mat banao
- Spring banayega
- Spring manage karega
- Spring inject karega

👉 Isi ko kehte hain **IoC**.

---

## 2️⃣ DI (Dependency Injection) kya hota hai?
DI ka matlab hai:
> Ek class ko jo objects chahiye (dependencies), wo **Spring automatically provide kare**.

Example:
- Controller ko Service chahiye
- Service ko Repository chahiye

Spring:
- Pehle Repository banata hai
- Phir Service me inject karta hai
- Phir Controller me inject karta hai

👉 Ye process **Dependency Injection** kehlata hai.

---

## 3️⃣ IoC Container kya hota hai?
IoC Container Spring ka **heart** hota hai.

Responsibilities:
- Beans create karna
- Dependencies inject karna
- Bean lifecycle manage karna

### Common Containers:
- `ApplicationContext` (Most used)
- `BeanFactory` (Low level)

---

## 4️⃣ Real-World Use Case
**Scenario: Payment Application**

Without Spring:
- Controller khud Service banata
- Service khud Repository banata
- Tight coupling

With Spring IoC + DI:
- Loose coupling
- Easy testing
- Easy replacement (Mocking)

👉 Industry me **IoC + DI mandatory** hai.

---

## 5️⃣ DI Types in Spring

### 1️⃣ Constructor Injection (BEST PRACTICE)
```java
@Service // Business logic class ko Spring bean banata hai
public class PaymentService {
    public void pay() {
        System.out.println("Payment done");
    }
}

@RestController // REST API controller
public class PaymentController {

    private final PaymentService paymentService;

    // Constructor Injection
    // Spring automatically PaymentService inject karega
    public PaymentController(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

👉 **Recommended by Spring team**.

---

### 2️⃣ Setter Injection
```java
@Service
public class OrderService {
    private PaymentService paymentService;

    // @Autowired setter ke through dependency inject karta hai
    @Autowired
    public void setPaymentService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

Use when:
- Optional dependency ho

---

### 3️⃣ Field Injection (NOT recommended)
```java
@Service
public class InvoiceService {

    // Direct field pe injection
    // Testing me problem aati hai
    @Autowired
    private PaymentService paymentService;
}
```

❌ Avoid in real projects.

---

## 6️⃣ Important Annotations (With WHY)

```java
@Component
// Purpose: Simple Spring bean banana
// Use: Jab generic class ho
// Why here: Spring ko batane ke liye ye class managed hai
```

```java
@Service
// Purpose: Business logic layer
// Use: Service classes ke liye
// Why here: Readability + semantics
```

```java
@Repository
// Purpose: Data access layer
// Use: Repository classes
// Why here: Exception translation
```

```java
@Autowired
// Purpose: Dependency inject karna
// Use: Constructor / Setter
// Why here: Spring ko injection batane ke liye
```

---

## 7️⃣ IoC & DI Flow (ASCII Diagram)
```
Application Start
      |
      v
Spring Boot
      |
      v
IoC Container
      |
      | Scan @Component classes
      v
Create Beans
      |
      | Inject Dependencies
      v
Application Ready
```

### Step Explanation:
1. App start hoti hai
2. Spring beans scan karta hai
3. Objects create karta hai
4. Dependencies inject karta hai
5. App run ke liye ready

---

## 8️⃣ Common Mistakes
❌ `new` keyword ka use
❌ Field Injection
❌ Circular dependency
❌ Multiple beans without `@Qualifier`

---

## 9️⃣ Interview Questions

1. IoC kya hota hai?
2. DI kya hota hai?
3. Constructor injection kyun best hai?
4. `@Autowired` ka role?
5. IoC container kya karta hai?

---

## ✅ Summary
- IoC = control Spring ko dena
- DI = dependency injection process
- Constructor injection best practice
- Loose coupling = maintainable code

---

### ✅ Next Topic?
**MODULE 1 → Topic (l): Aspect Oriented Programming (AOP)**

👉 Likho: **YES**

