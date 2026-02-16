# ✅ First Understand Important Terms

---

## 🌱 What is a **Bean**?

A **Bean** is:

> An object that is created, managed, and controlled by the Spring IoC container.

If Spring creates the object → it becomes a Bean.

---

## 🌿 What is `@Component`?

`@Component` tells Spring:

> "Create an object of this class and manage it as a Bean."

Example:

```java
@Component
public class BubbleSort {
}
```

Now Spring automatically creates a BubbleSort object.

---

## 🔍 What is `@ComponentScan`?

`@ComponentScan` tells Spring:

> "Scan this package and create beans for all classes annotated with @Component."

Example:

```java
@ComponentScan("com.example")
```

Spring searches inside `com.example` package.

---

## 🔗 What is `@Autowired`?

`@Autowired` means:

> Automatically inject the required dependency.

Spring finds the matching bean and injects it.

---

## 🏗 What is `ApplicationContext`?

`ApplicationContext` is:

> The Spring IoC Container.

It:

* Creates beans
* Injects dependencies
* Manages lifecycle

---

## 🚀 What is `SpringApplication.run()`?

Used in **Spring Boot**

It:

* Starts Spring Boot
* Creates ApplicationContext
* Starts embedded server (if web app)
* Initializes all beans

---

# ✅ Now Full Example: Sorting Algorithm

We will create:

* SortAlgorithm (Interface)
* BubbleSort (Bean)
* SelectionSort (Bean)
* SearchService (Uses sorting algorithm)
* Main Spring Boot class

---

# 📌 Step 1: Create Interface

```java
package com.example.demo;

public interface SortAlgorithm {
    int[] sort(int[] numbers);
}
```

---

# 📌 Step 2: Create BubbleSort Bean

```java
package com.example.demo;

import org.springframework.stereotype.Component;

@Component
public class BubbleSort implements SortAlgorithm {

    public int[] sort(int[] numbers) {
        System.out.println("Using Bubble Sort");
        return numbers;
    }
}
```

---

# 📌 Step 3: Create SelectionSort Bean

```java
package com.example.demo;

import org.springframework.stereotype.Component;

@Component
public class SelectionSort implements SortAlgorithm {

    public int[] sort(int[] numbers) {
        System.out.println("Using Selection Sort");
        return numbers;
    }
}
```

---

# 📌 Step 4: Create SearchService Bean

```java
package com.example.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class SearchService {

    private SortAlgorithm sortAlgorithm;

    @Autowired
    public SearchService(SortAlgorithm sortAlgorithm) {
        this.sortAlgorithm = sortAlgorithm;
    }

    public int search(int[] numbers, int key) {
        int[] sorted = sortAlgorithm.sort(numbers);

        for (int i = 0; i < sorted.length; i++) {
            if (sorted[i] == key) {
                return i;
            }
        }
        return -1;
    }
}
```

Here:

* `SearchService` depends on `SortAlgorithm`
* Spring injects either BubbleSort or SelectionSort

---

# 📌 Step 5: Main Spring Boot Class

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {

        ApplicationContext context =
            SpringApplication.run(DemoApplication.class, args);

        SearchService searchService =
            context.getBean(SearchService.class);

        int result = searchService.search(new int[]{5,3,1,4}, 4);
        System.out.println("Result Index: " + result);
    }
}
```

---

# 🔄 How Everything Works (Step-by-Step)

1. `SpringApplication.run()` starts Spring Boot.
2. Spring creates ApplicationContext.
3. `@ComponentScan` scans package.
4. Spring creates:

   * BubbleSort bean
   * SelectionSort bean
   * SearchService bean
5. Spring sees `@Autowired`.
6. Injects one SortAlgorithm implementation.
7. SearchService uses it.

---

# ⚠ Important Concept: Multiple Beans Problem

Since we have:

* BubbleSort
* SelectionSort

Spring will throw error:

> NoUniqueBeanDefinitionException

Because two beans implement SortAlgorithm.

---

# ✅ Solution: Use `@Primary`

```java
@Component
@Primary
public class BubbleSort implements SortAlgorithm {
}
```

Now BubbleSort will be injected by default.

OR use:

```java
@Autowired
@Qualifier("selectionSort")
```

---

# 🏗 Complete Flow Diagram

```
SpringApplication.run()
        ↓
Creates ApplicationContext
        ↓
ComponentScan finds Beans
        ↓
Creates:
   BubbleSort
   SelectionSort
   SearchService
        ↓
Autowired injects SortAlgorithm
        ↓
