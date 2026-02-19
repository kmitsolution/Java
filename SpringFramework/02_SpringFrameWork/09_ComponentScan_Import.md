# ✅ Difference Between `@ComponentScan` and `@Import` in Spring

Both are used to register beans in Spring, but they work in different ways.

---

# 🟢 1️⃣ `@ComponentScan`

### 📌 What It Does

`@ComponentScan` tells Spring:

> “Scan the given package(s) and automatically detect classes annotated with
> `@Component`, `@Service`, `@Repository`, `@Controller`.”

It performs **automatic scanning**.

---

## 🔹 Example

### Package Structure

```
com.kmitcourses
   ├── config
   │     └── AppConfig.java
   ├── service
   │     └── OrderService.java
```

---

### OrderService.java

```java
package com.kmitcourses.service;

import org.springframework.stereotype.Service;

@Service
public class OrderService {

    public void process() {
        System.out.println("Order processed");
    }
}
```

---

### AppConfig.java

```java
package com.kmitcourses.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan("com.kmitcourses.service")
public class AppConfig {
}
```

---

### What Happens?

Spring:

1. Scans `com.kmitcourses.service`
2. Finds `@Service`
3. Registers OrderService as bean

---

# 🟡 2️⃣ `@Import`

### 📌 What It Does

`@Import` tells Spring:

> “Register this specific class as a bean.”

It does **explicit importing**, not scanning.

---

## 🔹 Example

### OrderService.java (No Annotation)

```java
package com.kmitcourses.service;

public class OrderService {

    public void process() {
        System.out.println("Order processed");
    }
}
```

---

### AppConfig.java

```java
package com.kmitcourses.config;

import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Import;
import com.kmitcourses.service.OrderService;

@Configuration
@Import(OrderService.class)
public class AppConfig {
}
```

---

### What Happens?

Spring:

1. Does NOT scan package
2. Directly registers OrderService
3. Bean is created

Even though OrderService has NO `@Component`.

---

# 🔥 Key Differences

| Feature                      | `@ComponentScan`         | `@Import`                   |
| ---------------------------- | ------------------------ | --------------------------- |
| How it works                 | Automatic scanning       | Manual class registration   |
| Requires annotation on class | Yes (`@Component`, etc.) | No                          |
| Used for                     | Large packages           | Specific classes            |
| Scans sub-packages           | Yes                      | No                          |
| Best for                     | Application modules      | Config classes or libraries |

---

# 🏗 Real-World Use Case

## When to Use `@ComponentScan`

✔ Normal application development
✔ Large codebase
✔ Automatic bean discovery
✔ Microservices

---

## When to Use `@Import`

✔ Import configuration class from another module
✔ Third-party library configuration
✔ Manually register specific beans
✔ Modular architecture

---

# 🎯 Example: Importing Configuration Class

### SecurityConfig.java

```java
@Configuration
public class SecurityConfig {
}
```

### MainConfig.java

```java
@Configuration
@Import(SecurityConfig.class)
public class MainConfig {
}
```

Now SecurityConfig is included without scanning.

---

# 🧠 Internal Understanding

### `@ComponentScan`

Uses:

```
ClassPath scanning mechanism
```

Spring scans classpath and finds annotated classes.

---

### `@Import`

Registers class directly into:

```
BeanDefinitionRegistry
```

No scanning involved.

---

# 🏆 Final Understanding

```
@ComponentScan = Automatic Discovery
@Import        = Manual Registration
```

---

# 🎓 Interview Answer (Short)

> `@ComponentScan` automatically scans packages and registers annotated classes as beans. `@Import` explicitly registers specific classes or configuration classes as beans without scanning.

---

# 🚀 Best Practice

Use:

✔ `@ComponentScan` for your application
✔ `@Import` for modular configuration

---

