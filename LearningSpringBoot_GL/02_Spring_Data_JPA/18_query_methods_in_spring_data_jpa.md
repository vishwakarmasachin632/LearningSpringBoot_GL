# 18) Query Methods in Spring Data JPA

> **Module:** 2 (Spring Data JPA)  
> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Framework:** Spring Boot (Latest Stable)  
> **Build Tool:** Maven  
> **Database:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ Query Methods kya hote hain? (Theory)
Query Methods wo methods hote hain jo **method name se hi SQL/JPA query generate** kar dete hain.

👉 Matlab: **SQL likhne ki zarurat nahi**, sirf proper method naming follow karo.

Example:
```java
findByDepartment(String dept)
```
Spring khud samajh jaata hai:
```sql
SELECT * FROM employees WHERE department = ?
```

---

## 2️⃣ Real-World Use Case
**HR Management System** me:
- Department wise employees nikalna
- Salary ke basis pe filter
- Active / Inactive users fetch karna

Industry me:
> 70–80% queries **Query Methods** se hi handle ho jaati hain.

---

## 3️⃣ Query Method ka Syntax Rule (VERY IMPORTANT)

```
findBy + FieldName + Condition
```

Examples:
- findByName
- findByDepartment
- findBySalaryGreaterThan

⚠️ Field name **Entity ke variable ke exact name** se match hona chahiye.

---

## 4️⃣ Entity (Reference)
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

    private Double salary;
}
```

---

## 5️⃣ Common Query Methods Examples

### 🔹 Equality
```java
List<Employee> findByDepartment(String department);
```

### 🔹 AND / OR
```java
List<Employee> findByDepartmentAndSalary(String dept, Double salary);
List<Employee> findByDepartmentOrSalary(String dept, Double salary);
```

---

### 🔹 Comparison
```java
List<Employee> findBySalaryGreaterThan(Double salary);
List<Employee> findBySalaryLessThan(Double salary);
```

---

### 🔹 LIKE / Contains
```java
List<Employee> findByNameContaining(String keyword);
```

SQL:
```sql
WHERE name LIKE %keyword%
```

---

### 🔹 IN Query
```java
List<Employee> findByDepartmentIn(List<String> departments);
```

---

## 6️⃣ Sorting ke saath Query Method
```java
List<Employee> findByDepartmentOrderBySalaryDesc(String department);
```

---

## 7️⃣ Query Method with Boolean
```java
List<Employee> findByActiveTrue();
List<Employee> findByActiveFalse();
```

---

## 8️⃣ Repository Interface Example
```java
@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {

    List<Employee> findByDepartment(String department);

    List<Employee> findBySalaryGreaterThan(Double salary);

    List<Employee> findByNameContaining(String keyword);
}
```

---

## 9️⃣ Service Layer Usage
```java
@Service
public class EmployeeService {

    private final EmployeeRepository repository;

    public EmployeeService(EmployeeRepository repository) {
        this.repository = repository;
    }

    public List<Employee> getByDepartment(String dept) {
        return repository.findByDepartment(dept);
    }
}
```

---

## 🔟 Flow Diagram (ASCII)

```
Controller
  |
  v
Service
  |
  v
Query Method (Repository)
  |
  v
Hibernate → PostgreSQL
```

---

## 1️⃣1️⃣ When NOT to use Query Methods?
❌ Very complex joins
❌ Huge dynamic conditions

👉 Aise cases me:
- @Query (JPQL)
- Criteria API

---

## 1️⃣2️⃣ Common Mistakes
❌ Field name mismatch
❌ Wrong return type
❌ Typo in method name
❌ Using DB column name instead of entity field name

---

# 1️⃣3️⃣ Interview Questions: Spring Data JPA Query Methods

## 1. Query method kya hota hai?

**Query Method** Spring Data JPA ka ek feature hai jisme hum method name ke basis par database query create kar sakte hain.

Simple words mein:

> Query method ka matlab hai method name likho, aur Spring Data JPA automatically SQL/JPQL query bana deta hai.

### Example

```java
public interface UserRepository extends JpaRepository<User, Long> {

    User findByEmail(String email);
}
```

Yahan humne manually query nahi likhi.

Spring Data JPA method name `findByEmail` ko read karega aur internally query banayega:

```sql
SELECT * FROM users WHERE email = ?;
```

### Interview Answer

> Query method is a feature of Spring Data JPA where queries are created automatically based on repository method names. We only define the method name, and Spring Data JPA generates the query at runtime.

---

## 2. Method name kaise query banata hai?

Spring Data JPA method name ko parse karta hai.

Example:

```java
User findByEmail(String email);
```

Spring is method ko parts mein read karta hai:

```text
findBy + Email
```

| Part | Meaning |
|---|---|
| `findBy` | Data fetch karna hai |
| `Email` | Entity ka field name |
| `String email` | Search value |

Agar entity mein field hai:

```java
@Entity
public class User {

