# 10) Spring Boot Logging

> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Build Tool:** Maven  
> **DB Context:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ Logging kya hota hai? (Theory)
Logging ka matlab hai **application ke andar hone wali activities ka record rakhna**.

Simple words me:
- App start hui
- Koi API hit hui
- Koi error aaya
- DB call hua

👉 Ye sab cheezein **logs** me likhi jaati hain.

### Logging kyun zaroori hai?
- Debugging ke liye
- Production issues samajhne ke liye
- Monitoring & auditing ke liye
- Performance analysis ke liye

---

## 2️⃣ Real-World Use Case
**Scenario:**
Production me user bolta hai:
> "Payment fail ho raha hai"

Tum directly user ka system nahi dekh sakte ❌

Tum kya karoge?
- Server logs check
- Error ka exact reason milega
- Fix apply karoge

👉 Isliye logging industry me **MOST IMPORTANT** hai.

---

## 3️⃣ Spring Boot me Logging kaise kaam karta hai?

Spring Boot by default:
- **SLF4J** (logging facade) use karta hai
- **Logback** ko implementation ke roop me deta hai

Tumhe manually kuch add karne ki zaroorat nahi hoti 👍

---

## 4️⃣ Logging Levels (VERY IMPORTANT)

| Level | Meaning | Kab use kare |
|------|--------|-------------|
| TRACE | Sabse detailed | Deep debugging |
| DEBUG | Debug info | Development |
| INFO | Normal flow | App status |
| WARN | Potential issue | Risky situation |
| ERROR | Failure | Exception / crash |

👉 Production me usually **INFO / WARN / ERROR** enabled rehta hai.

---

## 5️⃣ Logger kaise banate hain? (Practical)

### Example: Service Class
```java
package com.example.demo.service;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Service;

// @Service batata hai ki ye class business logic ke liye hai
// Ye Spring container me bean ban jaati hai
@Service
public class PaymentService {

    // LoggerFactory se logger object milta hai
    // Har class ke liye alag logger banana best practice hai
    private static final Logger logger = LoggerFactory.getLogger(PaymentService.class);

    public void processPayment(double amount) {
        // INFO: normal application flow
        logger.info("Payment processing started. Amount: {}", amount);

        if (amount <= 0) {
            // WARN: galat input, but app crash nahi hui
            logger.warn("Invalid payment amount received: {}", amount);
        }

        try {
            // Dummy logic
            int result = 10 / 2;

            // DEBUG: internal calculation info
            logger.debug("Payment calculation result: {}", result);

        } catch (Exception ex) {
            // ERROR: serious problem
            logger.error("Payment processing failed", ex);
        }
    }
}
```

---

## 6️⃣ application.properties me logging config

```properties
# Root logging level
logging.level.root=INFO

# Package specific logging
logging.level.com.example.demo=DEBUG

# Log file location
logging.file.name=logs/app.log
```

### Explanation:
- `logging.level.root` → default level
- `package logging` → specific module debug
- `logging.file.name` → file me logs store

---

## 7️⃣ Console vs File Logging

| Type | Use |
|----|----|
| Console | Development & debugging |
| File | Production & audit |

👉 Real projects me **Dono enabled** rehte hain.

---

## 8️⃣ Logging Flow (ASCII Diagram)
```
Application Code
      |
      | logger.info()
      v
SLF4J API
      |
      v
Logback
      |
      v
Console / Log File
```

### Step Explanation:
1. Code logger call karta hai
2. SLF4J request receive karta hai
3. Logback process karta hai
4. Output console/file me likha jata hai

---

## 9️⃣ Common Logging Mistakes
❌ System.out.println() use karna
❌ Sensitive data (password, card) log karna
❌ Har jagah ERROR use karna
❌ Debug logs production me ON rakhna

---

## 🔟 Interview Questions

1. Logging kya hota hai?
2. SLF4J kya hai?
3. Logback kya hai?
4. Logging levels explain karo
5. System.out.println kyun avoid karte hain?

---

## ✅ Summary
- Logging = application ka black box recorder
- Spring Boot me logging built-in hoti hai
- SLF4J + Logback default stack
- Proper level use karna industry standard hai

---

### ✅ Next Topic?
**MODULE 1 → Topic (k): Spring Boot IoC & DI**

👉 Likho: **YES**

