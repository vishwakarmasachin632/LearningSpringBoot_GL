# 25) Web Services – Introduction

> **Module:** 3 (Spring REST)  
> **Topic:** Web Services Introduction  
> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Framework:** Spring Boot (Latest Stable)  
> **Build Tool:** Maven  
> **Database:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ Web Service kya hota hai? (Theory)

Web Service ek **software component** hota hai jo **network (internet / intranet)** ke through
**machine-to-machine communication** karta hai.

Simple shabdon me:
> Ek application doosri application se **HTTP ke through data exchange** kare → use Web Service kehte hain.

Human UI ki zarurat nahi hoti ❌  
System-to-system communication hota hai ✅

---

## 2️⃣ Real-World Example (Industry Scenario)

### 🏦 Banking System
- ATM Machine → Bank Server
- Payment Gateway → Merchant Server
- IRCTC → Payment Provider

👉 Ye sab **Web Services** ke through baat karte hain.

---

## 3️⃣ Web Services ke Types

### 🔹 1. SOAP Web Services
- XML based
- Strict standards
- Heavy & complex

### 🔹 2. RESTful Web Services
- Lightweight
- JSON based
- Fast & scalable

👉 Aaj ke time me **90%+ industry REST use karti hai**.

---

## 4️⃣ SOAP vs REST (VERY IMPORTANT)

| SOAP | REST |
|-----|------|
| XML only | JSON / XML |
| Heavy | Lightweight |
| WSDL required | No WSDL |
| Slow | Fast |
| Complex | Easy |

---

## 5️⃣ Web Service ka Basic Flow

```
Client System
   |
   | HTTP Request
   v
Web Service (API)
   |
   v
Business Logic
   |
   v
Database
```

---

## 6️⃣ Spring Boot me Web Services kyun?

Without Spring Boot:
❌ Too much configuration
❌ Manual parsing

With Spring Boot:
✅ Auto config
✅ Easy REST APIs
✅ JSON auto handling

---

## 7️⃣ RESTful Web Service Example

```java
@RestController
// Purpose: REST based web service expose karna
// When: Client ko JSON response dena ho
// Why: @Controller + @ResponseBody ka combo
public class StatusController {

    @GetMapping("/status")
    // Purpose: HTTP GET request handle
    // When: Read-only info chahiye
    // Why: REST standard follow karne ke liye
    public String status() {
        return "Service is running";
    }
}
```

---

## 8️⃣ Data Format (JSON Example)

```json
{
  "service": "payment",
  "status": "UP"
}
```

JSON kyun?
- Lightweight
- Language independent
- Easy to parse

---

## 9️⃣ Web Services me HTTP Codes

| Code | Meaning |
|-----|--------|
| 200 | OK |
| 201 | Created |
| 400 | Bad Request |
| 404 | Not Found |
| 500 | Server Error |

---

## 🔟 Common Beginner Confusions

❓ REST vs Web Service same?
👉 REST **ek type** ka Web Service hai

❓ API vs Web Service?
👉 Web Service = API exposed over network

---

## 1️⃣1️⃣ Interview Questions

1. Web Service kya hota hai?
2. SOAP aur REST me difference?
3. REST kyun popular hai?
4. Web Service ka real use case?
5. HTTP status codes kyun zaroori hain?

---

## ✅ Summary

- Web Service = system-to-system communication
- REST = most used web service type
- Spring Boot web services banana easy
- JSON + HTTP backbone hai

---

### ❓ Next Topic?
**MODULE 3 → Topic (c): REST API Development**

👉 Likho: **YES**