    @Id
    private Long id;

    private String email;
}
```

To Spring Data JPA query banayega:

```sql
SELECT * FROM users WHERE email = ?;
```

### More Examples

```java
List<User> findByName(String name);
```

SQL meaning:

```sql
SELECT * FROM users WHERE name = ?;
```

```java
List<User> findByAgeGreaterThan(int age);
```

SQL meaning:

```sql
SELECT * FROM users WHERE age > ?;
```

```java
List<User> findByNameAndEmail(String name, String email);
```

SQL meaning:

```sql
SELECT * FROM users WHERE name = ? AND email = ?;
```

```java
List<User> findByNameOrEmail(String name, String email);
```

SQL meaning:

```sql
SELECT * FROM users WHERE name = ? OR email = ?;
```

### Interview Answer

> Spring Data JPA creates queries by parsing the repository method name. Keywords like findBy, And, Or, GreaterThan, LessThan, Containing, StartingWith, and EndingWith are used to generate database queries automatically.

---

## 3. `findBy` vs `getBy`

`findBy` aur `getBy` dono repository method prefixes hain, lekin unka behavior alag ho sakta hai.

---

### `findBy`

`findBy` usually database se data search karta hai.

Example:

```java
Optional<User> findById(Long id);
User findByEmail(String email);
```

Agar data nahi mila, to mostly `null` ya `Optional.empty()` return hota hai, return type ke according.

Example:

```java
Optional<User> user = userRepository.findById(1L);
```

---

### `getBy`

`getBy` usually reference/proxy object return kar sakta hai, especially ID based methods mein.

Example:

```java
User user = userRepository.getById(1L);
```

Important:

> `getById()` immediately database hit nahi karta. Ye lazy proxy return kar sakta hai. Jab actual data access karte hain tab query execute hoti hai.

Example:

```java
User user = userRepository.getById(1L);