SearchService.search() executes
```

---

# 🏆 Final Summary

| Concept               | Meaning                  |
| --------------------- | ------------------------ |
| Bean                  | Object managed by Spring |
| @Component            | Makes class a Bean       |
| @ComponentScan        | Scans package for beans  |
| @Autowired            | Injects dependency       |
| ApplicationContext    | IoC container            |
| SpringApplication.run | Starts Spring Boot       |

---

# 🎯 Real Understanding

SearchService does NOT create:

```java
new BubbleSort();
```

Instead:

Spring creates BubbleSort → Injects into SearchService → IoC achieved.

---

If you want next, I can explain:

* What happens internally in Spring container
* How @Primary and @Qualifier work deeply
* Difference between Spring and Spring Boot in this example
* How this example works in pure Spring (without Boot) 😊

# 🌱 Complete Spring Boot Example

### ✅ Group: `com.kmitcourses`

### ✅ Artifact: `demo`

### ✅ Package: `com.kmitcourses.demo`

We will build the same **Sorting + Searching Algorithm** example using:

* `@Component`
* `@Autowired`
* `@Primary`
* `ApplicationContext`
* `SpringApplication.run()`

---

# ✅ Step 1: Create Project Using Spring Initializr

1. Go to 👉 [https://start.spring.io](https://start.spring.io)
2. Select:

   * **Project**: Maven
   * **Language**: Java
   * **Spring Boot**: Latest Version
3. Fill Details:

   * **Group**: `com.kmitcourses`
   * **Artifact**: `demo`
   * **Name**: `demo`
   * **Package Name**: `com.kmitcourses.demo`
4. Add Dependency:

   * Spring Web (optional but recommended)
5. Click **Generate**
6. Download and extract project
7. Open in IDE (IntelliJ / Eclipse / STS)

---

# 📁 Project Structure

```
src/main/java
   └── com
        └── kmitcourses
              └── demo
                    ├── DemoApplication.java
                    ├── SortAlgorithm.java
                    ├── BubbleSort.java
                    ├── SelectionSort.java
                    └── SearchService.java
```

---

# ✅ Step 2: Create Interface

## 📌 `SortAlgorithm.java`

```java
package com.kmitcourses.demo;

public interface SortAlgorithm {
    int[] sort(int[] numbers);
}
```

---

# ✅ Step 3: Create BubbleSort Bean

## 📌 `BubbleSort.java`

```java
package com.kmitcourses.demo;

import org.springframework.context.annotation.Primary;
import org.springframework.stereotype.Component;

@Component
@Primary
public class BubbleSort implements SortAlgorithm {

    @Override
    public int[] sort(int[] numbers) {
        System.out.println("Using Bubble Sort");
        return numbers;
    }
}
```

---

# ✅ Step 4: Create SelectionSort Bean

## 📌 `SelectionSort.java`

```java
package com.kmitcourses.demo;

import org.springframework.stereotype.Component;

@Component
public class SelectionSort implements SortAlgorithm {

    @Override
    public int[] sort(int[] numbers) {
        System.out.println("Using Selection Sort");
        return numbers;
    }
}
```

---

# ✅ Step 5: Create SearchService Bean

## 📌 `SearchService.java`

```java
package com.kmitcourses.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class SearchService {

    private SortAlgorithm sortAlgorithm;

    @Autowired
    public SearchService(SortAlgorithm sortAlgorithm) {
        this.sortAlgorithm = sortAlgorithm;
    }

    public int search(int[] numbers, int key) {

        int[] sortedNumbers = sortAlgorithm.sort(numbers);

        for (int i = 0; i < sortedNumbers.length; i++) {
            if (sortedNumbers[i] == key) {
                return i;
            }
        }

        return -1;
    }
}
```

---

# ✅ Step 6: Main Spring Boot Class

## 📌 `DemoApplication.java`

```java
package com.kmitcourses.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {

        ApplicationContext context =
                SpringApplication.run(DemoApplication.class, args);

        SearchService searchService =
                context.getBean(SearchService.class);

        int result = searchService.search(new int[]{5, 3, 1, 4}, 4);

        System.out.println("Result Index: " + result);
    }
}
```

---

# 🔎 Now Let’s Understand the Concepts Clearly

---

# ✅ What is a Bean?

A **Bean** is:

> An object created and managed by the Spring IoC container.

In this example, Beans are:

* BubbleSort
* SelectionSort
* SearchService

Because they are annotated with `@Component`.

---

# ✅ What is `@Component`?

`@Component` tells Spring:

> Create an object of this class and manage it as a Bean.

Example:

```java
@Component
public class BubbleSort
```

---

# ✅ What is `@Autowired`?

`@Autowired` means:

> Automatically inject the required dependency.

Spring sees:

```java
public SearchService(SortAlgorithm sortAlgorithm)
```

It searches for a bean implementing `SortAlgorithm`
Since `BubbleSort` has `@Primary`, it injects BubbleSort.

---

# ✅ What is `@Primary`?

When multiple beans implement the same interface:

* BubbleSort
* SelectionSort

Spring gets confused.

`@Primary` tells Spring:

> Use this bean by default.

---

# ✅ What is ApplicationContext?

`ApplicationContext` is:

> The Spring IoC container.

It:

* Creates beans
* Injects dependencies
* Manages lifecycle

We get it from:

```java
SpringApplication.run()
```

---

# ✅ What is `SpringApplication.run()`?

This method:

1. Starts Spring Boot
2. Creates ApplicationContext
3. Performs component scanning
4. Creates all beans
5. Injects dependencies
6. Starts embedded server (if web app)

---

# 🔄 Complete Flow

```
Run DemoApplication
        ↓
SpringApplication.run()
        ↓
ApplicationContext created
        ↓
Component scanning starts
        ↓
Creates Beans:
   BubbleSort
   SelectionSort
   SearchService
        ↓
@Autowired injects BubbleSort into SearchService
        ↓
search() method executes
```

---

# 🎯 Important Concept

Notice:

We NEVER wrote:

```java
new BubbleSort();
```

Spring created it automatically.

This is:

✔ Dependency Injection
✔ Inversion of Control
✔ Loose Coupling

---

# 🏆 Final Summary

| Concept               | Meaning                          |
| --------------------- | -------------------------------- |
| Bean                  | Object managed by Spring         |
| @Component            | Makes class a Bean               |
| @Autowired            | Injects dependency               |
| @Primary              | Default bean when multiple exist |
| ApplicationContext    | IoC container                    |
| SpringApplication.run | Starts Spring Boot               |

---

