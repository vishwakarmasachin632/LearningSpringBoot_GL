# MODULE 5 – SPRING SECURITY
## Topic (l): Spring Security Assessment (30 MCQs)

---

## 📝 Instructions
- Total Questions: **30**
- Type: Scenario + Concept based
- Har question ke saath **correct answer + explanation** diya gaya hai
- Language: Hinglish

---

### Q1️⃣ Spring Security ka core architecture kis concept par based hota hai?
A. Controller based
B. Aspect based
C. Filter based ✅
D. Servlet based

**Explanation:** Spring Security request ko controller tak pahunchne se pehle filters se pass karta hai.

---

### Q2️⃣ `SecurityFilterChain` ka main role kya hai?
A. Controllers map karna
B. Filters ka order define karna ✅
C. DB connection banana
D. JWT generate karna

**Explanation:** Ye filters ki ordered list hoti hai jo request process karti hai.

---

### Q3️⃣ 401 Unauthorized ka matlab kya hota hai?
A. User logged in hai
B. Permission nahi hai
C. Token missing/invalid hai ✅
D. Server error

**Explanation:** 401 authentication failure hota hai.

---

### Q4️⃣ 403 Forbidden kab aata hai?
A. Token invalid ho
B. User authenticated ho par permission na ho ✅
C. Server down ho
D. Password galat ho

---

### Q5️⃣ JWT kaunsa type ka authentication hai?
A. Stateful
B. Stateless ✅
C. Session based
D. Cookie based

---

### Q6️⃣ JWT ka payload kis form me hota hai?
A. Encrypted
B. Plain JSON ✅
C. Binary
D. XML

---

### Q7️⃣ JWT me sensitive data kyun nahi rakhna chahiye?
A. Size zyada hota hai
B. Payload encrypted nahi hota ✅
C. Token expire ho jata hai
D. Parsing slow hoti hai

---

### Q8️⃣ `PasswordEncoder` ka role kya hai?
A. Password decrypt karna
B. Password hash + verify karna ✅
C. Token generate karna
D. User create karna

---

### Q9️⃣ BCrypt kyun recommended hai?
A. Fast hai
B. Reversible hai
C. Salt + slow hashing karta hai ✅
D. Plain text store karta hai

---

### Q1️⃣0️⃣ JDBC Authentication me user data kahan se aata hai?
A. properties file
B. Hardcoded
C. Database tables se ✅
D. JWT se

---

### Q1️⃣1️⃣ Method level security enable karne ke liye kaunsa annotation use hota hai?
A. @EnableSecurity
B. @EnableWebSecurity
C. @EnableMethodSecurity ✅
D. @SecureMethods

---

### Q1️⃣2️⃣ @PreAuthorize kab check hota hai?
A. Method ke baad
B. Method ke pehle ✅
C. Controller load par
D. Application start par

---

### Q1️⃣3️⃣ Role internally kaise store hota hai?
A. ADMIN
B. ROLE_ADMIN ✅
C. admin_role
D. role-admin

---

### Q1️⃣4️⃣ REST APIs ke liye CSRF kyun disable karte hain?
A. CSRF kaam nahi karta
B. REST stateless hota hai ✅
C. Security kam hoti hai
D. JWT me bug hota hai

---

### Q1️⃣5️⃣ OAuth2 ka primary purpose kya hai?
A. Authentication
B. Authorization delegation ✅
C. Password encryption
D. Session management

---

### Q1️⃣6️⃣ "Login with Google" kaunse concept par based hai?
A. JWT
B. Basic Auth
C. OAuth2 ✅
D. LDAP

---

### Q1️⃣7️⃣ OAuth2 me password kisko diya jata hai?
A. Application ko
B. Client ko
C. Authorization Server ko ✅
D. Resource Server ko

---

### Q1️⃣8️⃣ OAuth2 ka most used grant type kaunsa hai?
A. Password
B. Implicit
C. Authorization Code ✅
D. Client Secret

---

### Q1️⃣9️⃣ SecurityContext me kya store hota hai?
A. JWT token
B. User authentication details ✅
C. DB connection
D. Controller info

---

### Q2️⃣0️⃣ SecurityContextHolder ka kaam kya hai?
A. Token generate karna
B. Thread-local security data rakhna ✅
C. Session manage karna
D. Filter register karna

---

### Q2️⃣1️⃣ Method level security ka best place kya hai?
A. Controller
B. Repository
C. Service layer ✅
D. Entity

---

### Q2️⃣2️⃣ `hasRole('ADMIN')` internally kis authority ko check karta hai?
A. ADMIN
B. ROLE_ADMIN ✅
C. admin
D. ROLE-ADMIN

---

### Q2️⃣3️⃣ JWT expire hone ke baad kya hota hai?
A. Automatically renew
B. Request reject hoti hai ✅
C. User logout nahi hota
D. Token valid rehta hai

---

### Q2️⃣4️⃣ Stateless authentication ka main benefit kya hai?
A. Fast DB
B. Easy scaling ✅
C. Simple code
D. Less security

---

### Q2️⃣5️⃣ JWT filter ka role kya hai?
A. Token generate karna
B. Token validate karna ✅
C. User save karna
D. Password encode karna

---

### Q2️⃣6️⃣ `OncePerRequestFilter` kyun use hota hai?
A. Multiple times filter run karne ke liye
B. Har request pe ek baar run karne ke liye ✅
C. Only login pe
D. Controller ke baad

---

### Q2️⃣7️⃣ Role-based authorization ka example kya hai?
A. Password match
B. Token generate
C. ADMIN accessing admin API only ✅
D. DB connect

---

### Q2️⃣8️⃣ Spring Security me default role prefix kya hai?
A. ADMIN_
B. ROLE_ ✅
C. SPRING_
D. SEC_

---

### Q2️⃣9️⃣ Microservices ke liye kaunsa auth best hai?
A. Session
B. Cookies
C. JWT / OAuth2 ✅
D. Basic Auth

---

### Q3️⃣0️⃣ Production REST APIs me kaunsa approach best practice hai?
A. Controller-only security
B. No security
C. Filter + Method level security ✅
D. Hardcoded roles

---

## 🎉 Assessment Complete

✔ Agar tum 22+ correct kar lete ho → **Spring Security STRONG** 💪

---

❓ **Next move?**

🔹 MODULE 6 → SPRING MICROSERVICES

👉 Batao: **YES** ya **REPEAT SECURITY**

