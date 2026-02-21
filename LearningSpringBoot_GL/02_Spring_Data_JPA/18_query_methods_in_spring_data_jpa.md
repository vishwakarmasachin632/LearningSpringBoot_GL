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

## 1️⃣3️⃣ Interview Questions
1. Query method kya hota hai?
2. Method name kaise query banata hai?
3. findBy vs getBy
4. LIKE query kaise likhte hain?
5. Query Methods ki limitation kya hai?

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

