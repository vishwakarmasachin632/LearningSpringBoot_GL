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
# 3️⃣ ACID Properties in DBMS / Transaction Management

ACID properties are very important in database transactions.

ACID stands for:

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

These properties make sure that database transactions are safe, reliable, and consistent.

---

## A – Atomicity

### Meaning

Atomicity means:

> All operations in a transaction should complete successfully, or none should happen.

Simple words:

> All or nothing.

---

### Example

Bank transfer:

```text
Account A se ₹1000 debit
Account B me ₹1000 credit
```

Both operations should happen together.

If debit is successful but credit fails, then the debit should also be rolled back.

---

### Without Atomicity Problem

```text
Account A debited
Account B not credited
```

This creates wrong data.

---

### With Atomicity

```text
Debit successful + Credit successful = Commit
Debit successful + Credit failed = Rollback
```

---

### Interview Answer

> Atomicity means a transaction is treated as a single unit. Either all operations are completed successfully, or none of them are applied. It follows the all-or-nothing rule.

---

## C – Consistency

### Meaning

Consistency means:

> A transaction should move the database from one valid state to another valid state.

Simple words:

> Data should always remain correct and valid.

---

### Example

Suppose account balance cannot be negative.

```text
Account balance = ₹500
Withdraw amount = ₹1000
```

This transaction should not be allowed because it breaks the rule.

---

### Why Consistency is Important?

Consistency makes sure that:

- Database rules are followed
- Constraints are maintained
- Invalid data is not saved
- Data remains accurate

---

### Interview Answer

> Consistency means a transaction should keep the database in a valid state before and after execution. It ensures that all rules, constraints, and validations are properly maintained.

---

## I – Isolation

### Meaning

Isolation means:

> Multiple transactions running at the same time should not affect each other incorrectly.

Simple words:

> Parallel transactions should be safe.

---

### Example

Two users are booking the last ticket at the same time.

```text
User A tries to book ticket
User B also tries to book same ticket
```

Isolation ensures that only one user gets the ticket.

---

### Without Isolation Problem

```text
Same ticket booked by two users
```

This creates data inconsistency.

---

### With Isolation

```text
Only one transaction succeeds
Other transaction waits or fails
```

---

### Interview Answer

> Isolation means multiple transactions can run at the same time without interfering with each other. It ensures that parallel transactions produce correct and consistent results.

---

## D – Durability

### Meaning

Durability means:

> Once a transaction is committed, the data should be permanently saved.

Simple words:

> Commit ke baad data safe.

---

### Example

If money transfer is successful and transaction is committed:

```text
Account A debited
Account B credited
Transaction committed
```

Now even if the system crashes, the committed data should not be lost.

---

### Why Durability is Important?

Durability ensures:

- Committed data is permanently stored
- System crash ke baad bhi data safe rahe
- Database recovery possible ho
- User ka saved data lost na ho

---

### Interview Answer

> Durability means once a transaction is committed, the changes are permanently saved in the database. Even if the system crashes after commit, the committed data should remain safe.

---

# ACID Properties Summary Table

| Property | Meaning | Simple Line |
|---|---|---|
| Atomicity | Complete transaction or nothing | All or nothing |
| Consistency | Database remains valid | Valid state |
| Isolation | Transactions do not disturb each other | Parallel transactions safe |
| Durability | Committed data is permanent | Commit ke baad data safe |

---

# Real-Life Example of ACID

Bank money transfer:

```text
Transfer ₹1000 from Account A to Account B
```

| ACID Property | Role |
|---|---|
| Atomicity | Debit and credit both should happen, otherwise rollback |
| Consistency | Balance should not become invalid |
| Isolation | Two transfers should not corrupt account balance |
| Durability | After successful transfer, data should remain saved |

---

# Best Interview Answer

```text
ACID properties are used to make database transactions reliable and safe.

Atomicity means all operations in a transaction should complete successfully, or none should happen.

Consistency means the database should move from one valid state to another valid state.

Isolation means multiple transactions running at the same time should not interfere with each other.

Durability means once a transaction is committed, the data should be permanently saved even if the system crashes.
```

---

# One-line Answer

> ACID properties ensure that database transactions are reliable, consistent, safe during parallel execution, and permanently saved after commit.

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

# 1️⃣2️⃣ Interview Questions: Spring Transaction Management

## 1. Transaction kya hota hai?

**Transaction** ek group of database operations hota hai jo ek single unit ke form mein execute hota hai.

Simple words mein:

> Transaction ka matlab hai database ke multiple operations ko ek saath safely execute karna.

Agar sab operations successful hote hain, to transaction **commit** hota hai.  
Agar koi error aata hai, to transaction **rollback** hota hai.

---

## Real-Life Example

Bank transfer example:

```text
Account A se ₹1000 debit karo
Account B me ₹1000 credit karo
```

Dono operations successful hone chahiye.

Agar debit ho gaya but credit fail ho gaya, to problem ho jayegi.

Isliye transaction use hota hai:

```text
Debit successful + Credit successful = Commit
Debit successful + Credit failed = Rollback
```

