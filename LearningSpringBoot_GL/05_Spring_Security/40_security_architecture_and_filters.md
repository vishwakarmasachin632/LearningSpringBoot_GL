# MODULE 5 – SPRING SECURITY
## Topic (c): Security Architecture & Filters

> Language: Hinglish
> JDK: 21 | Spring Boot: Latest Stable | Maven | IntelliJ IDEA

---

## 1️⃣ Spring Security Architecture ka overview

Spring Security **filter-based architecture** par kaam karta hai.

Matlab:
> Har incoming HTTP request pehle **Security Filters** se guzarti hai,
> phir Controller tak jaati hai.

Controller ke pehle hi security decision le liya jaata hai.

---

## 2️⃣ Filter-Based Architecture kya hoti hai?

Servlet world me **Filter** ek component hota hai jo:
- Request ko intercept karta hai
- Request / Response ko modify kar sakta hai
- Aage allow ya block kar sakta hai

Spring Security isi concept ko use karta hai.

---

## 3️⃣ High-Level Security Flow (ASCII Diagram)

```
Client Request
      ↓
Security Filter Chain
      ↓
Authentication Filters
      ↓
Authorization Filters
      ↓
DispatcherServlet
      ↓
Controller
```

### Step-by-step samjho:
1. Client request bhejta hai
2. Request Security Filter Chain me enter hoti hai
3. Authentication check hota hai
4. Authorization check hota hai
5. Agar pass → controller
6. Fail → 401 / 403

---

## 4️⃣ Security Filter Chain kya hoti hai?

**SecurityFilterChain** ek ordered list hoti hai filters ki.

Ye filters:
- Login handle karte hain
- Tokens verify karte hain
- Roles check karte hain

> ⚠️ Order bahut important hota hai

---

## 5️⃣ Important Spring Security Filters (Beginner Friendly)

### 🔹 1. SecurityContextPersistenceFilter
- SecurityContext ko load/save karta hai
- Request ke start aur end pe kaam karta hai

---

### 🔹 2. UsernamePasswordAuthenticationFilter
- Login request handle karta hai
- Username + password authenticate karta hai

---

### 🔹 3. BasicAuthenticationFilter
- HTTP Basic authentication ke liye
- Header se credentials padhta hai

---

### 🔹 4. BearerTokenAuthenticationFilter
- JWT token read karta hai
- Token validate karta hai

---

### 🔹 5. ExceptionTranslationFilter
- Security exceptions handle karta hai
- 401 / 403 response bhejta hai

---

### 🔹 6. FilterSecurityInterceptor
- Final authorization decision leta hai
- Role / authority check karta hai

---

## 6️⃣ SecurityContext & SecurityContextHolder

### SecurityContext
- Authenticated user ki details rakhta hai
- Principal + roles + authorities

### SecurityContextHolder
- Thread-local storage
- Current request ka security data rakhta hai

---

## 7️⃣ AuthenticationManager ka role

AuthenticationManager:
- Credentials verify karta hai
- UserDetailsService ko call karta hai
- PasswordEncoder use karta hai

> Ye authentication ka **brain** hota hai 🧠

---

## 8️⃣ Authorization kaise hoti hai?

Authorization hoti hai:
- URL match karke
- Method pe annotation dekh ke
- Role / authority compare karke

Example:
```
/admin/** → ROLE_ADMIN
```

---

## 9️⃣ Real-World REST API Example

```
POST /login        → Authentication Filter
GET /users        → ROLE_USER
DELETE /users     → ROLE_ADMIN
```

---

## 🔟 Interview Ready Points (🔥 Important)

- Spring Security = Filter based
- Controller se pehle security lagti hai
- SecurityContext request scoped hota hai
- 401 ≠ 403
- Filter order matters

---

## 1️⃣1️⃣ Common Beginner Confusion

❓ Controller me security kyu nahi likhte?

✅ Kyunki:
- Security cross-cutting concern hai
- Filter level pe centralize hoti hai
- Clean architecture maintain hota hai

---

## 1️⃣2️⃣ Summary

- Spring Security filters pe based hai
- Authentication + Authorization filters alag hote hain
- Ye base samajh liya to JWT, OAuth easy ho jaata hai

---

✅ Topic (c) COMPLETE

❓ **Should I move to next topic?**

🔹 MODULE 5 → Topic (d): In-Memory Authentication

👉 Sirf **YES** likho.

