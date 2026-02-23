# 📘 MODULE 1 – SPRING BASICS
## 🔹 Topic (f): Spring Configuration

---

## 🧠 1. Spring Configuration kya hota hai?

Spring Configuration ka matlab hai:
> **Spring ko batana ki kaunse objects (beans) kaise create honge aur kaise manage honge**

Configuration se hum decide karte hain:
- Bean kaise banegi
- Dependency kaise inject hogi
- Application ka behavior kya hoga

---

## 🧩 2. Spring Configuration ke Types

Spring me mainly **3 tareeke** hote hain configuration likhne ke:

1. XML Configuration (Old / Legacy)
2. Java-based Configuration (Recommended ✅)
3. Annotation-based Configuration (Most Used ✅)

Hum **Java + Annotation** approach use karenge.

---

## ❌ 3. XML Configuration (Old Way – Just for Knowledge)

```xml
<bean id="paymentService" class="com.example.PaymentService" />
```

❌ Problems:
- Zyada verbose
- Maintain karna mushkil
- Modern projects me use nahi hota

---

## ✅ 4. Java-based Configuration (@Configuration)

### 📌 @Configuration kya karta hai?
- Is class ko Spring configuration class declare karta hai
- Is class ke andar defined beans ko Spring manage karta hai

### Example:
```java
@Configuration
public class AppConfig {

    @Bean
    public PaymentService paymentService() {
        return new PaymentService();
    }
}
```

### Yahan kya ho raha hai?
- `@Configuration` → Batata hai yeh config class hai
- `@Bean` → Spring ko bolta hai object manage karo

---

## 🫘 5. @Bean Annotation (Deep Explanation)

### Purpose:
- Method ke return object ko Spring Bean banana

### Kab use kare?
- Jab third-party class ho
- Jab manual control chahiye

### Example:
```java
@Bean
public ObjectMapper objectMapper() {
    return new ObjectMapper();
}
```

---

## 🏷️ 6. Annotation-based Configuration

Spring automatically classes scan karta hai using annotations.

### Common Annotations:
- `@Component`
- `@Service`
- `@Repository`
- `@Controller`

### Example:
```java
@Component
public class EmailService {
    public void send() {
        System.out.println("Email Sent");
    }
}
```

👉 Spring automatically isko Bean bana dega.

---

## 🔍 7. Component Scanning

### @ComponentScan kya karta hai?
- Spring ko batata hai kaunse packages scan karne hain

### Example:
```java
@Configuration
@ComponentScan(basePackages = "com.example")
public class AppConfig {
}
```

👉 Spring in packages me annotated classes dhundhega.

---

## 🚀 8. Spring Boot Auto-Configuration

Spring Boot me:
- Manual config ki need kam hoti hai
- Convention over configuration follow hota hai

### @SpringBootApplication
Ye annotation internally ye sab karta hai:
- `@Configuration`
- `@ComponentScan`
- `@EnableAutoConfiguration`

---

## 🔄 9. Configuration Flow (ASCII Diagram)

```
Application Start
      |
      v
@Configuration Class Loaded
      |
      |-- @Bean Methods Execute
      |-- Component Scan
      |
      v
Beans Registered in Context
```

---

## 🌍 10. Real World Use Case

### Enterprise Application

- DataSource configuration
- Security configuration
- Kafka / Redis config

👉 Centralized configuration se maintenance easy hota hai.

---

## ⚠️ 11. Common Mistakes

- @Configuration miss kar dena
- Wrong package scan
- Bean name conflicts

---

## 🎯 12. Interview Focus

## 1️⃣ Difference: `@Component` vs `@Bean`

Dono ka use **Spring container me object (bean) create karne** ke liye hota hai, lekin kaam karne ka tareeqa alag hai.

### 🔍 Comparison Table

| Point | `@Component` | `@Bean` |
|------|-------------|---------|
| Use kahan hota hai | Class ke upar | Method ke upar |
| Object kaun banata hai | Spring automatically | Developer manually |
| Detection kaise hota hai | Component scanning se | `@Configuration` class se |
| Control | Kam control | Zyada control |
| Use case | Apni classes | Third-party / external classes |

### ✅ `@Component` Example
```java
@Component
public class MyService {
}

🔹 Jab Spring application start hota hai, to:

    Spring classpath scan karta hai

    @Component wali class detect karta hai

    Automatically object (bean) bana deta hai

✅ @Bean Example

@Configuration
public class AppConfig {

    @Bean
    public MyService myService() {
        return new MyService();
    }
}

🔹 Yahan:

Object kaise banega → ye developer decide karta hai

Mostly third-party classes ke liye use hota hai

👉 Conclusion:

Simple classes → @Component

External / customized object creation → @Bean

➡️ Ye dono annotations Spring Framework ka core part hain.


---

## ✅ 13. Summary

- Spring Configuration batata hai beans kaise banengi
- Java + Annotation approach best hai
- @Configuration + @Bean powerful combo
- Spring Boot auto-config karta hai

---

## ⏭️ Next Topic

🔹 **Module 1 – Topic (g): Spring Auto-Wiring**

❓ Should I move to the next topic?
👉 YES / NO likho