// Database query yahan execute ho sakti hai
System.out.println(user.getName());
```

### Difference Table

| Point | findBy | getBy |
|---|---|---|
| Purpose | Data find/search karna | Reference/proxy object lana |
| DB hit | Usually immediately query execute karta hai | Lazy proxy return kar sakta hai |
| Not found case | `Optional.empty()` ya `null` | Data access karne par exception aa sakti hai |
| Common use | Safe searching | Lazy reference loading |
| Recommended | Most cases mein preferred | Carefully use karna chahiye |

### Important Note

Modern Spring Data JPA mein `getById()` deprecated ho chuka hai.  
Uski jagah usually `getReferenceById()` use hota hai.

```java
User user = userRepository.getReferenceById(1L);
```

### Interview Answer

> `findBy` is used to search and fetch data from the database, usually executing the query immediately. `getBy` or `getReferenceById` can return a lazy proxy reference and may hit the database only when the object data is accessed. In most cases, `findBy` is safer and commonly used.

---

## 4. LIKE query kaise likhte hain?

LIKE query ka use partial matching ke liye hota hai.

SQL mein LIKE query:

```sql
SELECT * FROM users WHERE name LIKE '%raj%';
```

Spring Data JPA mein LIKE query likhne ke multiple ways hain.

---

### Method 1: `Containing`

```java
List<User> findByNameContaining(String name);
```

Usage:

```java
userRepository.findByNameContaining("raj");
```

SQL meaning:

```sql
SELECT * FROM users WHERE name LIKE '%raj%';
```

---

### Method 2: `StartingWith`

```java
List<User> findByNameStartingWith(String prefix);
```

Usage:

```java
userRepository.findByNameStartingWith("Sa");
```

SQL meaning:

```sql
SELECT * FROM users WHERE name LIKE 'Sa%';
```

---

### Method 3: `EndingWith`

```java
List<User> findByNameEndingWith(String suffix);
```

Usage:

```java
userRepository.findByNameEndingWith("in");
```

SQL meaning:

```sql
SELECT * FROM users WHERE name LIKE '%in';
```

---

### Method 4: `Like`

```java
List<User> findByNameLike(String pattern);
```

Usage:

```java
userRepository.findByNameLike("%raj%");
```

SQL meaning:

```sql
SELECT * FROM users WHERE name LIKE '%raj%';
```

Important:

> `Like` use karte time `%` manually pass karna padta hai.

---

### Method 5: `IgnoreCase`

Case-insensitive search ke liye:

```java
List<User> findByNameContainingIgnoreCase(String name);
```

Usage:

```java
userRepository.findByNameContainingIgnoreCase("RAJ");
```

Ye `raj`, `Raj`, `RAJ` sab match kar sakta hai.

### Interview Answer

> LIKE query in Spring Data JPA can be written using keywords like Containing, StartingWith, EndingWith, Like, and IgnoreCase. For example, `findByNameContaining("raj")` works like SQL `LIKE '%raj%'`.

---

## 5. Query Methods ki limitation kya hai?

Query methods simple queries ke liye best hote hain, lekin complex queries ke liye limitations hoti hain.

### Limitations

| Limitation | Explanation |
|---|---|
| Long method names | Complex conditions mein method name bahut bada ho jata hai |
| Complex joins difficult | Multiple tables join karna difficult ho sakta hai |
| Dynamic filters difficult | Runtime par optional filters handle karna hard hota hai |
| Custom query control kam | Exact SQL/JPQL control nahi milta |
| Readability issue | Long names samajhna difficult ho jata hai |
| Aggregation difficult | GROUP BY, COUNT, SUM jaise queries ke liye better option chahiye |

### Example of long method name

```java
List<User> findByNameContainingIgnoreCaseAndAgeGreaterThanAndStatusAndCityOrderByCreatedAtDesc(
    String name,
    int age,
    String status,
    String city
);
```

Ye method kaam karega, but readable nahi hai.

Better option:

```java
@Query("SELECT u FROM User u WHERE u.name LIKE %:name% AND u.age > :age")
List<User> searchUsers(@Param("name") String name, @Param("age") int age);
```

### Better alternatives for complex queries

| Situation | Better Option |
|---|---|
| Simple query | Query Method |
| Custom JPQL query | `@Query` |
| Complex dynamic filters | Specification API |
| Very complex SQL | Native Query |
| Type-safe query building | QueryDSL |

### Interview Answer

> Query methods are useful for simple queries, but they have limitations in complex scenarios. Method names can become very long and unreadable. Complex joins, dynamic filters, grouping, aggregation, and custom SQL logic are difficult with query methods. For complex cases, we use `@Query`, Specification API, QueryDSL, or native queries.

---

# Common Query Method Keywords

| Keyword | Example | Meaning |
|---|---|---|
| `findBy` | `findByEmail` | Find by field |
| `And` | `findByNameAndEmail` | Both conditions |
| `Or` | `findByNameOrEmail` | Either condition |
| `GreaterThan` | `findByAgeGreaterThan` | Greater than |
| `LessThan` | `findByAgeLessThan` | Less than |
| `Between` | `findByAgeBetween` | Between two values |
| `Containing` | `findByNameContaining` | LIKE `%value%` |
| `StartingWith` | `findByNameStartingWith` | LIKE `value%` |
| `EndingWith` | `findByNameEndingWith` | LIKE `%value` |
| `IgnoreCase` | `findByNameIgnoreCase` | Case-insensitive |
| `OrderBy` | `findByStatusOrderByCreatedAtDesc` | Sorting |
| `IsNull` | `findByDeletedAtIsNull` | Field is null |
| `IsNotNull` | `findByDeletedAtIsNotNull` | Field is not null |
| `True` | `findByActiveTrue` | Boolean true |
| `False` | `findByActiveFalse` | Boolean false |

---

# Best Interview Flow Answer

```text
Spring Data JPA query methods allow us to create database queries by simply defining method names in repository interfaces.

For example, findByEmail generates a query based on the email field.

Spring parses method names using keywords like findBy, And, Or, Containing, StartingWith, EndingWith, GreaterThan, and LessThan.

findBy is generally used to fetch data directly, while getBy or getReferenceById may return a lazy proxy reference.

LIKE queries can be written using Containing, StartingWith, EndingWith, Like, and IgnoreCase.

Query methods are good for simple queries, but for complex joins, dynamic filters, grouping, and custom SQL logic, we use @Query, Specification API, QueryDSL, or native queries.
```

---

## ✅ Summary
- Query Methods = Zero SQL
- Fast development
- Clean & readable code
- Most used feature of Spring Data JPA

---

### ❓ Next Topic?
**MODULE 2 → Topic (d): Transaction Management**

👉 Likho: **YES**

