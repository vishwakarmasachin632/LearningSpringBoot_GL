# 📘 MODULE 1 – SPRING BASICS
## 🔹 Topic (c): Spring Context

---

## 🧠 1. Spring Context kya hota hai?

**Spring Context** Spring Framework ka woh part hai jo **Spring Container** ko power deta hai.

Simple words me:
> Spring Context = Jagah jahan Spring **beans ko rakhta, manage karta aur supply karta** hai

Context ke bina:
- Beans nahi milengi
- Dependency Injection kaam nahi karega
- Application start hi nahi hogi

---

## 🏗️ 2. Spring Container vs Spring Context

### Spring Container
- Objects (Beans) banata hai
- Dependencies inject karta hai

### Spring Context (Advanced Container)
- Container + Extra features
- Events
- Internationalization (i18n)
- Resource loading

👉 **Spring Context = Smart Container**

---

## 🧩 3. ApplicationContext Interface

Spring Context ko technically represent karta hai:

```java
ApplicationContext
```

Ye interface:
- BeanFactory ko extend karta hai
- Enterprise features add karta hai

---

## 🔁 4. Types of ApplicationContext

### 1️⃣ ClassPathXmlApplicationContext (Old)
```java
ApplicationContext context =
    new ClassPathXmlApplicationContext("beans.xml");
```

❌ Ab mostly use nahi hota

---

### 2️⃣ AnnotationConfigApplicationContext
```java
ApplicationContext context =
    new AnnotationConfigApplicationContext(AppConfig.class);
```

✔️ Java configuration ke liye

---

### 3️⃣ WebApplicationContext
- Web applications ke liye
- Spring MVC / REST

✔️ Spring Boot internally use karta hai

---

## 🚀 5. Spring Boot me Context ka Role

Spring Boot jab start hota hai:

1. ApplicationContext create karta hai
2. Classes scan karta hai
3. Beans banata hai
4. Dependencies inject karta hai
5. App ready kar deta hai

👉 Ye sab **automatically** hota hai

---

## 🧪 6. Simple Practical Example

### Step 1: Bean Class
```java
@Component
public class MessageService {
    public String getMessage() {
        return "Hello from Spring Context";
    }
}
```

### Step 2: Access Bean from Context
```java
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        ApplicationContext context =
            SpringApplication.run(DemoApplication.class, args);

        MessageService service = context.getBean(MessageService.class);
        System.out.println(service.getMessage());
    }
}
```

---

## 🔄 7. Spring Context Flow (ASCII Diagram)

```
Application Start
      |
      v
SpringApplication.run()
      |
      v
ApplicationContext Created
      |
      |-- Scan Packages
      |-- Create Beans
      |-- Inject Dependencies
      |
      v
Application Ready
```

---

## 🌍 8. Real World Use Case

### Enterprise Application

- 100+ Beans
- Multiple Services
- Multiple Repositories

Spring Context:
- Sab beans ko ek jagah manage karta hai
- Required jagah inject karta hai
- Lifecycle handle karta hai

---

## ⚠️ 9. Common Mistakes

- Bean not found error
- Component scan issue
- Multiple beans confusion

👉 Sab context se related problems hote hain

---

## 🎯 10. Interview Points

## 🎯 Spring Context – Interview Notes

---

## ❓ What is ApplicationContext and why and when we use it?

### ✅ What is ApplicationContext?

**ApplicationContext** is the **Spring container** that creates, manages, and provides Spring Beans.

### 👉 In simple words

*ApplicationContext is the brain of Spring that manages all objects (beans).*

### ✅ Why we use it

* To **create and manage beans automatically**
* To handle **Dependency Injection (DI)**
* To provide advanced features like **AOP, Events, Internationalization (i18n)**

### ✅ When we use it

* In **Spring and Spring Boot applications**
* When we need **enterprise-level features** beyond basic bean creation

### 📝 One-liner (Interview Ready)

👉 *ApplicationContext is a Spring container used to manage beans and provide enterprise features.*

---

## ❓ Difference between BeanFactory & ApplicationContext

| Point          | BeanFactory              | ApplicationContext           |
| -------------- | ------------------------ | ---------------------------- |
| What it is     | Basic Spring container   | Advanced Spring container    |
| Bean Loading   | Lazy loading (on demand) | Eager loading (at startup)   |
| Features       | Only basic DI            | DI + AOP, Events, i18n       |
| Performance    | Less memory at start     | More memory at startup       |
| Ease of use    | Less convenient          | Easy and powerful            |
| Use case       | Simple or small apps     | Enterprise & real-world apps |
| Default choice | ❌ Rarely used            | ✅ Mostly used                |

### 📝 Simple Explanation

* **BeanFactory says:**
  👉 “I will create the object only when you ask for it.”
* **ApplicationContext says:**
  👉 “I will create all required objects when the app starts.”

### 📝 One-liner

👉 *BeanFactory is basic, ApplicationContext is advanced and preferred.*

---

## ❓ Spring Boot me ApplicationContext ka role

### ✅ Spring Boot me Context kya hai?

**ApplicationContext** Spring Boot ka **central container** hota hai jo poore application ko manage karta hai.

### 👉 Simple words me

*Spring Boot me context application ka brain hota hai.*

### ✅ Context ka role

* Beans **create aur manage** karta hai
* **Dependency Injection (DI)** handle karta hai
* **Auto-configuration** apply karta hai
* **AOP, @Transactional, Events** support deta hai
* Application start hote hi **required beans load** karta hai

### ⏱️ Context kab create hota hai?

* Jab application start hoti hai
* `SpringApplication.run()` ke time

### 📝 One-liner (Interview Ready)

👉 *Spring Boot me ApplicationContext beans aur configuration ko manage karta hai.*

---


---

## ✅ 11. Summary

- Spring Context = Advanced Container
- ApplicationContext is main interface
- Spring Boot context automatically manage karta hai
- Context ke bina Spring app possible nahi

---

## ⏭️ Next Topic

🔹 **Module 1 – Topic (d): Dependency Injection (Deep Dive)**

❓ Should I move to the next topic?
👉 YES / NO likho

