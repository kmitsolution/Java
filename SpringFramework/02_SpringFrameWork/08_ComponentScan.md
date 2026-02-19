# ✅ What is `@ComponentScan` in Spring?

`@ComponentScan` tells Spring:

> “Scan the specified packages and automatically create beans for classes annotated with
> `@Component`, `@Service`, `@Repository`, `@Controller`, etc.”

Without component scanning, Spring will **not detect your beans**.

---

# 🎯 Default Behavior in Spring Boot

When you use:

```java
@SpringBootApplication
```

It automatically includes:

```java
@ComponentScan
```

And scans:

```
Current package + all sub-packages
```

---

# 🏗 Example: Scanning 2 Different Packages

Let’s create 2 packages inside:

```
com.kmitcourses
```

---

# 📁 Project Structure

```
com.kmitcourses
    ├── demo
    │     └── DemoApplication.java
    ├── sorting
    │     └── BubbleSort.java
    └── searching
          └── SearchService.java
```

We want Spring to scan:

```
com.kmitcourses.sorting
com.kmitcourses.searching
```

---

# 📦 Package 1: sorting

## 📌 BubbleSort.java

```java
package com.kmitcourses.sorting;

import org.springframework.stereotype.Component;

@Component
public class BubbleSort {

    public void sort() {
        System.out.println("Sorting using Bubble Sort");
    }
}
```

---

# 📦 Package 2: searching

## 📌 SearchService.java

```java
package com.kmitcourses.searching;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;
import com.kmitcourses.sorting.BubbleSort;

@Component
public class SearchService {

    @Autowired
    private BubbleSort bubbleSort;

    public void search() {
        bubbleSort.sort();
        System.out.println("Searching completed");
    }
}
```

---

# 🚀 Main Class (In Different Package)

## 📌 DemoApplication.java

```java
package com.kmitcourses.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.ComponentScan;

@SpringBootApplication
@ComponentScan(basePackages = {
        "com.kmitcourses.sorting",
        "com.kmitcourses.searching"
})
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

---

# 🔍 What Happens Now?

Spring:

1. Starts application
2. Reads `@ComponentScan`
3. Scans both packages
4. Finds:

   * BubbleSort
   * SearchService
5. Creates beans
6. Injects BubbleSort into SearchService

---

# 🖥 Output (If called)

```
Sorting using Bubble Sort
Searching completed
```

---

# 🔄 Important Case: What If You Don’t Use ComponentScan?

If your main class is inside:

```
com.kmitcourses.demo
```

And other packages are:

```
com.kmitcourses.sorting
com.kmitcourses.searching
```

Then Spring Boot will NOT scan them automatically
Because they are **not sub-packages of demo**.

You must use:

```java
@ComponentScan(basePackages = "com.kmitcourses")
```

---

# ✅ Best Practice Structure

Best practice is:

Put main class at root package:

```
com.kmitcourses
```

Then everything under it:

```
com.kmitcourses.demo
com.kmitcourses.sorting
com.kmitcourses.searching
```

Then no need for manual `@ComponentScan`.

Spring Boot automatically scans sub-packages.

---

# 🎯 Multiple Package Scan Syntax Options

### Option 1: Multiple packages

```java
@ComponentScan(basePackages = {
    "com.kmitcourses.sorting",
    "com.kmitcourses.searching"
})
```

---

### Option 2: Scan Entire Root

```java
@ComponentScan("com.kmitcourses")
```

Recommended ✅

---

# 🏆 Summary Table

| Case                              | Behavior                            |
| --------------------------------- | ----------------------------------- |
| No @ComponentScan                 | Only current package + sub-packages |
| @ComponentScan("com.kmitcourses") | Scans entire project                |
| Multiple basePackages             | Scans specific packages             |

---

# 🎓 Interview Answer (Short)

> `@ComponentScan` tells Spring where to search for beans. By default, Spring Boot scans the package of the main class and its sub-packages. If beans are in different packages, we must specify them using `@ComponentScan(basePackages=...)`.

---

# 🚀 Final Understanding

```
@ComponentScan = Bean Discovery Mechanism
```

No scanning → No beans
No beans → No injection

---
