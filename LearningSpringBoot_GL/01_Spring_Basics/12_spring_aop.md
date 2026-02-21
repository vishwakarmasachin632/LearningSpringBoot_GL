# 12) Aspect Oriented Programming (AOP)

> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Build Tool:** Maven  
> **DB Context:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ AOP kya hota hai? (Theory)
AOP ka full form hai **Aspect Oriented Programming**.

Simple words me:
> AOP ka use **cross‑cutting concerns** ko alag rakhne ke liye hota hai.

### Cross‑cutting concerns kya hote hain?
Wo code jo:
- Har layer me repeat hota hai
- Business logic ka part nahi hota

Examples:
- Logging
- Security
- Transaction
- Performance monitoring

---

## 2️⃣ Problem Without AOP (Real pain)

```java
public void pay() {
    log.info("Start");
    // business logic
    log.info("End");
}
```

Har method me:
- Logging
- Security checks

❌ Code duplicate
❌ Maintenance problem

---

## 3️⃣ Solution: AOP
AOP bolta hai:
> Business logic ko clean rakho, extra logic **Aspect** me daal do.

---

## 4️⃣ AOP ke Important Terms

| Term | Meaning |
|----|----|
| Aspect | Extra logic class |
| Advice | Kab run kare |
| Join Point | Method execution point |
| Pointcut | Kis method pe |
| Weaving | Aspect attach karna |

---

## 5️⃣ Real‑World Use Case
**Scenario:**
Payment application me:
- Har API ka execution time log karna hai
- Bina business code change kiye

👉 AOP best solution hai.

---

## 6️⃣ Spring AOP Annotations (WITH WHY)

```java
@Aspect
// Purpose: Is class ko Aspect banana
// When: Jab cross‑cutting logic likhna ho
// Why here: Spring ko batane ke liye ye aspect hai
```

```java
@Component
// Purpose: Spring bean banana
// When: Aspect ko container me register karna ho
// Why here: Spring is class ko manage kare
```

```java
@Before
// Purpose: Method se pehle logic run
// When: Validation, logging start
// Why here: Method execution se pehle run chahiye
```

```java
@After
// Purpose: Method ke baad logic
// When: Cleanup
// Why here: Always run after method
```

```java
@Around
// Purpose: Method ke pehle aur baad
// When: Performance monitoring
// Why here: Total control chahiye
```

---

## 7️⃣ Practical Example (Execution Time Logging)

### Aspect Class
```java
package com.example.demo.aop;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.stereotype.Component;

@Aspect // Batata hai ye AOP aspect hai
@Component // Spring bean banata hai
public class LoggingAspect {

    @Around("execution(* com.example.demo.service.*.*(..))")
    // execution = kis package ki method
    // service layer ke sab methods
    public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();

        Object result = joinPoint.proceed(); // actual method call

        long end = System.currentTimeMillis();
        System.out.println(joinPoint.getSignature() + " executed in " + (end - start) + "ms");
        return result;
    }
}
```

---

## 8️⃣ AOP Flow (ASCII Diagram)
```
Client
  |
  v
Controller
  |
  v
AOP Proxy
  |
  | Before / Around Advice
  v
Service Method
  |
  | After Advice
  v
Return Response
```

---

## 9️⃣ Common Mistakes
❌ AOP ko business logic ke liye use karna
❌ Wrong pointcut expression
❌ AOP vs Filter vs Interceptor confusion

---

## 🔟 Interview Questions

1. AOP kya hai?
2. Cross‑cutting concern kya hota hai?
3. `@Around` vs `@Before`
4. AOP real projects me kyun use hota hai?
5. Spring AOP vs AspectJ

---

## ✅ Summary
- AOP = clean code
- Logging, security ke liye best
- Business logic isolated
- Industry standard practice

---

### ✅ Next Topic?
**MODULE 1 → Topic (m): Spring Boot Application Debugging**

👉 Likho: **YES**

