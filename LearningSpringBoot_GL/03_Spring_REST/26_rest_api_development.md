# MODULE 3 → Topic (c): REST API Development (Spring Boot)

> **Language:** Hinglish (Beginner Friendly)
> **JDK:** 21
> **DB:** PostgreSQL
> **Build Tool:** Maven
> **IDE:** IntelliJ IDEA

---

## 1️⃣ THEORY – REST API Development kya hota hai?

REST API development ka matlab hota hai **client (frontend / mobile / other system)** ko **HTTP endpoints** dena jisse wo **data create, read, update, delete (CRUD)** kar sake.

Simple words me:
- Frontend → request bhejta hai (HTTP)
- Backend (Spring Boot) → process karta hai
- Database → data store / fetch
- Backend → response (JSON) return karta hai

REST API **stateless** hoti hai:
- Har request me complete info hoti hai
- Server client ka state yaad nahi rakhta

---

## 2️⃣ REAL-WORLD USE CASE

### 🎯 Use Case: Employee Management System (EMS)

Company ke paas:
- Web App (React)
- Mobile App (Android / iOS)

Dono ko same backend chahiye:
- Employee add
- Employee list
- Employee update
- Employee delete

➡️ Solution: **REST APIs using Spring Boot**

---

## 3️⃣ PROJECT STRUCTURE (Industry Standard)

```
employee-management
 └── src/main/java
     └── com.company.ems
         ├── controller
         │    └── EmployeeController.java
         ├── service
         │    ├── EmployeeService.java
         │    └── EmployeeServiceImpl.java
         ├── repository
         │    └── EmployeeRepository.java
         ├── entity
         │    └── Employee.java
         ├── exception
         │    └── ResourceNotFoundException.java
         └── EmsApplication.java
```

---

## 4️⃣ ENTITY LAYER

### Employee.java

```java
package com.company.ems.entity;

import jakarta.persistence.*;

// @Entity
// Purpose: Batata hai ki ye class database table se mapped hai
// When: Jab bhi JPA/Hibernate use karte ho
// Why here: Employee table create karni hai
@Entity

// @Table
// Purpose: Table ka naam define karta hai
// When: Custom table name chahiye
// Why here: "employees" naam ka table chahiye
@Table(name = "employees")
public class Employee {

    // @Id
    // Purpose: Primary key define karta hai
    // When: Har entity me mandatory
    // Why here: Employee ka unique identifier
    @Id

    // @GeneratedValue
    // Purpose: Auto increment value generate karta hai
    // When: ID DB se generate karani ho
    // Why here: Manual ID nahi chahiye
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    // @Column
    // Purpose: Column mapping
    // When: Column constraints define karni ho
    // Why here: Name blank nahi ho sakta
    @Column(nullable = false)
    private String name;

    private String department;
    private Double salary;

    // getters & setters
}
```

---

## 5️⃣ REPOSITORY LAYER

### EmployeeRepository.java

```java
package com.company.ems.repository;

import com.company.ems.entity.Employee;
import org.springframework.data.jpa.repository.JpaRepository;

// JpaRepository
// Purpose: CRUD + pagination + sorting ready methods
// When: Database operations chahiye
// Why here: Employee table access karna hai
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
}
```

---

## 6️⃣ SERVICE LAYER

### EmployeeService.java

```java
package com.company.ems.service;

import com.company.ems.entity.Employee;
import java.util.List;

public interface EmployeeService {
    Employee save(Employee employee);
    List<Employee> findAll();
    Employee findById(Long id);
    Employee update(Long id, Employee employee);
    void delete(Long id);
}
```

### EmployeeServiceImpl.java

```java
package com.company.ems.service;

import com.company.ems.entity.Employee;
import com.company.ems.repository.EmployeeRepository;
import com.company.ems.exception.ResourceNotFoundException;
import org.springframework.stereotype.Service;

import java.util.List;

// @Service
// Purpose: Business logic layer batata hai
// When: Service class ho
// Why here: Controller aur Repository ke beech logic
@Service
public class EmployeeServiceImpl implements EmployeeService {

    private final EmployeeRepository repository;

    // Constructor Injection
    public EmployeeServiceImpl(EmployeeRepository repository) {
        this.repository = repository;
    }

    @Override
    public Employee save(Employee employee) {
        return repository.save(employee);
    }

    @Override
    public List<Employee> findAll() {
        return repository.findAll();
    }

    @Override
    public Employee findById(Long id) {
        return repository.findById(id)
                .orElseThrow(() -> new ResourceNotFoundException("Employee not found"));
    }

    @Override
    public Employee update(Long id, Employee employee) {
        Employee existing = findById(id);
        existing.setName(employee.getName());
        existing.setDepartment(employee.getDepartment());
        existing.setSalary(employee.getSalary());
        return repository.save(existing);
    }

    @Override
    public void delete(Long id) {
        repository.delete(findById(id));
    }
}
```

---

## 7️⃣ CONTROLLER LAYER

### EmployeeController.java

```java
package com.company.ems.controller;

import com.company.ems.entity.Employee;
import com.company.ems.service.EmployeeService;
import org.springframework.web.bind.annotation.*;

import java.util.List;

// @RestController
// Purpose: REST API expose karta hai
// When: JSON based API chahiye
// Why here: Employee APIs banani hain
@RestController

// @RequestMapping
// Purpose: Base URL define karta hai
// When: Common path chahiye
// Why here: /api/employees
@RequestMapping("/api/employees")
public class EmployeeController {

    private final EmployeeService service;

    public EmployeeController(EmployeeService service) {
        this.service = service;
    }

    // @PostMapping
    // Purpose: Create resource
    // When: Data save karna ho
    // Why here: New employee add
    @PostMapping
    public Employee create(@RequestBody Employee employee) {
        return service.save(employee);
    }

    // @GetMapping
    // Purpose: Read resource
    // When: Data fetch karna ho
    // Why here: Employee list
    @GetMapping
    public List<Employee> getAll() {
        return service.findAll();
    }

    @GetMapping("/{id}")
    public Employee getById(@PathVariable Long id) {
        return service.findById(id);
    }

    // @PutMapping
    // Purpose: Update resource
    // When: Existing data update
    // Why here: Employee update
    @PutMapping("/{id}")
    public Employee update(@PathVariable Long id, @RequestBody Employee employee) {
        return service.update(id, employee);
    }

    // @DeleteMapping
    // Purpose: Delete resource
    // When: Data remove karna ho
    // Why here: Employee delete
    @DeleteMapping("/{id}")
    public void delete(@PathVariable Long id) {
        service.delete(id);
    }
}
```

---

## 8️⃣ EXCEPTION HANDLING

```java
package com.company.ems.exception;

public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
```

---

## 9️⃣ FLOW DIAGRAM (ASCII)

```
Client (Browser / App)
        |
        | HTTP Request (JSON)
        v
EmployeeController
        |
        v
EmployeeService
        |
        v
EmployeeRepository
        |
        v
PostgreSQL Database
        |
        v
JSON Response
```

---

## 🔟 INTERVIEW POINTS

- REST API stateless hoti hai
- Controller sirf request/response handle karta hai
- Business logic Service me hota hai
- Repository sirf DB access karta hai
- Proper layers = maintainable + testable code

---

## ✅ SUMMARY

✔ Industry standard REST API
✔ Proper layering
✔ PostgreSQL ready
✔ Java 21 compatible
✔ Interview + project ready

---

**Next confirmation required**

