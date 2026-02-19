# ✅ What is `@Configuration` in Spring?

`@Configuration` is a Spring annotation that tells Spring:

> “This class contains bean definitions.”

It is used to define **Java-based configuration** instead of XML.

---

# 🎯 Why Do We Need `@Configuration`?

Before Spring 3, we used XML:

```xml
<bean id="orderService" class="com.kmitcourses.demo.OrderService"/>
```

Now we use Java:

```java
@Configuration
public class AppConfig {
}
```

This is called **Java-Based Configuration**.

---

# 🏗 Basic Example

Let’s use your package:

```
com.kmitcourses.demo
```

---

# 📦 Step 1: Create a Normal Class (No Annotation)

## `OrderService.java`

```java
package com.kmitcourses.demo;

public class OrderService {

    public void process() {
        System.out.println("Order processed successfully");
    }
}
```

---

# 📦 Step 2: Create Configuration Class

## `AppConfig.java`

```java
package com.kmitcourses.demo;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    public OrderService orderService() {
        return new OrderService();
    }
}
```

---

# 📦 Step 3: Load ApplicationContext

```java
package com.kmitcourses.demo;

import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class DemoApplication {

    public static void main(String[] args) {

        ApplicationContext context =
                new AnnotationConfigApplicationContext(AppConfig.class);

        OrderService service = context.getBean(OrderService.class);
        service.process();
    }
}
```

---

# 🖥 Output

```
Order processed successfully
```

---

# 🔍 What Happens Internally?

1. Spring reads `@Configuration`
2. Scans for `@Bean` methods
3. Calls `orderService()` method
4. Registers returned object as bean
5. Stores it in IoC container

---

# 🎯 Important Points About `@Configuration`

### ✔ It is a special type of `@Component`

Internally:

```
@Configuration = @Component + special behavior
```

So it is also detected during component scanning.

---

# 🔥 Important Feature: Singleton Guarantee

Consider this:

```java
@Configuration
public class AppConfig {

    @Bean
    public OrderService orderService() {
        return new OrderService();
    }

    @Bean
    public UserService userService() {
        return new UserService(orderService());
    }
}
```

Even though `orderService()` is called inside `userService()`,
Spring ensures:

✔ Only one OrderService object is created.

Because Spring enhances `@Configuration` class using CGLIB proxy.

---

# ⚠ Difference Between `@Configuration` and `@Component`

If you write:

```java
@Component
public class AppConfig {
}
```

Spring will NOT enforce singleton behavior on `@Bean` methods.

`@Configuration` ensures:

✔ Proper bean lifecycle
✔ Singleton guarantee
✔ Method call interception

---

# 🏗 Real-World Use Cases

Use `@Configuration` when:

✔ Creating beans manually
✔ Configuring third-party libraries
✔ Setting up DataSource
✔ Defining custom security config
✔ Replacing XML configuration

---

# 🟢 Example: Database Configuration

```java
@Configuration
public class DatabaseConfig {

    @Bean
    public DataSource dataSource() {
        return new HikariDataSource();
    }
}
```

---

# 🏆 Summary

| Feature            | `@Configuration`                |
| ------------------ | ------------------------------- |
| Purpose            | Define Java-based configuration |
| Contains           | `@Bean` methods                 |
| Replaces           | XML configuration               |
| Is it a component? | Yes                             |
| Ensures singleton? | Yes                             |

---

# 🎓 Interview Answer (Short)

> `@Configuration` is used to define Java-based configuration in Spring. It indicates that the class contains `@Bean` methods, and Spring processes it to create and manage beans in the IoC container.

---

# 🚀 Final Understanding

```
@Configuration → Defines configuration class
@Bean → Defines individual bean inside it
```

# ✅ What is a Proxy in Spring?

### 🔹 Simple Meaning

A **Proxy** is:

> An object that acts as a middleman between the client and the real object.

Instead of calling the real object directly, you call the proxy.

The proxy can:

* Add extra behavior
* Control access
* Manage transactions
* Maintain singleton rules
* Add logging / security

---

# 🎯 Real-Life Analogy

Think of:

```
You → Receptionist → Doctor
```

You don’t directly access the doctor.

The receptionist (proxy) controls access.

---

# 🏗 Why Spring Uses Proxies?

Spring uses proxies for:

✔ AOP (Logging, Security)
✔ Transactions (`@Transactional`)
✔ Lazy loading
✔ Singleton guarantee in `@Configuration`

---

# ✅ What is CGLIB Proxy?

CGLIB = Code Generation Library

It is used by Spring to:

> Create a subclass of your class at runtime.

Instead of using interface-based proxy (JDK dynamic proxy),
CGLIB creates:

```
A child class dynamically
```

---

# 🔥 Now Let’s Understand `@Configuration` Proxy

---

# Example Without Understanding Proxy

```java
@Configuration
public class AppConfig {

    @Bean
    public OrderService orderService() {
        return new OrderService();
    }

    @Bean
    public UserService userService() {
        return new UserService(orderService());
    }
}
```

Question:

How many OrderService objects are created?

---

If this was normal Java:

```
userService() calls orderService()
→ new OrderService() created again
```

So 2 objects would be created.

But in Spring:

✔ Only ONE OrderService object is created.

How?

👉 Using CGLIB proxy.

---

# 🔎 What Spring Does Internally

When Spring sees:

```java
@Configuration
```

It does:

1. Creates a subclass of `AppConfig`
2. Overrides `orderService()` method
3. Intercepts method calls
4. Checks if bean already exists
5. Returns existing bean instead of creating new one

---

# 🏗 Internal Working Flow

Original:

```
AppConfig
```

Spring creates:

```
AppConfig$$EnhancerBySpringCGLIB
```

This subclass overrides:

```
orderService()
```

---

# 🔄 Step-by-Step Execution

When:

```java
userService()
```

calls:

```java
orderService()
```

Actually:

```
Proxy intercepts the call
```

Proxy checks:

```
Is OrderService already created?
```

If YES:

✔ Return existing singleton

If NO:

✔ Create it and store in container

---

# 🧠 Why Proxy Is Needed?

Because without proxy:

Java method call inside same class is:

```
Direct method call
```

Spring cannot intercept it.

Proxy allows Spring to:

```
Intercept internal method calls
```

---

# 🎯 Important Note

If you remove `@Configuration` and replace with:

```java
@Component
```

Then:

Spring will NOT create CGLIB proxy.

Result:

```
Multiple OrderService objects may be created
```

---

# 🔥 Visual Diagram

Without Proxy:

```
userService()
   ↓
orderService()
   ↓
new OrderService()  (multiple times)
```

With Proxy:

```
userService()
   ↓
Proxy intercepts orderService()
   ↓
Checks container
   ↓
Returns existing singleton
```

---

# 🏆 Summary

| Concept | Meaning                                   |
| ------- | ----------------------------------------- |
| Proxy   | Middle object controlling access          |
| CGLIB   | Library that creates subclass dynamically |
| Used in | @Configuration, AOP, Transactions         |
| Purpose | Maintain singleton behavior, add features |

---

# 🎓 Interview Answer (Short Version)

> A proxy in Spring is an object that wraps the original object to add extra behavior like transaction management or singleton control. In `@Configuration`, Spring uses CGLIB to create a subclass proxy that intercepts `@Bean` method calls and ensures singleton beans are not created multiple times.

---

# 🚀 Final Understanding

```
@Configuration → Uses CGLIB Proxy
Proxy → Intercepts @Bean methods
Ensures → Singleton behavior
```


Together they replace XML configuration.

