# 21) Redis Cache Integration with Spring Boot

> **Module:** 2 (Spring Data JPA)  
> **Language:** Hinglish (Beginner Friendly)  
> **JDK:** 21  
> **Framework:** Spring Boot (Latest Stable)  
> **Build Tool:** Maven  
> **Database:** PostgreSQL  
> **Cache:** Redis  
> **IDE:** IntelliJ IDEA

---

## 1️⃣ Cache kya hota hai? (Theory)
Cache ka matlab hota hai **frequently used data ko fast memory me store karna**.

Simple words me:
> DB slow hota hai, cache fast hota hai.

---

## 2️⃣ Real-World Use Case
- Employee list (bar-bar same request)
- Product catalog
- Configuration data

Without cache:
❌ DB pe load  
❌ Slow response

With cache:
✅ Fast response  
✅ DB load kam

---

## 3️⃣ Redis kya hai?
Redis ek **in-memory key-value store** hai.

Features:
- Extremely fast
- Supports TTL (time-to-live)
- Widely used in industry

---

## 4️⃣ Spring Cache Abstraction
Spring cache abstraction:
- Cache provider independent
- Same annotations

Common annotations:
- `@EnableCaching`
- `@Cacheable`
- `@CachePut`
- `@CacheEvict`

---

## 5️⃣ Maven Dependencies

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```

---

## 6️⃣ Redis Configuration (application.yml)

```yaml
spring:
  cache:
    type: redis
  data:
    redis:
      host: localhost
      port: 6379
```

---

## 7️⃣ Enable Caching

```java
@SpringBootApplication
@EnableCaching
// Purpose: Cache support enable karna
// When: Redis / any cache use kar rahe ho
// Why: Cache annotations ko activate karne ke liye
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

---

## 8️⃣ @Cacheable Annotation

```java
@Service
public class EmployeeService {

    private final EmployeeRepository repo;

    public EmployeeService(EmployeeRepository repo) {
        this.repo = repo;
    }

    @Cacheable(value = "employees", key = "#id")
    // Purpose: Method result ko cache me store karna
    // When: Read-heavy operations
    // Why: DB call avoid karne ke liye
    public Employee getById(Long id) {
        simulateSlowService();
        return repo.findById(id).orElseThrow();
    }

    private void simulateSlowService() {
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}
```

---

## 9️⃣ @CachePut Annotation

```java
@CachePut(value = "employees", key = "#result.id")
// Purpose: Cache ko update karna
// When: Data update ke baad
// Why: Cache stale na ho
public Employee update(Employee emp) {
    return repo.save(emp);
}
```

---

## 🔟 @CacheEvict Annotation

```java
@CacheEvict(value = "employees", key = "#id")
// Purpose: Cache entry delete karna
// When: Data delete ho
// Why: Invalid cache avoid karne ke liye
public void delete(Long id) {
    repo.deleteById(id);
}
```

---

## 1️⃣1️⃣ Cache Flow Diagram (ASCII)

```
Client
  |
  v
Service
  |
  |-- Cache Hit --> Redis --> Response
  |
  |-- Cache Miss --> DB --> Cache --> Response
```

---

## 1️⃣2️⃣ Common Mistakes
❌ @EnableCaching bhool jana
❌ Wrong cache key
❌ Cache + Transaction confusion
❌ Cache not evicted on update

---

## 1️⃣3️⃣ Interview Questions
1. Cache kya hota hai?
2. Redis kyun use karte hain?
3. @Cacheable vs @CachePut
4. Cache eviction kyun zaroori hai?
5. Cache miss kya hota hai?

---

## ✅ Summary
- Redis = fast in-memory cache
- Spring cache abstraction easy
- @Cacheable most used
- DB load reduce hota hai

---

### ❓ Next Topic?
**MODULE 2 → Topic (g): Capstone Project – Spring Data JPA**

👉 Likho: **YES**

