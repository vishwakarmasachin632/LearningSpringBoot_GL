# MODULE 3 → Topic (g): REST Capstone Project (Industry Ready)

> **Project Name:** Employee Management REST API  
> **Language:** Hinglish  
> **JDK:** 21  
> **Spring Boot:** Latest Stable  
> **Build Tool:** Maven  
> **Database:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ PROJECT OVERVIEW (Theory)

Ye capstone project tumhe **industry-style REST application** banana sikhayega jisme:
- Proper layers honge
- Clean architecture hogi
- Logging, exception handling hogi
- Real-world CRUD APIs hongi

👉 Ye project **resume + interview dono ke liye PERFECT** hai.

---

## 2️⃣ REAL-WORLD SCENARIO

### 🏢 Company: XYZ Tech Pvt Ltd

Requirement:
- Employees ka data manage karna
- Multiple frontend clients (Web / Mobile)
- Secure & scalable REST APIs

Solution:
✅ **Spring Boot REST API (PostgreSQL)**

---

## 3️⃣ COMPLETE FOLDER STRUCTURE (Industry Standard)

```
employee-management-api
 ├── src/main/java
 │   └── com.company.ems
 │       ├── controller
 │       │   └── EmployeeController.java
 │       ├── service
 │       │   ├── EmployeeService.java
 │       │   └── EmployeeServiceImpl.java
 │       ├── repository
 │       │   └── EmployeeRepository.java
 │       ├── entity
 │       │   └── Employee.java
 │       ├── exception
 │       │   ├── ResourceNotFoundException.java
 │       │   └── GlobalExceptionHandler.java
 │       ├── config
 │       │   ├── WebConfig.java
 │       │   └── OpenApiConfig.java
 │       └── EmsApplication.java
 └── src/main/resources
     └── application.yml
```

---

## 4️⃣ ENTITY LAYER

### Employee.java

```java
@Entity
// Purpose: JPA entity define karta hai
// When: DB table map karni ho
// Why here: Employee table chahiye
@Table(name = "employees")
public class Employee {

    @Id
    // Purpose: Primary key
    // Why: Unique employee identification
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;

    private String department;
    private Double salary;
}
```

---

## 5️⃣ REPOSITORY LAYER

```java
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
}
```

---

## 6️⃣ SERVICE LAYER

```java
@Service
// Purpose: Business logic layer
public class EmployeeServiceImpl implements EmployeeService {

    private final EmployeeRepository repository;

    public EmployeeServiceImpl(EmployeeRepository repository) {
        this.repository = repository;
    }

    public Employee save(Employee employee) {
        return repository.save(employee);
    }
}
```

---

## 7️⃣ CONTROLLER LAYER

```java
@RestController
// Purpose: REST APIs expose karta hai
@RequestMapping("/api/employees")
public class EmployeeController {

    private final EmployeeService service;

    public EmployeeController(EmployeeService service) {
        this.service = service;
    }

    @PostMapping
    public Employee create(@RequestBody Employee employee) {
        return service.save(employee);
    }
}
```

---

## 8️⃣ GLOBAL EXCEPTION HANDLING

```java
@RestControllerAdvice
// Purpose: Centralized exception handling
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleNotFound(ResourceNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}
```

---

## 9️⃣ LOGGING (IMPORTANT)

```java
@Slf4j
// Purpose: Logging enable karta hai
public class EmployeeServiceImpl {

    public Employee save(Employee employee) {
        log.info("Saving employee: {}", employee.getName());
        return repository.save(employee);
    }
}
```

---

## 🔟 APPLICATION CONFIG (PostgreSQL)

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/ems_db
    username: postgres
    password: postgres
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
```

---

## 1️⃣1️⃣ PROJECT FLOW (ASCII)

```
Client
  |
  | HTTP JSON Request
  v
Controller
  |
  v
Service (Business Logic)
  |
  v
Repository
  |
  v
PostgreSQL DB
```

---

## 1️⃣2️⃣ INTERVIEW POINTS

- Layered architecture kyun?
- Service layer ka role
- Global exception handling ka fayda
- Logging kyun important

---

## ✅ SUMMARY

✔ Industry-style REST project
✔ Clean architecture
✔ PostgreSQL ready
✔ Resume ready capstone

---

❓ **Should I move to the next topic?**

🔹 MODULE 3 → Topic (h): Self Assessment (30 MCQs)

👉 Sirf **YES** likho.

