# 19) Transaction Management in Spring Data JPA

> **Module:** 2 (Spring Data JPA)  
> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Framework:** Spring Boot (Latest Stable)  
> **Build Tool:** Maven  
> **Database:** PostgreSQL  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ Transaction kya hota hai? (Theory)
Transaction ka matlab hota hai **operations ka ek atomic unit**.

Simple shabdon me:
> Ya to **saare steps successful**, ya **ek bhi nahi**.

Example:
- Bank transfer: Debit + Credit
- Agar debit ho gaya aur credit fail → **rollback**

---

## 2️⃣ Real-World Use Case
**Salary Processing System**:
- Employee salary update
- Audit table me entry

Dono ka ek transaction hona zaroori hai.

---

## 3️⃣ ACID Properties (VERY IMPORTANT)

- **A – Atomicity** → All or nothing
- **C – Consistency** → Valid state
- **I – Isolation** → Parallel transactions safe
- **D – Durability** → Commit ke baad data safe

---

## 4️⃣ Spring Transaction Management ka Role
Spring:
- Transaction start karta hai
- Commit / Rollback manage karta hai
- Developer ko boilerplate se bachata hai

👉 Ye kaam mostly **@Transactional** karta hai.

---

## 5️⃣ @Transactional Annotation

```java
@Transactional
```

### Purpose:
- Method ko transaction boundary banana

### When to use:
- Multiple DB operations ek logical unit ho

### Why needed here:
- Failure par automatic rollback

---

## 6️⃣ @Transactional ka Placement

### 🔹 Service Layer (BEST PRACTICE)
```java
@Service
public class SalaryService {

    private final EmployeeRepository repo;

    public SalaryService(EmployeeRepository repo) {
        this.repo = repo;
    }

    @Transactional
    // Purpose: Salary update + audit insert ko ek transaction banana
    // When: Multiple DB operations
    // Why: Partial data avoid karne ke liye
    public void updateSalary(Long id, Double amount) {
        Employee emp = repo.findById(id).orElseThrow();
        emp.setSalary(amount);
        repo.save(emp);

        // maan lo yaha exception aayi
        // to salary update rollback ho jayega
    }
}
```

❌ Controller layer me generally avoid karte hain.

---

## 7️⃣ Rollback Rules
Default behavior:
- **RuntimeException / Error** → Rollback
- **Checked Exception** → Commit

### Force Rollback
```java
@Transactional(rollbackFor = Exception.class)
```

---

## 8️⃣ Read-Only Transaction
```java
@Transactional(readOnly = true)
```

### Use Case:
- Fetch only queries
- Performance improve hoti hai

---

## 9️⃣ Transaction Propagation (Conceptual)

- REQUIRED (default)
- REQUIRES_NEW
- SUPPORTS

👉 Mostly **REQUIRED** hi use hota hai.

---

## 🔟 Flow Diagram (ASCII)

```
Controller
  |
  v
Service (@Transactional)
  |
  v
Repository
  |
  v
PostgreSQL

[Exception]
   |
Rollback
```

---

## 1️⃣1️⃣ Common Mistakes
❌ @Transactional on private methods
❌ Self-invocation
❌ Using it on controller

---

## 1️⃣2️⃣ Interview Questions
1. Transaction kya hota hai?
2. @Transactional kab use karte hain?
3. Default rollback behavior kya hai?
4. readOnly transaction ka fayda?
5. Service layer me kyu lagate hain?

---

## ✅ Summary
- Transaction = data consistency
- @Transactional core annotation
- Service layer is best place
- Avoid partial updates

---

### ❓ Next Topic?
**MODULE 2 → Topic (e): Pagination & Sorting**

👉 Likho: **YES**