---

## Transaction Example

```java
@Service
public class PaymentService {

    @Transactional
    public void transferMoney(Long fromAccount, Long toAccount, Double amount) {

        // Step 1: Debit money
        debitAccount(fromAccount, amount);

        // Step 2: Credit money
        creditAccount(toAccount, amount);
    }
}
```

Agar `creditAccount()` mein error aata hai, to `debitAccount()` bhi rollback ho jayega.

---

## Interview Answer

> Transaction is a group of database operations that execute as a single unit. If all operations are successful, the transaction is committed. If any operation fails, the transaction is rolled back to maintain data consistency.

---

## 2. `@Transactional` kab use karte hain?

`@Transactional` annotation tab use karte hain jab hume database operations ko transaction ke andar execute karna hota hai.

Simple words mein:

> `@Transactional` Spring ko batata hai ki is method ke database operations ko safely manage karo.

---

## Common Use Cases

| Use Case | Example |
|---|---|
| Multiple database operations | Debit and credit money |
| Save + update together | Order create + stock update |
| Delete related data | User delete + user roles delete |
| Rollback required | Error aaye to data undo ho jaye |
| Consistency needed | Half data save na ho |

---

## Example: Order Creation

```java
@Service
public class OrderService {

    @Transactional
    public void placeOrder(Order order) {

        orderRepository.save(order);

        inventoryService.reduceStock(order.getProductId(), order.getQuantity());

        paymentService.makePayment(order.getAmount());
    }
}
```

Yahan 3 operations hain:

```text
1. Order save
2. Stock reduce
3. Payment process
```

Agar payment fail hota hai, to order save aur stock reduce rollback ho sakta hai.

---

## Without `@Transactional`

```java
public void placeOrder(Order order) {

    orderRepository.save(order);

    inventoryService.reduceStock(order.getProductId(), order.getQuantity());

    paymentService.makePayment(order.getAmount());
}
```

Agar payment fail ho gaya, to order already save ho sakta hai.  
Isse inconsistent data create ho sakta hai.

---

## With `@Transactional`

```java
@Transactional
public void placeOrder(Order order) {

    orderRepository.save(order);

    inventoryService.reduceStock(order.getProductId(), order.getQuantity());

    paymentService.makePayment(order.getAmount());
}
```

Agar payment fail hua, to complete transaction rollback ho jayega.

---

## Interview Answer

> `@Transactional` is used when a method performs database operations that should be executed as a single unit. It helps Spring automatically manage commit and rollback. We use it when data consistency is important, especially when multiple database operations are involved.

---

## 3. Default rollback behavior kya hai?

Spring mein `@Transactional` ka default rollback behavior ye hota hai:

> By default, Spring rollback sirf unchecked exceptions par karta hai.

Unchecked exceptions:

```text
RuntimeException
NullPointerException
IllegalArgumentException
ArithmeticException
```

Checked exceptions par by default rollback nahi hota.

Checked exceptions:

```text
IOException
SQLException
FileNotFoundException
Exception
```

---

## Example: RuntimeException

```java
@Transactional
public void saveUser(User user) {

    userRepository.save(user);

    throw new RuntimeException("Something went wrong");
}
```

Yahan rollback hoga because `RuntimeException` unchecked exception hai.

```text
Data save nahi hoga
Transaction rollback ho jayega
```

---

## Example: Checked Exception

```java
@Transactional
public void saveUser(User user) throws IOException {

    userRepository.save(user);

    throw new IOException("File error");
}
```

Yahan by default rollback nahi hoga because `IOException` checked exception hai.

```text
Data save ho sakta hai
Rollback automatically nahi hoga
```

---

## Checked Exception par rollback kaise kare?

Agar checked exception par bhi rollback chahiye, to `rollbackFor` use karte hain.

```java
@Transactional(rollbackFor = Exception.class)
public void saveUser(User user) throws IOException {

    userRepository.save(user);

    throw new IOException("File error");
}
```

Ab checked exception par bhi rollback hoga.

---

## Specific Exception ke liye rollback

```java
@Transactional(rollbackFor = IOException.class)
public void saveUser(User user) throws IOException {

    userRepository.save(user);

    throw new IOException("File error");
}
```

---

## Interview Answer

> By default, Spring rolls back a transaction only for unchecked exceptions like RuntimeException and Error. It does not roll back for checked exceptions by default. If we want rollback for checked exceptions, we use `rollbackFor` in `@Transactional`.

---

## 4. `readOnly` transaction ka fayda?

`readOnly = true` transaction ka use tab karte hain jab method sirf data read karta hai, data modify nahi karta.

Simple words mein:

> `readOnly = true` Spring ko batata hai ki ye method sirf read operation karega, write operation nahi karega.

---

## Example

```java
@Transactional(readOnly = true)
public List<User> getAllUsers() {
    return userRepository.findAll();
}
```

Yahan method sirf users fetch kar raha hai.

---

## Benefits of `readOnly = true`

