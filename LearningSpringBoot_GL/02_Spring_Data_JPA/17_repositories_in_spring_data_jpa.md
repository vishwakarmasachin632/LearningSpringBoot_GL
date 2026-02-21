# 17) Repositories in Spring Data JPA

> **Module:** 2 (Spring Data JPA)  
> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Framework:** Spring Boot (Latest Stable)  
> **Build Tool:** Maven  
> **Database:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ Repository kya hota hai? (Theory)
Repository **Data Access Layer** hoti hai jo database se baat karti hai.

Simple words me:
> Service bolegi **kya kaam chahiye**, Repository handle karegi **DB kaise**.

Spring Data JPA me Repository **interface** hoti hai — implementation Spring khud banata hai.

---

## 2️⃣ Problem Without Spring Data Repositories
- CRUD ke liye bohot saara boilerplate code
- SQL likho → map karo → exception handle karo

❌ Time waste  
❌ Error-prone

---

## 3️⃣ Spring Data Repository ka Fayda
- CRUD methods **out-of-the-box**
- No implementation class required
- Pagination, sorting built-in

👉 Tum sirf **interface** likhte ho.

---

## 4️⃣ Repository Hierarchy (VERY IMPORTANT)

```
Repository (Marker Interface)
   |
   +-- CrudRepository
   |
   +-- PagingAndSortingRepository
   |
   +-- JpaRepository   ⭐ MOST USED
```

### Kab kaunsa use kare?
- `CrudRepository` → Basic CRUD
- `PagingAndSortingRepository` → Pagination + Sorting
- `JpaRepository` → CRUD + Paging + Batch + Flush (Best choice)

---

## 5️⃣ JpaRepository kyun BEST hai?
`JpaRepository` already include karta hai:
- save(), findById(), findAll()
- delete(), count()
- pagination & sorting

👉 99% projects me **JpaRepository** hi use hota hai.

---

## 6️⃣ Practical: Repository Interface Banana

### Step 1: Entity (Recap)
```java
@Entity
@Table(name = "employees")
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;

    private String department;
}
```

---

### Step 2: Repository Interface
```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
// Purpose: Spring ko batata hai ye data access layer hai
// When: JPA repositories ke liye
// Why here: Exception translation + clarity
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
    // No code needed
}
```

### Important Points:
- `Employee` → Entity class
- `Long` → Primary key type
- Implementation Spring auto-generate karega

---

## 7️⃣ Repository ko Service me Use karna

```java
@Service
// Purpose: Business logic layer
public class EmployeeService {

    private final EmployeeRepository repository;

    // Constructor Injection (BEST PRACTICE)
    public EmployeeService(EmployeeRepository repository) {
        this.repository = repository;
    }

    public Employee save(Employee emp) {
        return repository.save(emp);
    }

    public List<Employee> getAll() {
        return repository.findAll();
    }
}
```

---

## 8️⃣ End-to-End Flow (ASCII Diagram)

```
Client
  |
  v
Controller
  |
  v
Service
  |
  v
JpaRepository
  |
  v
Hibernate
  |
  v
PostgreSQL
```

---

## 9️⃣ Common Mistakes
❌ Repository ko class banana (interface hona chahiye)
❌ Wrong ID type
❌ Entity annotation missing
❌ Multiple DB configs

---

## 🔟 Interview Questions

1. Repository kya hota hai?
2. JpaRepository vs CrudRepository
3. Repository interface ka implementation kaun karta hai?
4. Repository ko @Repository kyun annotate karte hain?
5. Service layer kyun zaroori hai?

---

## ✅ Summary
- Repository = Data access layer
- Spring Data JPA implementation khud banata hai
- JpaRepository most powerful & commonly used
- Clean & maintainable architecture

---

### ✅ Next Topic?
**MODULE 2 → Topic (c): Query Methods**

👉 Likho: **YES**

