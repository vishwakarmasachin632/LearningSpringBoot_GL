# 20) Pagination & Sorting in Spring Data JPA

> **Module:** 2 (Spring Data JPA)  
> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Framework:** Spring Boot (Latest Stable)  
> **Build Tool:** Maven  
> **Database:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ Pagination kya hoti hai? (Theory)
Pagination ka matlab hota hai **large data ko chhote-chhote pages me todna**.

Example:
- Total employees = 1,00,000
- Ek page = 20 records

👉 Client bolega: *page 3 dikhao*

---

## 2️⃣ Real-World Use Case
- Admin dashboards
- E‑commerce product listing
- HR employee listing

Without pagination:
❌ Slow response  
❌ High memory usage

---

## 3️⃣ Spring Data JPA Pagination Support
Spring Data JPA me:
- `Pageable` → pagination info
- `Page<T>` → result + metadata

---

## 4️⃣ Pageable Interface
```java
Pageable pageable = PageRequest.of(pageNumber, pageSize);
```

### Parameters:
- pageNumber → 0 se start hota hai
- pageSize → ek page me kitne records

---

## 5️⃣ Repository me Pagination

```java
@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {

    Page<Employee> findAll(Pageable pageable);
}
```

> Note: Ye method **JpaRepository already provide karta hai**.

---

## 6️⃣ Service Layer Implementation

```java
@Service
public class EmployeeService {

    private final EmployeeRepository repo;

    public EmployeeService(EmployeeRepository repo) {
        this.repo = repo;
    }

    public Page<Employee> getEmployees(int page, int size) {
        Pageable pageable = PageRequest.of(page, size);
        return repo.findAll(pageable);
    }
}
```

---

## 7️⃣ Controller Example

```java
@RestController
@RequestMapping("/employees")
public class EmployeeController {

    private final EmployeeService service;

    public EmployeeController(EmployeeService service) {
        this.service = service;
    }

    @GetMapping
    public Page<Employee> list(
            @RequestParam(defaultValue = "0") int page,
            @RequestParam(defaultValue = "10") int size) {
        return service.getEmployees(page, size);
    }
}
```

---

## 8️⃣ Sorting in Spring Data JPA
Sorting ka matlab hota hai **order by**.

Example:
- Salary descending
- Name ascending

---

## 9️⃣ Sorting Example

```java
Sort sort = Sort.by("salary").descending();
Pageable pageable = PageRequest.of(page, size, sort);
```

---

## 🔟 Pagination + Sorting Combined

```java
Pageable pageable = PageRequest.of(page, size,
        Sort.by("salary").descending());
```

---

## 1️⃣1️⃣ Page Object ka Fayda

```java
Page<Employee> page = repo.findAll(pageable);

page.getContent();      // actual data
page.getTotalPages();   // total pages
page.getTotalElements();// total records
page.isLast();          // last page or not
```

---

## 1️⃣2️⃣ Flow Diagram (ASCII)

```
Client
  |
  v
Controller (page,size)
  |
  v
Service
  |
  v
JpaRepository
  |
  v
PostgreSQL (LIMIT / OFFSET)
```

---

## 1️⃣3️⃣ Common Mistakes
❌ Page index 1 se start karna
❌ Very large page size
❌ Sorting field typo

---

## 1️⃣4️⃣ Interview Questions
1. Pagination kyun zaroori hai?
2. Pageable vs Page
3. PageRequest.of parameters
4. Sorting kaise karte hain?
5. LIMIT / OFFSET ka role

---

## ✅ Summary
- Pagination improves performance
- Pageable = request
- Page = response
- Sorting easily integrate hoti hai

---

### ❓ Next Topic?
**MODULE 2 → Topic (f): Redis Cache Integration**

👉 Likho: **YES**

