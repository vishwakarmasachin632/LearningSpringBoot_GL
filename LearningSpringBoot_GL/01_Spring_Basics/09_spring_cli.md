# 09) Spring CLI (Spring Command Line Interface)

> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Build Tool:** Maven  
> **DB:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ Spring CLI kya hai? (Theory)
Spring CLI (Command Line Interface) ek tool hai jisse hum **terminal/command prompt se directly Spring Boot application** create aur run kar sakte hain — bina IDE open kiye.

### Simple words me:
- CLI = terminal se kaam
- Spring CLI = Spring Boot app ko fast banane ka tool

### Kyun use hota hai?
- POC (Proof of Concept) banana
- Fast demo banana
- Learning & quick experiments

> ⚠️ **Industry note:** Real projects me zyada tar log **Spring Initializr + IDE** use karte hain. CLI knowledge interview + tooling understanding ke liye important hai.

---

## 2️⃣ Real‑World Use Case
**Scenario:**
Tumhe 10–15 minutes me client ko demo dikhana hai ki Spring Boot app kaise run hoti hai.

- IDE open karne ka time nahi
- Bas terminal se app banao
- Run karo
- Endpoint hit karo

👉 Yahan Spring CLI ka use hota hai.

---

## 3️⃣ Spring CLI Install kaise kare?

### Step 1: Java check karo
```bash
java -version
```
Output me **Java 21** dikhna chahiye.

---

### Step 2: Spring CLI download
Official site se **spring-boot-cli** download karo (ZIP).

- Extract karo
- `bin` folder ko **PATH** me add karo

Verify:
```bash
spring --version
```

---

## 4️⃣ Spring CLI se app banana (Practical)

### Step 1: New project folder
```bash
mkdir spring-cli-demo
cd spring-cli-demo
```

---

### Step 2: Spring Boot app create
```bash
spring init --build=maven \
--java-version=21 \
--dependencies=web,data-jpa,postgresql \
--name=cliDemo \
cli-demo
```

### Command explanation:
- `spring init` → project generator
- `--build=maven` → Maven project
- `--java-version=21` → JDK 21
- `--dependencies` → required starters
- `cli-demo` → project folder name

---

## 5️⃣ Generated Project Structure
```
cli-demo
 ├── src
 │   └── main
 │       ├── java
 │       │   └── com/example/clidemo
 │       │       └── CliDemoApplication.java
 │       └── resources
 │           └── application.properties
 ├── pom.xml
 └── mvnw
```

> Same structure jo IntelliJ se banta hai 👍

---

## 6️⃣ Application Run karna (CLI se)

### Method 1: Maven Wrapper
```bash
./mvnw spring-boot:run
```

### Method 2: Build + Run
```bash
./mvnw clean package
java -jar target/*.jar
```

---

## 7️⃣ Simple REST Controller add karo

### File: `HelloController.java`
```java
package com.example.clidemo.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

// @RestController batata hai ki ye class REST API banayegi
// Ye @Controller + @ResponseBody ka combination hai
@RestController
public class HelloController {

    // @GetMapping HTTP GET request ko map karta hai
    // Jab /hello URL hit hoga, ye method chalega
    @GetMapping("/hello")
    public String hello() {
        return "Hello from Spring CLI";
    }
}
```

Test:
```
http://localhost:8080/hello
```

---

## 8️⃣ Spring CLI ka Internal Flow (ASCII Diagram)
```
Developer
   |
   | spring init
   v
Spring CLI
   |
   | Generates project structure
   v
Spring Boot App
   |
   | mvnw spring-boot:run
   v
Embedded Tomcat
   |
   v
REST API Running
```

### Step Explanation:
1. Developer command likhta hai
2. CLI project generate karta hai
3. Maven dependencies download hoti hain
4. Embedded server start hota hai
5. API ready ho jati hai

---

## 9️⃣ Spring CLI vs Spring Initializr

| Feature | Spring CLI | Spring Initializr |
|------|-----------|------------------|
| Usage | Terminal | Browser / IDE |
| Speed | Very Fast | Fast |
| Learning | Medium | Easy |
| Industry | Limited | Widely Used |

---

## 🔟 Common Mistakes
- Java PATH set nahi hota
- Spring CLI install but PATH missing
- Dependency name galat likhna
- CLI ko production tool samajhna

---

## 11️⃣ Interview Questions

1. Spring CLI kya hai?
2. Spring CLI aur Spring Initializr me difference?
3. CLI kab use karte ho?
4. CLI production me kyun kam use hota hai?

---

## ✅ Summary
- Spring CLI = fast project generator
- Learning + demo ke liye best
- Industry me IDE + Initializr zyada popular
- Interview perspective se important

---

### ✅ Next Topic?
**MODULE 1 → Topic (j): Spring Boot Logging**

👉 Likho: **YES**

