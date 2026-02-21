# 13) Spring Boot Application Debugging

> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Build Tool:** Maven  
> **DB Context:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ Debugging kya hota hai? (Theory)
Debugging ka matlab hota hai:
> **Application me aane wale bugs / errors ka root cause find karna** aur unko fix karna.

Simple language me:
- Code kyu fail ho raha hai?
- Expected output kyu nahi aa raha?
- Application crash kyu hui?

👉 In sab ka jawab debugging se milta hai.

---

## 2️⃣ Real-World Use Case (Industry Scenario)
**Scenario:**
Production me error aaya:
> HTTP 500 – Internal Server Error

Tum directly prod DB ya code change nahi kar sakte.

Tum kya karoge?
1. Logs check karoge
2. Debug mode me local run karoge
3. Breakpoints lagaoge
4. Root cause nikaaloge

👉 Ye hi real debugging flow hota hai.

---

## 3️⃣ Types of Debugging in Spring Boot

### 🔹 1) Logging based debugging
- Logs dekh kar issue samajhna
- Production me MOST USED

### 🔹 2) IDE Debugger (IntelliJ)
- Breakpoints
- Step Over / Step Into
- Variable inspection

### 🔹 3) Spring Boot Debug Mode
- Auto-configuration details

---

## 4️⃣ IntelliJ Debugging (Practical)

### Step 1: Breakpoint lagana
- Line number pe click karo (🔴 red dot)

### Step 2: Debug mode me run
- Run ▶️ ke bajay **Debug 🐞** button

### Step 3: Debug Controls
| Button | Use |
|------|----|
| Step Over | Next line |
| Step Into | Method ke andar |
| Resume | Next breakpoint |

---

## 5️⃣ Debug Example (Service Class)

```java
@Service
public class OrderService {

    public int placeOrder(int qty) {
        int price = 100;
        int total = qty * price; // 🔴 breakpoint yahan

        return total;
    }
}
```

Debug karte waqt:
- qty ki value dekho
- price check karo
- total calculation verify karo

---

## 6️⃣ Spring Boot Debug Mode

### application.properties
```properties
# Spring Boot auto-configuration debug
# Ye batata hai kaun se beans load hue
# Kaun se skip hue

debug=true
```

Run logs me:
- `CONDITIONS EVALUATION REPORT`
- Auto-config details

👉 Interview favorite topic 🔥

---

## 7️⃣ Common Errors & Debugging Tips

### ❌ Bean not found
- Cause: Component scan issue
- Fix: Package structure check

### ❌ Port already in use
```properties
server.port=9090
```

### ❌ NullPointerException
- Debug variables
- Check injection

---

## 8️⃣ Debugging Flow (ASCII Diagram)
```
Bug/Error
   |
   v
Check Logs
   |
   v
Local Debug Mode
   |
   v
Breakpoint Hit
   |
   v
Inspect Variables
   |
   v
Fix Code
```

---

## 9️⃣ Production Debugging Best Practices

✔ Proper logging levels
✔ Correlation IDs
✔ Never debug directly on prod
✔ Reproduce issue locally

---

## 🔟 Interview Questions

1. Debugging kya hota hai?
2. Logging vs Debugging
3. IntelliJ debugger ka use
4. `debug=true` ka purpose
5. Production debugging kaise karte ho?

---

## ✅ Summary
- Debugging = problem solving skill
- Logs + Debugger = best combo
- Spring Boot debug mode powerful tool
- Industry me debugging daily ka kaam hai

---

### ✅ Next Topic?
**MODULE 1 → Topic (n): Spring Basics Capstone Project**

👉 Likho: **YES**

