# MODULE 5 – SPRING SECURITY
## Topic (b): Authentication vs Authorization (Deep Dive)

> Language: Hinglish
> JDK: 21 | Spring Boot: Latest Stable | Maven | IntelliJ IDEA

---

## 1️⃣ Authentication kya hota hai?

**Authentication** ka matlab hota hai:
> 👉 "Tum kaun ho?"

System verify karta hai ki user **real hai ya nahi**.

### Common authentication methods:
- Username + Password
- OTP
- JWT Token
- OAuth2 (Google, GitHub login)

**Example:**
> User login karta hai → system credentials verify karta hai → user authenticated

---

## 2️⃣ Authorization kya hota hai?

**Authorization** ka matlab hota hai:
> 👉 "Tum kya kar sakte ho?"

Isme system check karta hai ki user ko **kaun-sa resource access karne ka right** hai.

**Example:**
- USER → sirf profile dekh sakta hai
- ADMIN → sabka data dekh sakta hai

---

## 3️⃣ Simple Real-Life Example (Office Entry)

```
Office Building

Security Guard → Authentication (ID check)
HR Manager → Authorization (Which room access?)
```

👉 Pehle authentication, phir authorization

---

## 4️⃣ Spring Security Flow (Authentication → Authorization)

```
Client Request
   ↓
Spring Security Filters
   ↓
Authentication Manager
   ↓
Security Context
   ↓
Authorization Check
   ↓
Controller Access
```

### Step Explanation:
1. Request aati hai
2. User authenticate hota hai
3. User details SecurityContext me store hoti hain
4. Role/authority check hota hai
5. Access allow/deny

---

## 5️⃣ Authentication in Spring Security

Spring Security authentication ke liye use karta hai:
- AuthenticationManager
- UserDetailsService
- PasswordEncoder

**Responsibility split:**
- UserDetailsService → user data laata hai
- PasswordEncoder → password match karta hai

---

## 6️⃣ Authorization in Spring Security

Authorization ke tareeke:
- URL based security
- Method level security
- Role-based access

Examples:
- `/admin/**` → ADMIN only
- `/user/**` → USER, ADMIN

---

## 7️⃣ Role vs Authority

| Concept | Meaning |
|------|--------|
| Role | High-level permission (ROLE_ADMIN) |
| Authority | Fine-grained permission (READ_USER) |

👉 Spring internally **authorities** use karta hai

---

## 8️⃣ Authentication vs Authorization (Comparison Table)

| Feature | Authentication | Authorization |
|------|---------------|---------------|
| Question | Who are you? | What can you do? |
| Happens | First | After authentication |
| Example | Login | Role check |
| Failure | 401 Unauthorized | 403 Forbidden |

---

## 9️⃣ REST API Status Codes

- **401 Unauthorized** → Authentication failed / missing
- **403 Forbidden** → Authorization failed

Interview me ye difference zaroor puchte hain ⚠️

---

## 🔟 Real-World REST API Scenario

### Banking API

```
POST /login        → Authentication
GET /accounts     → Authorization (ROLE_USER)
DELETE /accounts  → Authorization (ROLE_ADMIN)
```

---

## 1️⃣1️⃣ Interview Ready Points

- Authentication ≠ Authorization
- Auth happens before authorization
- JWT mostly authentication ke liye use hota hai
- Roles & authorities authorization ke liye

---

## 1️⃣2️⃣ Summary

- Authentication = identity verification
- Authorization = access control
- Spring Security dono ko separate handle karta hai

---

✅ Topic (b) COMPLETE

❓ **Should I move to next topic?**

🔹 MODULE 5 → Topic (c): Security Architecture & Filters

👉 Sirf **YES** likho.

