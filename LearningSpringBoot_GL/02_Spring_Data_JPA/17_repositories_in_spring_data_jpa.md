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

## 1. Repository kya hota hai?

**Repository** ek layer/interface hoti hai jo database ke saath communication karti hai.

Simple words mein:

> Repository ka kaam hota hai database se data save, fetch, update, delete karna.

### Example

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
}
```

Iske through hum directly methods use kar sakte hain:

```java
userRepository.save(user);
userRepository.findById(1L);
userRepository.findAll();
userRepository.deleteById(1L);
```

### Interview Answer

> Repository is a data access layer in Spring Boot. It is responsible for interacting with the database and performing CRUD operations.

---

## 2. JpaRepository vs CrudRepository

| Point | CrudRepository | JpaRepository |
|---|---|---|
| Purpose | Basic CRUD operations | CRUD + JPA-specific advanced features |
| Methods | save, findById, findAll, delete | All CrudRepository methods + pagination + sorting + batch operations |
| Parent | Base repository | Extends PagingAndSortingRepository and CrudRepository |
| Use case | Simple CRUD | Real-world Spring Boot projects |

### Example using CrudRepository

```java
public interface UserRepository extends CrudRepository<User, Long> {
}
```

### Example using JpaRepository

```java
public interface UserRepository extends JpaRepository<User, Long> {
}
```

**JpaRepository is more powerful.**

### Interview Answer

> CrudRepository provides basic CRUD operations, while JpaRepository provides CRUD plus pagination, sorting, flushing, and batch operations. In most Spring Boot JPA projects, we prefer JpaRepository.

---

## 3. Repository interface ka implementation kaun karta hai?

Repository interface ka implementation **Spring Data JPA automatically runtime par create karta hai**.

Hum sirf interface banate hain:

```java
public interface UserRepository extends JpaRepository<User, Long> {
}
```

Hum implementation class manually nahi banate:

```java
// UserRepositoryImpl manually create karne ki zaroorat nahi hoti
```

Spring internally proxy object banata hai aur methods implement karta hai.

### Interview Answer

> Spring Data JPA provides the implementation automatically at runtime using proxy classes. We only create the repository interface.

Note: **Proxy class** is a runtime-generated helper class created by Spring. It works as a middleman between our code and the actual logic. In Spring Data JPA, we only create repository interfaces, and Spring creates proxy implementations at runtime to handle methods like save, findById, findAll, and delete. Proxy classes are also used for features like transaction management, security, logging, and exception handling.

---

## 4. Repository ko `@Repository` kyun annotate karte hain?

`@Repository` Spring ko batata hai ki ye class/interface **database access layer** ka part hai.

### Benefits

1. Spring isko bean ke form mein manage karta hai.
2. Exception translation hota hai.
3. Code layered architecture follow karta hai.

### Example

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
}
```

### Important Point

> Agar repository interface `JpaRepository` extend kar raha hai, to `@Repository` lagana optional hai, kyunki Spring Data JPA automatically detect kar leta hai.

### Interview Answer

> `@Repository` marks a class as a persistence layer component. It also helps Spring convert database-related exceptions into Spring’s DataAccessException hierarchy. In Spring Data JPA repositories, it is usually optional because Spring detects repository interfaces automatically.

---

## 5. Service layer kyun zaroori hai?

**Service layer business logic handle karti hai.**

Controller ka kaam request/response handle karna hota hai.  
Repository ka kaam database operations karna hota hai.  
Service ka kaam business rules apply karna hota hai.

### Application Flow

```text
Controller → Service → Repository → Database
```

### Example

```java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public User registerUser(User user) {
        // business logic
        if (user.getEmail() == null) {
            throw new RuntimeException("Email required");
        }

        return userRepository.save(user);
    }
}
```

### Service Layer Benefits

| Benefit | Meaning |
|---|---|
| Business logic separation | Logic controller mein mix nahi hota |
| Reusability | Same service multiple controllers use kar sakte hain |
| Testing easy | Service methods ko unit test kar sakte hain |
| Clean architecture | Code maintainable hota hai |
| Transaction management | `@Transactional` service layer mein use hota hai |

### Interview Answer

> Service layer is necessary to keep business logic separate from controller and repository. Controller handles HTTP requests, repository handles database operations, and service handles business rules. It makes the application clean, reusable, testable, and maintainable.

---

# Best Interview Flow Answer

```text
In Spring Boot, we usually follow layered architecture:

Controller layer handles client requests.
Service layer contains business logic.
Repository layer communicates with the database.

Repository interfaces like JpaRepository are implemented automatically by Spring Data JPA at runtime using proxy classes.

CrudRepository provides basic CRUD operations, while JpaRepository provides additional JPA features like pagination, sorting, flushing, and batch operations.

Service layer is important because it separates business logic from controller and repository, making the code clean, reusable, and testable.
```

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

