# MODULE 5 – SPRING SECURITY
## Topic (f): Password Encoding & BCrypt

---

## 1️⃣ Password Encoding kya hota hai?

Password Encoding ka matlab hai **user ke password ko plain text me store na karna**.

👉 Plain password store karna **bahut bada security risk** hai:
- Database leak ho jaye to sab passwords expose
- Legal & compliance issues

Isliye industry me **encoded (hashed) passwords** store kiye jaate hain.

---

## 2️⃣ Encoding vs Encryption vs Hashing

| Term | Meaning | Reversible? | Usage |
|---|---|---|---|
| Encoding | Format change | ✅ | Data transfer |
| Encryption | Secret key se secure | ✅ | Sensitive data |
| Hashing | One-way | ❌ | Passwords |

👉 **Passwords ke liye ALWAYS Hashing**

---

## 3️⃣ BCrypt kya hai?

BCrypt ek **strong hashing algorithm** hai jo:
- Salt automatically add karta hai
- Brute force attacks se protect karta hai
- Slow hashing karta hai (security ke liye good)

👉 **Spring Security ka recommended encoder** ✅

---

## 4️⃣ Real World Example

🏦 Banking App:
- User registers → password encode hota hai
- DB me encoded password store hota hai
- Login time raw password + encoded password match hote hain

---

## 5️⃣ PasswordEncoder Interface

```java
public interface PasswordEncoder {
    String encode(CharSequence rawPassword);
    boolean matches(CharSequence rawPassword, String encodedPassword);
}
```

---

## 6️⃣ BCryptPasswordEncoder Bean Configuration

```java
@Configuration
// 👉 Security related beans define karne ke liye
public class SecurityConfig {

    @Bean
    // 👉 Password hashing ke liye
    // 👉 JDBC / JWT sab jagah required
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

---

## 7️⃣ Password Encode karna (User Registration)

```java
@Service
// 👉 Business logic ke liye
public class UserService {

    private final PasswordEncoder passwordEncoder;

    public UserService(PasswordEncoder passwordEncoder) {
        this.passwordEncoder = passwordEncoder;
    }

    public void registerUser(String username, String password) {
        String encodedPassword = passwordEncoder.encode(password);
        // 👉 Encoded password DB me save hoga
        System.out.println(encodedPassword);
    }
}
```

---

## 8️⃣ Password Matching (Login Time)

```java
boolean isMatch = passwordEncoder.matches(
        rawPassword,
        encodedPasswordFromDb
);
```

👉 Spring Security internally ye kaam khud karta hai

---

## 9️⃣ BCrypt Strength (Cost Factor)

```java
new BCryptPasswordEncoder(12);
```

| Cost | Security | Speed |
|---|---|---|
| 8 | Low | Fast |
| 10 | Medium | Normal |
| 12 | High | Slow |

👉 Production ke liye **10–12 recommended**

---

## 🔟 Common Interview Questions 🔥

- Plain password store karna kyun wrong hai?
- BCrypt kyun MD5 / SHA-1 se better hai?
- PasswordEncoder ka role kya hai?
- `matches()` kaise kaam karta hai?

---

## 1️⃣1️⃣ Summary

✔ Password hashing mandatory hai
✔ BCrypt industry standard hai
✔ Spring Security automatically password match karta hai
✔ JWT & OAuth2 ka foundation

---

❓ **Next topic move karein?**

🔹 MODULE 5 → Topic (g): Role & Method Level Security

👉 Sirf **YES** likho

