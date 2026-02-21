# MODULE 3 → Topic (f): API Testing with JUnit & Mockito (Spring Boot)

> **Language:** Hinglish (Beginner Friendly)
> **JDK:** 21
> **Spring Boot:** Latest Stable
> **Testing:** JUnit 5 (Jupiter) + Mockito
> **Build Tool:** Maven
> **IDE:** IntelliJ IDEA

---

## 1️⃣ THEORY – API Testing kya hoti hai?

API Testing ka matlab hota hai **backend APIs ko verify karna** ki:
- API expected response de rahi hai ya nahi
- Business logic sahi kaam kar raha hai ya nahi
- Error cases properly handle ho rahe hain ya nahi

Simple language me:
> "Code likhne ke baad usko test karna bina UI ke"

---

## 2️⃣ REAL-WORLD USE CASE (Industry)

### 🎯 Scenario: Employee Management System

Company me:
- Daily code changes hote hain
- Multiple developers kaam karte hain

Risk:
❌ New change se purana feature toot sakta hai

Solution:
✅ **Automated API Tests (JUnit + Mockito)**

CI/CD pipeline me:
- Code push
- Tests run
- Fail → deployment stop

---

## 3️⃣ TYPES OF TESTING (IMPORTANT)

| Type | Kya test hota hai |
|----|------------------|
| Unit Test | Single class / method |
| Integration Test | Multiple layers |
| API Test | Controller endpoints |

Aaj hum focus karenge:
👉 **Unit Testing + Controller Testing**

---

## 4️⃣ REQUIRED DEPENDENCIES (Maven)

### pom.xml

```xml
<!-- Spring Boot Test Starter -->
<!-- Purpose: JUnit, Mockito, MockMvc sab ek saath -->
<!-- When: Testing likhni ho -->
<!-- Why here: Separate dependencies add karne ki zarurat nahi -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

---

## 5️⃣ SERVICE LAYER UNIT TEST (Mockito)

### EmployeeServiceTest.java

```java
package com.company.ems.service;

import com.company.ems.entity.Employee;
import com.company.ems.repository.EmployeeRepository;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import java.util.List;

import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

// @ExtendWith(MockitoExtension.class)
// Purpose: Mockito ko JUnit 5 ke saath integrate karta hai
// When: Mockito annotations use karni ho
// Why here: @Mock aur @InjectMocks kaam kare
@ExtendWith(MockitoExtension.class)
class EmployeeServiceTest {

    // @Mock
    // Purpose: Fake object create karta hai
    // When: Real DB call nahi chahiye
    // Why here: Repository ko mock karna
    @Mock
    private EmployeeRepository repository;

    // @InjectMocks
    // Purpose: Mock objects inject karta hai
    // When: Service class test karni ho
    // Why here: Repository mock inject ho
    @InjectMocks
    private EmployeeServiceImpl service;

    @Test
    void shouldReturnAllEmployees() {
        when(repository.findAll()).thenReturn(List.of(new Employee()));
        List<Employee> employees = service.findAll();
        assertEquals(1, employees.size());
    }
}
```

---

## 6️⃣ CONTROLLER TESTING (MockMvc)

### EmployeeControllerTest.java

```java
package com.company.ems.controller;

import com.company.ems.entity.Employee;
import com.company.ems.service.EmployeeService;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.test.web.servlet.MockMvc;

import static org.mockito.Mockito.*;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

// @WebMvcTest
// Purpose: Sirf controller layer load karta hai
// When: API endpoints test karni ho
// Why here: Fast & focused testing
@WebMvcTest(EmployeeController.class)
class EmployeeControllerTest {

    @Autowired
    private MockMvc mockMvc;

    // @MockBean
    // Purpose: Spring context me mock bean register karta hai
    // When: Service layer mock karni ho
    // Why here: Real service call avoid
    @MockBean
    private EmployeeService service;

    @Test
    void shouldReturnEmployeeList() throws Exception {
        when(service.findAll()).thenReturn(List.of(new Employee()));

        mockMvc.perform(get("/api/employees"))
                .andExpect(status().isOk());
    }
}
```

---

## 7️⃣ TEST FLOW (ASCII)

```
JUnit Test
   |
   v
MockMvc / Mockito
   |
   v
Controller / Service
   |
   v
Assertions
```

---

## 8️⃣ COMMON BEGINNER MISTAKES

❌ Database hit karna unit test me
❌ Sab kuch integration test banana
❌ Assertions na likhna

---

## 9️⃣ INTERVIEW QUESTIONS

1. Unit test aur integration test me difference?
2. Mockito ka use kyun?
3. @Mock vs @MockBean?
4. MockMvc kya karta hai?
5. CI/CD me testing ka role?

---

## 🔟 SUMMARY

✔ JUnit = testing framework
✔ Mockito = mocking tool
✔ Unit tests fast & reliable
✔ Controller tests API verify karte hain
✔ Industry me mandatory skill

---

❓ **Should I move to the next topic?**

🔹 MODULE 3 → Topic (g): REST Capstone Project

👉 Sirf **YES** likho.

