# 24) REST using Spring Boot

> **Module:** 3 (Spring REST)  
> **Topic:** REST using Spring Boot  
> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Framework:** Spring Boot (Latest Stable)  
> **Build Tool:** Maven  
> **Database:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ REST kya hota hai? (Theory)

REST ka full form hota hai **Representational State Transfer**.

Simple shabdon me:
> REST ek **architecture style** hai jiske through **client (frontend / app)** aur **server (backend)** HTTP ke through baat karte hain.

REST koi framework nahi hai ❌  
REST ek **rule / guideline set** hai ✅

---

## 2️⃣ Real-World Example (Relatable)

### Zomato / Swiggy Scenario

- Mobile App → order place karta hai
- Backend API → order receive karta hai
- Database → order save hota hai

Ye poora flow **REST APIs** ke through hota hai.

---

## 3️⃣ REST ke Core Principles

### 🔹 1. Client–Server
- Client aur server separate hote hain
- UI aur business logic alag

### 🔹 2. Stateless
- Server client ka state remember nahi karta
- Har request me complete data aata hai

### 🔹 3. Uniform Interface
- Standard HTTP methods use hote hain

---

## 4️⃣ HTTP Methods (VERY IMPORTANT)

| Method | Use Case |
|------|--------|
| GET | Data read |
| POST | New data create |
| PUT | Full update |
| PATCH | Partial update |
| DELETE | Data delete |

---

## 5️⃣ Spring Boot REST kyun use karte hain?

Without Spring Boot:
❌ Bohot configuration
❌ Manual JSON handling

With Spring Boot:
✅ Auto configuration
✅ JSON auto convert (Jackson)
✅ Easy annotations

---

## 6️⃣ @RestController Annotation

```java
@RestController
// Purpose: Class ko REST controller banana
// When: JSON/XML response chahiye
// Why: @Controller + @ResponseBody combine karta hai
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello Spring REST";
    }
}
```

---

## 7️⃣ @GetMapping Annotation

```java
@GetMapping("/hello")
// Purpose: HTTP GET request handle karna
// When: Data fetch karna ho
// Why: REST standard follow karne ke liye
```

---

## 8️⃣ JSON Response kaise aata hai?

```java
@GetMapping("/employee")
public Employee getEmployee() {
    return new Employee(1L, "Rahul", "IT");
}
```

Spring Boot automatically object → JSON convert karta hai.

---

## 9️⃣ Flow Diagram (ASCII)

```
Client (Browser / App)
   |
   | HTTP GET /employees
   v
RestController
   |
   v
Service
   |
   v
Repository
   |
   v
PostgreSQL
```

---

## 🔟 REST vs SOAP (Interview Favorite)

| REST | SOAP |
|----|------|
| Lightweight | Heavy |
| JSON | XML |
| Fast | Slow |
| Easy | Complex |

---

## 1️⃣1️⃣ Common Beginner Mistakes

❌ @Controller use karna instead of @RestController
❌ Wrong HTTP method
❌ URL naming galat (verbs use karna)

Correct URL:
```
GET /employees
POST /employees
```

---

## 1️⃣2️⃣ Interview Questions

1. REST kya hota hai?
2. REST stateless kyun hota hai?
3. @RestController vs @Controller
4. GET vs POST difference
5. JSON conversion kaise hoti hai?

---

## ✅ Summary

- REST = architecture style
- Spring Boot REST banana easy
- @RestController core annotation
- HTTP methods ka sahi use

---

### ❓ Next Topic?
**MODULE 3 → Topic (b): Web Services Introduction**

👉 Likho: **YES**

