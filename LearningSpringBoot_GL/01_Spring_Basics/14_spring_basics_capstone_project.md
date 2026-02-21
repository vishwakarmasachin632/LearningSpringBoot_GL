# 14) Spring Basics – Capstone Project

> **Project Level:** Beginner → Industry Ready  
> **Language:** Hinglish  
> **JDK:** 21  
> **Framework:** Spring Boot (Latest Stable)  
> **Build Tool:** Maven  
> **DB:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 🎯 Project Overview

### Project Name: **Employee Management System (EMS)**

Ye project hum **sirf Spring BASICS** use karke banayenge.

👉 Iska main goal hai:
- Spring Core samajhna
- IoC, DI, AOP, Logging ka real use
- Proper **layered architecture** follow karna

⚠️ Abhi **JPA / REST deep nahi jayenge** – wo next modules me aayega.

---

## 🏗️ Architecture (Industry Standard)

```
Controller  --->  Service  --->  Repository  --->  Database
     |              |               |
     |              |               |
   REST/API      Business        Data Access
```

---

## 📁 Folder Structure

```
ems-spring-basics
 ├── src/main/java
 │   └── com/example/ems
 │       ├── controller
 │       │   └── EmployeeController.java
 │       ├── service
 │       │   └── EmployeeService.java
 │       ├── repository
 │       │   └── EmployeeRepository.java
 │       ├── model
 │       │   └── Employee.java
 │       ├── aop
 │       │   └── LoggingAspect.java
 │       └── EmsApplication.java
 ├── src/main/resources
 │   └── application.properties
 └── pom.xml
```

---

## 1️⃣ pom.xml (Important Dependencies)

```xml
<dependencies>
    <!-- Spring Boot Core -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
    </dependency>

    <!-- Spring Web (Controller layer ke liye) -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- Logging (Default: SLF4J + Logback) -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-logging</artifactId>
    </dependency>
</dependencies>
```

---

## 2️⃣ Main Application Class

```java
@SpringBootApplication
// Purpose: Spring Boot application ka entry point
// Why: Component scan + auto configuration enable karta hai
public class EmsApplication {
    public static void main(String[] args) {
        SpringApplication.run(EmsApplication.class, args);
    }
}
```

---

## 3️⃣ Model Layer (Employee)

```java
public class Employee {
    private int id;
    private String name;
    private String department;

    // getters & setters
}
```

👉 Simple POJO – abhi DB mapping nahi kar rahe.

---

## 4️⃣ Repository Layer

```java
@Repository
// Purpose: Data access layer
// Why: Future me DB se interact karega
public class EmployeeRepository {

    public String save(Employee employee) {
        return "Employee saved successfully";
    }
}
```

---

## 5️⃣ Service Layer

```java
@Service
// Purpose: Business logic layer
// Why: Controller aur Repository ke beech separation
public class EmployeeService {

    private final EmployeeRepository repository;

    // Constructor Injection (BEST PRACTICE)
    public EmployeeService(EmployeeRepository repository) {
        this.repository = repository;
    }

    public String addEmployee(Employee employee) {
        return repository.save(employee);
    }
}
```

---

## 6️⃣ Controller Layer

```java
@RestController
// Purpose: REST API expose karna
// Why: Client requests handle karne ke liye
@RequestMapping("/employees")
public class EmployeeController {

    private final EmployeeService service;

    public EmployeeController(EmployeeService service) {
        this.service = service;
    }

    @PostMapping
    public String addEmployee(@RequestBody Employee employee) {
        return service.addEmployee(employee);
    }
}
```

---

## 7️⃣ AOP – Logging Aspect

```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.ems.service.*.*(..))")
    public void logBefore() {
        System.out.println("Service method called");
    }
}
```

---

## 8️⃣ Logging Configuration

```properties
logging.level.root=INFO
logging.file.name=logs/ems.log
```

---

## 🔄 Complete Flow (ASCII Diagram)

```
Client Request
     |
     v
Controller
     |
     v
Service
     |
     v
Repository
     |
     v
Response
```

---

## 💡 What You Learned From This Project

✔ Spring Boot project structure
✔ IoC & DI real usage
✔ Layered architecture
✔ AOP for logging
✔ Logging configuration
✔ Industry coding style

---

## 🎯 Interview Questions (Capstone Based)

1. Spring Boot project ka flow explain karo
2. Controller, Service, Repository kyun alag hote hain?
3. AOP real project me kaise help karta hai?
4. Constructor injection kyun best hai?
5. Logging production me kyun zaroori hai?

---

## ✅ End of Topic (n)

### 👉 Next Topic?
**MODULE 1 → Topic (o): Spring Basics Assessment (30+ MCQs)**

Likho: **YES**

