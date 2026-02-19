# ✅ What is `@Qualifier` in Spring?

`@Qualifier` is used when:

> There are **multiple beans of the same type**, and you want to tell Spring **exactly which one to inject**.

---

# 🎯 Why Do We Need `@Qualifier`?

In our example we have:

* `BubbleSort`
* `SelectionSort`

Both implement:

```java
SortAlgorithm
```

So when Spring sees:

```java
@Autowired
public SearchService(SortAlgorithm sortAlgorithm)
```

Spring gets confused:

> ❌ Which one should I inject?

This causes:

```
NoUniqueBeanDefinitionException
```

---

# ✅ Solution 1: Use `@Primary` (Default Bean)

If one bean is marked:

```java
@Primary
@Component
public class BubbleSort implements SortAlgorithm
```

Spring injects `BubbleSort` by default.

But what if you want to use **SelectionSort instead?**

👉 That’s where `@Qualifier` is used.

---

# ✅ How to Use `@Qualifier`

We will use the same project:

### Package:

```
com.kmitcourses.demo
```

---

# Step 1️⃣ Remove `@Primary`

Remove `@Primary` from `BubbleSort`.

---

# Step 2️⃣ Use `@Qualifier`

### Modify `SearchService.java`

```java
package com.kmitcourses.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Component;

@Component
public class SearchService {

    private SortAlgorithm sortAlgorithm;

    @Autowired
    public SearchService(
            @Qualifier("selectionSort") SortAlgorithm sortAlgorithm) {

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

# 🔍 Important Rule

By default, Spring bean name is:

```
class name with first letter lowercase
```

So:

| Class Name    | Bean Name     |
| ------------- | ------------- |
| BubbleSort    | bubbleSort    |
| SelectionSort | selectionSort |

That’s why we wrote:

```java
@Qualifier("selectionSort")
```

---

# 🔄 What Happens Now?

```
Spring sees multiple SortAlgorithm beans
        ↓
Sees @Qualifier("selectionSort")
        ↓
Injects SelectionSort
```

Now output will be:

```
Using Selection Sort
```

---

# 🏗 Flow Diagram

```
BubbleSort   → Bean name: bubbleSort
SelectionSort → Bean name: selectionSort

SearchService
     ↓
@Autowired
@Qualifier("selectionSort")
     ↓
SelectionSort injected
```

---

# ✅ Real Use Cases of `@Qualifier`

### 1️⃣ Multiple Payment Methods

```java
CreditCardPayment
UPIPayment
NetBankingPayment
```

You can choose which one to inject.

---

### 2️⃣ Multiple Database Connections

* MySQL DataSource
* PostgreSQL DataSource

Choose specific datasource.

---

### 3️⃣ Multiple Sorting Algorithms (Our Example)

Choose:

* BubbleSort
* SelectionSort
* QuickSort

---

# ✅ Alternative Way (Custom Bean Name)

You can also give custom name:

```java
@Component("fastSort")
public class BubbleSort implements SortAlgorithm
```

Then:

```java
@Qualifier("fastSort")
```

---

# 🔥 Difference: `@Primary` vs `@Qualifier`

| Feature                 | @Primary      | @Qualifier     |
| ----------------------- | ------------- | -------------- |
| Default Bean            | Yes           | No             |
| Specific Bean Selection | No            | Yes            |
| Used When               | One main bean | Multiple beans |

---

# 🏆 Final Summary

`@Qualifier` is used when:

✔ Multiple beans of same type exist
✔ You want specific bean injection
✔ Avoid NoUniqueBeanDefinitionException

---

# 🎯 Interview Answer (Short Version)

> `@Qualifier` is used along with `@Autowired` when multiple beans of same type are present. It helps specify which exact bean should be injected.

