# 📘 MODULE 1 – SPRING BASICS
## 🔹 Topic (e): Spring Bean Lifecycle and Scope

---

## 🧠 1. Spring Bean Lifecycle kya hota hai?

Spring Bean Lifecycle ka matlab hai:
> **Bean kab create hoti hai, kaise initialize hoti hai, use hoti hai aur kab destroy hoti hai**

Spring container poori lifecycle **automatically manage** karta hai.

---

## 🔄 2. Spring Bean Lifecycle – High Level Steps

```
Spring Container Start
      |
      v
Bean Instantiation (Object Create)
      |
      v
Dependency Injection
      |
      v
Bean Initialization
      |
      v
Bean Ready to Use
      |
      v
Bean Destruction (App Shutdown)
```

---

## 🧩 3. Detailed Bean Lifecycle Steps

1️⃣ **Bean Instantiation**  
- Spring object create karta hai

2️⃣ **Dependency Injection**  
- Required dependencies inject hoti hain

3️⃣ **Aware Interfaces (Optional)**  
- Bean ko context ki info milti hai

4️⃣ **Bean Initialization**  
- Custom init logic execute hota hai

5️⃣ **Bean Ready**  
- Bean business use ke liye ready

6️⃣ **Bean Destruction**  
- Cleanup logic execute hota hai

---

## 🧪 4. Practical Example – Bean Lifecycle

```java
@Component
public class DatabaseConnection {

    public DatabaseConnection() {
        System.out.println("1️⃣ Constructor: Bean Created");
    }

    @PostConstruct
    public void init() {
        System.out.println("2️⃣ @PostConstruct: Bean Initialized");
    }

    @PreDestroy
    public void destroy() {
        System.out.println("3️⃣ @PreDestroy: Bean Destroyed");
    }
}
```

### Output Flow:
- Application start → Constructor
- Dependencies injected
- `@PostConstruct` run
- Application stop → `@PreDestroy`

---

## 🏷️ 5. Important Lifecycle Annotations

### 🔹 @PostConstruct
- Purpose: Bean initialize karne ke baad logic chalana
- Kab use kare: DB connection, cache load

### 🔹 @PreDestroy
- Purpose: Bean destroy hone se pehle cleanup
- Kab use kare: Connection close, resource free

---

## 📦 6. Spring Bean Scope kya hota hai?

Bean Scope define karta hai:
> **Kitni baar bean create hogi aur kahan-kahan use hogi**

---

## 🧩 7. Types of Bean Scope

### 1️⃣ Singleton (Default)
- Sirf **1 object** poori application me

```java
@Component
@Scope("singleton")
public class UserService {}
```

---

### 2️⃣ Prototype
- Har request pe **new object**

```java
@Component
@Scope("prototype")
public class ReportGenerator {}
```

---

### 3️⃣ Request (Web)
- Har HTTP request ke liye new bean

---

### 4️⃣ Session (Web)
- Har HTTP session ke liye new bean

---

### 5️⃣ Application
- Ek bean per application lifecycle

---

## 🔄 8. Bean Scope Flow Diagram

```
Singleton Scope
App Start
   |
   v
One Bean Instance
   |
Used Everywhere
```

```
Prototype Scope
Each Request
   |
   v
New Bean Instance
```

---

## 🌍 9. Real World Use Case

### Banking Application

- UserService → Singleton
- TransactionProcessor → Prototype
- SessionData → Session scope

👉 Correct scope = Better performance

---

## ⚠️ 10. Common Mistakes

- Prototype bean me @PreDestroy expect karna
- Stateful data singleton me rakhna
- Wrong scope selection

---

## 🎯 11. Interview Focus Points

- Bean lifecycle steps
- @PostConstruct vs Constructor
- Singleton vs Prototype
- Default bean scope

---

## ✅ 12. Summary

- Bean lifecycle Spring manage karta hai
- @PostConstruct & @PreDestroy important
- Singleton default scope
- Correct scope performance improve karta hai

---

## ⏭️ Next Topic

🔹 **Module 1 – Topic (f): Spring Configuration**

❓ Should I move to the next topic?
👉 YES / NO likho

