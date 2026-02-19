# ✅ Bean Searching **By Name using `@Autowired` on Variable**

You are asking:

> Not using `@Qualifier`, but using name matching directly on the `sortAlgorithm` variable.

This works because:

> `@Autowired` first tries **By Type**.
> If multiple beans exist, Spring can use **field name matching** to resolve the correct bean.

Let’s see clearly with your project:

```
Group: com.kmitcourses
Package: com.kmitcourses.demo
Artifact: demo
```

---

# 🎯 Important Rule

If:

* Multiple beans of same type exist
* And the **variable name matches a bean name**

Spring will inject that bean.

---

# 📌 Step 1: Interface

```java
package com.kmitcourses.demo;

public interface SortAlgorithm {
    int[] sort(int[] numbers);
}
```

---

# 📌 Step 2: BubbleSort Bean

```java
package com.kmitcourses.demo;

import org.springframework.stereotype.Component;

@Component
public class BubbleSort implements SortAlgorithm {

    @Override
    public int[] sort(int[] numbers) {
        System.out.println("Using Bubble Sort");
        return numbers;
    }
}
```

Bean name automatically becomes:

```
bubbleSort
```

---

# 📌 Step 3: SelectionSort Bean

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

Bean name:

```
selectionSort
```

---

# ✅ Step 4: By-Name Injection Using Variable Name

Now modify `SearchService`.

Instead of using constructor + qualifier, use field injection.

```java
package com.kmitcourses.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class SearchService {

    @Autowired
    private SortAlgorithm bubbleSort;   // Variable name matches bean name

    public int search(int[] numbers, int key) {

        int[] sorted = bubbleSort.sort(numbers);

        for (int i = 0; i < sorted.length; i++) {
            if (sorted[i] == key) {
                return i;
            }
        }

        return -1;
    }
}
```

---

# 🔍 What Happens Internally?

Spring sees:

```
Two beans of type SortAlgorithm:
   bubbleSort
   selectionSort
```

Spring tries:

1. Match by Type → ❌ multiple found
2. Match by Field Name → ✔ finds bean named "bubbleSort"

So it injects:

```
bubbleSort
```

---

# 🔄 Flow Diagram

```
Beans Available:
   bubbleSort
   selectionSort

SearchService has:

@Autowired
private SortAlgorithm bubbleSort;

Spring checks:
   Is there bean named "bubbleSort"? → YES
Inject that bean.
```

---

# 🎯 If You Change Variable Name

```java
@Autowired
private SortAlgorithm selectionSort;
```

Then Spring injects:

```
selectionSort
```

Output becomes:

```
Using Selection Sort
```

---

# ⚠ Important Notes

1. This works only if:

   * Field name exactly matches bean name.
2. If names don’t match → Spring throws error.
3. Constructor injection is still recommended in real projects.

---

# 🔥 Difference Summary

| Method                                | Injection Type     |
| ------------------------------------- | ------------------ |
| `@Autowired` only                     | By Type            |
| `@Autowired` + matching variable name | By Name (fallback) |
| `@Autowired` + `@Qualifier`           | Explicit By Name   |
| `@Resource`                           | Pure By Name       |

---

# 🏆 Final Understanding

Using:

```java
@Autowired
private SortAlgorithm bubbleSort;
```

Spring:

✔ Finds multiple SortAlgorithm beans
✔ Matches field name "bubbleSort"
✔ Injects corresponding bean

No `@Qualifier` needed.

---

# 🎓 Interview Answer (Short)

> When multiple beans of same type exist, Spring’s `@Autowired` can resolve dependency by matching the field name with the bean name if no `@Qualifier` is provided.

