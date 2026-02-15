# ✅ 1️⃣ What is Dependency Injection?

Dependency Injection (DI) means:

> The Spring IoC container creates objects (beans) and injects required dependencies instead of the class creating them.

There are two main types:

1. **Setter Injection**
2. **Constructor Injection**

---

# ✅ 2️⃣ Constructor Injection

### 🔹 Definition

Dependencies are injected through the **constructor**.

---

## 🔸 Example Without Spring (Normal Java)

```java
class Engine {
    void start() {
        System.out.println("Engine Started");
    }
}

class Car {

    private Engine engine;

    public Car(Engine engine) {   // Constructor Injection
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car is running");
    }
}
```

Here:

* `Car` depends on `Engine`
* `Engine` is injected through constructor

---

## 🔸 Constructor Injection Using Spring XML

### Step 1: POJO Classes

```java
public class Engine {
    public void start() {
        System.out.println("Engine Started");
    }
}
```

```java
public class Car {

    private Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car Running");
    }
}
```

---

### Step 2: XML Configuration File (beans.xml)

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Define Engine Bean -->
    <bean id="engine" class="com.example.Engine"/>

    <!-- Constructor Injection -->
    <bean id="car" class="com.example.Car">
        <constructor-arg ref="engine"/>
    </bean>

</beans>
```

---

### Step 3: Load Spring Container

```java
ApplicationContext context =
    new ClassPathXmlApplicationContext("beans.xml");

Car car = context.getBean("car", Car.class);
car.drive();
```

---

# ✅ 3️⃣ Setter Injection

### 🔹 Definition

Dependencies are injected using **setter methods**.

---

## 🔸 POJO Classes

```java
public class Car {

    private Engine engine;

    public void setEngine(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car Running");
    }
}
```

---

## 🔸 XML Configuration (Setter Injection)

```xml
<bean id="engine" class="com.example.Engine"/>

<bean id="car" class="com.example.Car">
    <property name="engine" ref="engine"/>
</bean>
```

Here:

* `property name="engine"` → refers to `setEngine()`
* `ref="engine"` → refers to engine bean

---

# ✅ 4️⃣ Difference: Constructor vs Setter Injection

| Feature              | Constructor Injection | Setter Injection      |
| -------------------- | --------------------- | --------------------- |
| Injection Time       | At object creation    | After object creation |
| Mandatory Dependency | Yes                   | No                    |
| Immutable Object     | Yes                   | No                    |
| Recommended          | ✅ Yes                 | Only if optional      |

👉 Constructor injection is recommended in modern Spring.

---

# ✅ 5️⃣ What is Configuration File for IoC?

The configuration file tells Spring:

* Which classes are beans
* How to create beans
* How to inject dependencies

In XML configuration, we define:

```xml
<bean id="beanName" class="fullyQualifiedClassName">
    <property/>
    <constructor-arg/>
</bean>
```

---

# 🔄 How IoC Works Step-by-Step

1. You create POJO classes.
2. You define beans in configuration (XML/Java/Annotation).
3. Spring IoC container reads configuration.
4. Spring creates objects.
5. Spring injects dependencies.
6. Objects are ready to use.

---

# 🔥 Modern Alternative (Annotation-Based)

Instead of XML:

```java
@Component
public class Engine {
}
```

```java
@Component
public class Car {

    private Engine engine;

    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

Configuration:

```java
@Configuration
@ComponentScan("com.example")
public class AppConfig {
}
```

Load:

```java
ApplicationContext context =
    new AnnotationConfigApplicationContext(AppConfig.class);
```

---

# 🏗️ Visual Flow

```
Engine Bean
     ↓
Injected into
     ↓
Car Bean
     ↓
Managed by Spring IoC Container
```

---

# 🏆 Final Summary

| Concept               | Meaning                               |
| --------------------- | ------------------------------------- |
| Setter Injection      | Dependency injected via setter method |
| Constructor Injection | Dependency injected via constructor   |
| XML Configuration     | Defines beans and dependencies        |
| IoC Container         | Creates and manages beans             |
| Recommended Approach  | Constructor Injection                 |

---