| Benefit | Explanation |
|---|---|
| Performance improve | Database/JPA optimize kar sakta hai |
| Clear intention | Code se clear hota hai ki method sirf read ke liye hai |
| Dirty checking reduce | Hibernate unnecessary change tracking avoid kar sakta hai |
| Safety | Developer ko signal milta hai ki method mein update/delete nahi hona chahiye |
| Better readability | Code maintain karna easy hota hai |

---

## Without `readOnly`

```java
@Transactional
public List<User> getAllUsers() {
    return userRepository.findAll();
}
```

Ye bhi kaam karega, but Spring/Hibernate is method ko normal transaction treat karega.

---

## With `readOnly = true`

```java
@Transactional(readOnly = true)
public List<User> getAllUsers() {
    return userRepository.findAll();
}
```

Ye better hai for read-only operations.

---

## Important Point

`readOnly = true` ka matlab ye nahi hai ki database 100% write block kar dega.

Mostly ye ek optimization hint hota hai Spring/JPA/Hibernate ke liye.

---

## Interview Answer

> `readOnly = true` is used for methods that only read data from the database. It improves performance, reduces unnecessary dirty checking, and clearly shows that the method is not supposed to modify data. It is mainly an optimization hint for Spring, JPA, and Hibernate.

---

## 5. Service layer me kyu lagate hain?

`@Transactional` mostly **service layer** mein lagate hain because service layer business logic handle karti hai.

Simple words mein:

> Transaction ko service layer mein lagate hain kyunki ek business operation ke andar multiple repository/database calls ho sakti hain.

---

## Application Flow

```text
Controller → Service → Repository → Database
```

Controller request handle karta hai.  
Service business logic handle karti hai.  
Repository database operation handle karta hai.

---

## Example

```java
@Service
public class OrderService {

    @Autowired
    private OrderRepository orderRepository;

    @Autowired
    private PaymentRepository paymentRepository;

    @Transactional
    public void placeOrder(Order order, Payment payment) {

        orderRepository.save(order);

        paymentRepository.save(payment);
    }
}
```

Yahan service method ke andar 2 repository calls hain:

```text
1. Order save
2. Payment save
```

Agar payment save fail hota hai, to order save bhi rollback ho jayega.

---

## Repository layer par kyu nahi?

Repository ka kaam sirf single database operation perform karna hota hai.

Example:

```java
orderRepository.save(order);
paymentRepository.save(payment);
```

Lekin business transaction usually multiple repositories ko combine karta hai.

Isliye transaction boundary service layer par define karna better hota hai.

---

## Controller layer par kyu nahi?

Controller ka kaam HTTP request/response handle karna hota hai.

Controller mein transaction lagane se:

```text
Business logic controller mein mix ho sakti hai
Code tightly coupled ho sakta hai
Testing difficult ho sakti hai
Layered architecture break ho sakta hai
```

---

## Correct Place

```java
@RestController
public class OrderController {

    @Autowired
    private OrderService orderService;

    @PostMapping("/orders")
    public String placeOrder(@RequestBody Order order) {
        orderService.placeOrder(order);
        return "Order placed successfully";
    }
}
```

```java
@Service
public class OrderService {

    @Transactional
    public void placeOrder(Order order) {
        // business logic + database operations
    }
}
```

---

## Benefits of using `@Transactional` in Service Layer

| Benefit | Meaning |
|---|---|
| Proper transaction boundary | Complete business operation cover hota hai |
| Clean architecture | Controller aur repository clean rehte hain |
| Multiple repository calls safe | Ek failure par sab rollback ho sakta hai |
| Business logic centralized | Logic service layer mein rehta hai |
| Testing easy | Service methods ko test karna easy hota hai |
| Maintainability | Code long-term maintainable hota hai |

---

## Interview Answer

> We usually apply `@Transactional` at the service layer because service methods represent business operations. A single service method may call multiple repositories. If any operation fails, the entire transaction should roll back. This keeps transaction boundaries clean and maintains proper layered architecture.

---

# Common Transaction Keywords

| Keyword | Meaning |
|---|---|
| Transaction | Group of DB operations executed as one unit |
| Commit | Save all changes permanently |
| Rollback | Undo changes when error occurs |
| `@Transactional` | Annotation used to manage transaction automatically |
| `readOnly = true` | Used for read-only operations |
| `rollbackFor` | Used to rollback for checked exceptions |
| Checked Exception | Compile-time exception |
| Unchecked Exception | Runtime exception |
| Transaction Boundary | Start and end point of a transaction |

---

# Best Interview Flow Answer

```text
A transaction is a group of database operations executed as a single unit.

If all operations are successful, the transaction is committed. If any operation fails, the transaction is rolled back.

@Transactional is used when we want Spring to manage commit and rollback automatically.

By default, Spring rolls back only for unchecked exceptions like RuntimeException. For checked exceptions, we use rollbackFor.

readOnly = true is used for read-only methods to improve performance and reduce unnecessary dirty checking.

We usually apply @Transactional on the service layer because service methods contain business logic and may call multiple repositories. This keeps transaction boundaries clean and ensures data consistency.
```

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

