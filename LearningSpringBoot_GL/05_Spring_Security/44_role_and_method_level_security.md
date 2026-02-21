# MODULE 5 – SPRING SECURITY
## Topic (g): Role & Method Level Security

---

## 1️⃣ Role & Method Level Security kya hota hai?

Role & Method Level Security ka matlab hota hai:
- **Kaunsa USER kaunsa API access kar sakta hai**
- **Kaunsa ROLE kaunsa METHOD execute kar sakta hai**

👉 Ye security **Controller level se bhi zyada fine‑grained** hoti hai.

---

## 2️⃣ Real World Example (Industry Scenario)

🏦 **Banking System**
- USER → sirf account dekh sakta hai
- ADMIN → account create / delete kar sakta hai
- MANAGER → reports generate kar sakta hai

👉 Agar controller same ho, tab bhi **method level security** kaam aati hai.

---

## 3️⃣ Types of Security in Spring Boot

| Level | Description |
|---|---|
| URL Level | Endpoint based (`/admin/**`) |
| Method Level | Method / function based |

👉 Industry me **dono use hote hain**

---

## 4️⃣ Method Level Security Enable karna (IMPORTANT)

```java
@Configuration
// 👉 Security related configuration class
@EnableMethodSecurity
// 👉 Method level annotations ko enable karta hai
// 👉 @PreAuthorize, @PostAuthorize kaam karenge
public class SecurityConfig {
}
```

---

## 5️⃣ Common Method Level Annotations

### 🔹 @PreAuthorize
Method execute hone **se pehle** check hota hai

```java
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser() {
}
```

### 🔹 @PostAuthorize
Method execute hone **ke baad** check hota hai

```java
@PostAuthorize("returnObject.username == authentication.name")
public User getUser() {
}
```

### 🔹 @Secured
Old style, simple role check

```java
@Secured("ROLE_ADMIN")
public void adminTask() {}
```

---

## 6️⃣ Practical Example – Service Layer Security

```java
@Service
// 👉 Business logic ke liye
public class AccountService {

    @PreAuthorize("hasRole('USER')")
    // 👉 Sirf USER role wala access karega
    public String viewAccount() {
        return "Account Details";
    }

    @PreAuthorize("hasRole('ADMIN')")
    // 👉 Sirf ADMIN role wala delete karega
    public void deleteAccount() {
    }
}
```

---

## 7️⃣ SpEL (Spring Expression Language)

Spring Security expressions:

| Expression | Meaning |
|---|---|
| hasRole('ADMIN') | Role check |
| hasAuthority('READ') | Authority check |
| isAuthenticated() | Login check |
| authentication.name | Logged‑in username |

---

## 8️⃣ Role vs Authority (VERY IMPORTANT 🔥)

| Role | Authority |
|---|---|
| ROLE_USER | READ |
| ROLE_ADMIN | WRITE |

👉 Internally **ROLE_ prefix mandatory** hota hai

---

## 9️⃣ Controller + Method Security Combined

```java
@RestController
@RequestMapping("/api")
public class DemoController {

    @GetMapping("/user")
    @PreAuthorize("hasRole('USER')")
    public String userApi() {
        return "User API";
    }

    @GetMapping("/admin")
    @PreAuthorize("hasRole('ADMIN')")
    public String adminApi() {
        return "Admin API";
    }
}
```

---

## 🔟 Common Interview Questions 🔥

- Method level security kyun chahiye?
- @PreAuthorize vs @Secured difference?
- Role vs Authority ka real difference?
- SpEL kya hota hai?

---

## 1️⃣1️⃣ Summary

✔ Method level security = fine‑grained control
✔ Service layer me lagana best practice
✔ @PreAuthorize sabse powerful
✔ JWT / OAuth2 me heavily used

---

❓ **Next topic move karein?**

🔹 MODULE 5 → Topic (h): JWT Authentication (Deep + Industry)

👉 Sirf **YES** likho

