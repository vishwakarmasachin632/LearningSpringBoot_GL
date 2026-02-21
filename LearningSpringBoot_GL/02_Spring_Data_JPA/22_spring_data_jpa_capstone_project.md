# 22) Spring Data JPA – Capstone Project (Industry Ready)

> **Module:** 2 (Spring Data JPA)  
> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Framework:** Spring Boot (Latest Stable)  
> **Build Tool:** Maven  
> **Database:** PostgreSQL  
> **Cache:** Redis  
> **IDE:** IntelliJ IDEA

---

## 🎯 Project Overview

### Project Name: **Employee Management System (EMS)**

Real-world inspired project jo companies me **HR / Admin portals** me hota hai.

### Business Features:
- Employee create / update / delete
- Employee fetch (pagination + sorting)
- Department wise search
- Redis cache integration
- Transaction management

---

## 🏗️ Industry Folder Structure

```
ems-service
 └── src/main/java
     └── com.company.ems
         ├── controller
         │    └── EmployeeController.java
         ├── service
         │    └── EmployeeService.java
         ├── repository
         │    └── EmployeeRepository.java
         ├── entity
         │    └── Employee.java
         ├── exception
         │    └── GlobalExceptionHandler.java
         └── EmsApplication.java
```

---

## 1️⃣ Entity Layer

```java
@Entity
// Purpose: Class ko DB table se map karna
// When: JPA use karte ho
// Why: ORM mapping ke liye
@Table(name = "employees")
public class Employee {

    @Id
    // Purpose: Primary key
    // Why: Unique row identify karne ke liye
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;

    private String department;

    private Double salary;
}
```

---

## 2️⃣ Repository Layer

```java
@Repository
// Purpose: Data access layer
// Why: DB operations ke liye
public interface EmployeeRepository extends JpaRepository<Employee, Long> {

    List<Employee> findByDepartment(String department);
}
```

---

## 3️⃣ Service Layer (Transaction + Cache)

```java
@Service
// Purpose: Business logic layer
public class EmployeeService {

    private final EmployeeRepository repo;

    public EmployeeService(EmployeeRepository repo) {
        this.repo = repo;
    }

    @Transactional
    // Purpose: Multiple DB operations safe banana
    @CachePut(value = "employees", key = "#result.id")
    public Employee create(Employee emp) {
        return repo.save(emp);
    }

    @Cacheable(value = "employees", key = "#id")
    public Employee getById(Long id) {
        return repo.findById(id)
                .orElseThrow(() -> new RuntimeException("Employee not found"));
    }

    @CacheEvict(value = "employees", key = "#id")
    public void delete(Long id) {
        repo.deleteById(id);
    }
}
```

---

## 4️⃣ Controller Layer

```java
@RestController
@RequestMapping("/api/employees")
// Purpose: REST APIs expose karna
public class EmployeeController {

    private final EmployeeService service;

    public EmployeeController(EmployeeService service) {
        this.service = service;
    }

    @PostMapping
    public Employee create(@RequestBody Employee emp) {
        return service.create(emp);
    }

    @GetMapping("/{id}")
    public Employee get(@PathVariable Long id) {
        return service.getById(id);
    }

    @DeleteMapping("/{id}")
    public void delete(@PathVariable Long id) {
        service.delete(id);
    }
}
```

---

## 5️⃣ Global Exception Handling

```java
@RestControllerAdvice
// Purpose: Centralized exception handling
public class GlobalExceptionHandler {

    @ExceptionHandler(RuntimeException.class)
    public String handle(RuntimeException ex) {
        return ex.getMessage();
    }
}
```

---

## 🔄 End-to-End Flow (ASCII Diagram)

```
Client
  |
  v
Controller
  |
  v
Service (@Transactional + Cache)
  |
  v
Repository
  |
  v
Hibernate
  |
  v
PostgreSQL
```

---

## ✅ What You Learned (Industry Mapping)

| Concept | Industry Usage |
|------|---------------|
| Entity | DB mapping |
| Repository | Data access |
| Service | Business logic |
| Transaction | Data consistency |
| Cache | Performance |

---

## 🎯 Interview Ready Points
- Layered architecture explain kar sakte ho
- Cache vs DB clearly samajh aa gaya
- Transaction importance clear
- Pagination / sorting already covered

---

### ❓ Next Topic?
**MODULE 2 → Topic (h): Spring Data JPA Assessment (30 MCQs)**

👉 Likho: **YES**

