# ✅ Bean Scope in Spring

**Bean Scope** defines:

> How many objects of a bean Spring should create and how long they live.

The two most important scopes are:

1. **Singleton**
2. **Prototype**

---

# 🥇 1️⃣ Singleton Scope (Default Scope)

### 📌 Definition

> Only **one object** of the bean is created per Spring container.

This is the **default scope** in Spring.

---

## ✅ Example (Singleton Scope)

### `MyService.java`

```java
package com.kmitcourses.demo;

import org.springframework.stereotype.Component;

@Component
public class MyService {

    public MyService() {
        System.out.println("MyService Object Created");
    }
}
```

---

### Main Class

```java
ApplicationContext context =
        SpringApplication.run(DemoApplication.class, args);

MyService s1 = context.getBean(MyService.class);
MyService s2 = context.getBean(MyService.class);

System.out.println(s1 == s2);
```

---

### Output:

```
MyService Object Created
true
```

✔ Object created only once
✔ Both references point to same object

---

## 🔹 How to Explicitly Define Singleton

```java
@Component
@Scope("singleton")
public class MyService {
}
```

OR using constant:

```java
@Scope(ConfigurableBeanFactory.SCOPE_SINGLETON)
```

---

# 🥈 2️⃣ Prototype Scope

### 📌 Definition

> A new object is created every time you request the bean.

---

## ✅ Example (Prototype Scope)

### `MyService.java`

```java
package com.kmitcourses.demo;

import org.springframework.context.annotation.Scope;
import org.springframework.stereotype.Component;
import org.springframework.beans.factory.config.ConfigurableBeanFactory;

@Component
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class MyService {

    public MyService() {
        System.out.println("Prototype Object Created");
    }
}
```

---

### Main Class

```java
MyService s1 = context.getBean(MyService.class);
MyService s2 = context.getBean(MyService.class);

System.out.println(s1 == s2);
```

---

### Output:

```
Prototype Object Created
Prototype Object Created
false
```

✔ Object created twice
✔ Different objects

---

# 🎯 What is `ConfigurableBeanFactory.SCOPE_PROTOTYPE`?

It is a constant defined in:

```
org.springframework.beans.factory.config.ConfigurableBeanFactory
```

Instead of writing:

```java
@Scope("prototype")
```

You write:

```java
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
```

### Purpose:

✔ Avoids typing mistakes
✔ Compile-time safety
✔ Cleaner code
✔ Professional way

---

# 🏗 Comparison Table

| Feature                     | Singleton         | Prototype                |
| --------------------------- | ----------------- | ------------------------ |
| Default Scope               | Yes               | No                       |
| Number of Objects           | One per container | New object every request |
| Memory Usage                | Less              | More                     |
| Lifecycle Managed by Spring | Fully             | Only creation            |
| Use Case                    | Services, DAO     | Stateful objects         |

---

# 🔥 Important Concept: Lifecycle Difference

### Singleton

Spring:

* Creates object
* Manages full lifecycle
* Calls destroy methods

---

### Prototype

Spring:

* Creates object
* Gives it to you
* Does NOT manage destruction

You must handle cleanup manually.

---

# ⚠ Important Interview Question

## What Happens If Prototype Bean Is Injected Into Singleton?

Example:

```java
@Component
@Scope("prototype")
public class PrototypeBean {
}
```

```java
@Component
public class SingletonBean {

    @Autowired
    private PrototypeBean prototypeBean;
}
```

👉 Only one prototype instance will be injected at startup.

It will NOT create new instance every time.

Why?

Because injection happens only once when singleton is created.

---

# 🛠 Solution for That Problem

Use:

* ObjectFactory
* Provider
* @Lookup

Example:

```java
@Autowired
private ObjectFactory<PrototypeBean> prototypeBeanFactory;

public void method() {
    PrototypeBean bean = prototypeBeanFactory.getObject();
}
```

Now each call creates new object.

---

# 🏆 When To Use What?

## Use Singleton When:

✔ Stateless services
✔ DAO
✔ Service layer
✔ Controllers

## Use Prototype When:

✔ Stateful objects
✔ Temporary objects
✔ User-specific objects
✔ Heavy calculation instances

---

# 🎓 Interview Answer (Short)

> Singleton scope creates one bean per container and is default in Spring. Prototype scope creates a new bean every time it is requested. ConfigurableBeanFactory.SCOPE_PROTOTYPE is a constant used to define prototype scope safely instead of using string value.

---

# 🚀 Final Understanding

Singleton → One object shared
Prototype → New object each time

---
