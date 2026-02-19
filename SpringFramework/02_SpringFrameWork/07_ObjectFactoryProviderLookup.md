# ✅ How to Get Prototype Bean Inside Singleton

### Using:

1. `ObjectFactory`
2. `Provider`
3. `@Lookup`

We’ll use your package:

```
com.kmitcourses.demo
```

And real-time example:

```
OrderService  → Singleton
OrderProcessor → Prototype
```

Goal:

> Every time `placeOrder()` runs → create NEW OrderProcessor object.

---

# 🥇 1️⃣ Using `ObjectFactory`

### 📌 What is ObjectFactory?

`ObjectFactory<T>` is a Spring interface.

It provides:

```java
T getObject();
```

Each time you call `getObject()`, Spring gives a new instance (if bean is prototype).

---

## Step 1: Prototype Bean

```java
package com.kmitcourses.demo;

import org.springframework.context.annotation.Scope;
import org.springframework.stereotype.Component;
import org.springframework.beans.factory.config.ConfigurableBeanFactory;

@Component
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class OrderProcessor {

    public OrderProcessor() {
        System.out.println("New OrderProcessor Created");
    }

    public void process(String orderId) {
        System.out.println("Processing order: " + orderId);
    }
}
```

---

## Step 2: Singleton Bean Using ObjectFactory

```java
package com.kmitcourses.demo;

import org.springframework.beans.factory.ObjectFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class OrderService {

    @Autowired
    private ObjectFactory<OrderProcessor> processorFactory;

    public void placeOrder(String orderId) {

        OrderProcessor processor = processorFactory.getObject();
        processor.process(orderId);
    }
}
```

---

## What Happens?

Every call:

```java
processorFactory.getObject();
```

Creates NEW object.

---

# 🥈 2️⃣ Using `Provider` (Recommended Modern Way)

`Provider<T>` comes from:

```
jakarta.inject.Provider
```

It works similar to ObjectFactory but is Java standard.

---

## Step 1: Import

```java
import jakarta.inject.Provider;
```

---

## Step 2: Singleton Bean Using Provider

```java
package com.kmitcourses.demo;

import jakarta.inject.Provider;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class OrderService {

    @Autowired
    private Provider<OrderProcessor> processorProvider;

    public void placeOrder(String orderId) {

        OrderProcessor processor = processorProvider.get();
        processor.process(orderId);
    }
}
```

---

## What Happens?

Every call:

```java
processorProvider.get();
```

Returns NEW prototype instance.

---

# 🥉 3️⃣ Using `@Lookup`

`@Lookup` is a special Spring annotation.

It tells Spring:

> Override this method and return a new bean every time.

---

## Step 1: Singleton Bean

```java
package com.kmitcourses.demo;

import org.springframework.beans.factory.annotation.Lookup;
import org.springframework.stereotype.Component;

@Component
public abstract class OrderService {

    public void placeOrder(String orderId) {

        OrderProcessor processor = createProcessor();
        processor.process(orderId);
    }

    @Lookup
    protected abstract OrderProcessor createProcessor();
}
```

---

## What Happens?

Spring:

* Creates subclass dynamically
* Overrides `createProcessor()`
* Returns new prototype bean each time

---

# 🔄 Comparison of All Three

| Feature        | ObjectFactory | Provider           | @Lookup       |
| -------------- | ------------- | ------------------ | ------------- |
| Part of Spring | Yes           | No (Java standard) | Yes           |
| Method         | getObject()   | get()              | Custom method |
| Easy to Read   | Medium        | High               | Medium        |
| Recommended    | Good          | ✅ Best             | Advanced      |

---

# 🎯 Which One Should You Use?

✔ Modern applications → Use **Provider**
✔ Pure Spring → ObjectFactory
✔ Advanced dynamic method override → @Lookup

---

# 🧠 Why These Are Needed?

Because:

When prototype is injected into singleton normally:

```
Only one instance is injected
```

To get NEW object every time:

```
We need lazy fetching
```

These 3 methods provide that.

---

# 🏗 Execution Flow (Provider Example)

```
OrderService (Singleton)
        ↓
Calls provider.get()
        ↓
Spring creates new OrderProcessor
        ↓
Returns it
```

---

# 🏆 Interview Answer (Short Version)

> When a prototype bean is injected into a singleton, it behaves like singleton. To get a new instance every time, we use ObjectFactory, Provider, or @Lookup. These perform lazy retrieval of the prototype bean.

---

# 🚀 Final Understanding

Singleton → Created once
Prototype → Created multiple times
Prototype inside Singleton → Needs lazy retrieval

