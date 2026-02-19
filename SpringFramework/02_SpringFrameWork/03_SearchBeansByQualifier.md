# ✅ Bean Searching **By Name** in Spring

(Using SortAlgorithm Example)

In Spring, dependency injection can happen:

1. **By Type** (default behavior of `@Autowired`)
2. **By Name** (using `@Qualifier` or `@Resource`)

Now let’s clearly understand **By Name searching** using your:

```
com.kmitcourses.demo
```

Sorting Algorithm example.

---

# 🎯 What is By-Name Bean Searching?

By-Name means:

> Spring injects the bean whose **name matches the variable name** or the specified qualifier name.

---

# 🔎 Default Bean Names in Spring

When you use:

```java
@Component
public class BubbleSort
```

Spring automatically creates a bean with name:

```
bubbleSort
```

Similarly:

```java
@Component
public class SelectionSort
```

Bean name becomes:

```
selectionSort
```

Rule:

> ClassName → first letter lowercase

---

# ✅ Example: By-Name Injection Using `@Qualifier`

---

## 📌 Step 1: Interface

```java
package com.kmitcourses.demo;

public interface SortAlgorithm {
    int[] sort(int[] numbers);
}
```

---

## 📌 Step 2: BubbleSort Bean

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

---

## 📌 Step 3: SelectionSort Bean

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

# ✅ Step 4: Inject By Name Using `@Qualifier`

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

---

# 🔍 What Happens Internally?

Spring sees:

```
Multiple beans of type SortAlgorithm:
   bubbleSort
   selectionSort
```

Then sees:

```java
@Qualifier("selectionSort")
```

Spring injects:

```
Bean with name "selectionSort"
```

---

# 🏗 Flow

```
BubbleSort  → bean name: bubbleSort
SelectionSort → bean name: selectionSort

SearchService constructor
      ↓
@Qualifier("selectionSort")
      ↓
Spring injects SelectionSort
```

---

# ✅ Alternative: Using `@Resource` (Pure By Name)

`@Resource` works primarily by name.

```java
import jakarta.annotation.Resource;

@Component
public class SearchService {

    @Resource(name = "bubbleSort")
    private SortAlgorithm sortAlgorithm;

    public int search(int[] numbers, int key) {
        sortAlgorithm.sort(numbers);
        return -1;
    }
}
```

Here:

```
@Resource(name="bubbleSort")
```

Spring directly searches bean by name.

---

# 🔥 Difference Between By-Type and By-Name

| Injection Type | How It Works                          |
| -------------- | ------------------------------------- |
| By Type        | Matches based on class/interface type |
| By Name        | Matches based on bean name            |
| @Autowired     | By Type (default)                     |
| @Qualifier     | By Name (with @Autowired)             |
| @Resource      | By Name (default behavior)            |

---

# 🎯 When To Use By-Name?

Use By-Name when:

✔ Multiple beans of same type exist
✔ You want specific implementation
✔ You want clear control
✔ Avoid ambiguity error

---

# 🏆 Final Understanding

In your Sorting example:

If you want:

* BubbleSort → use `"bubbleSort"`
* SelectionSort → use `"selectionSort"`

Spring searches bean name inside IoC container and injects matching one.

---

# 🎓 Interview Answer (Short)

> By-name injection in Spring means the container injects a dependency by matching the bean name. It can be done using `@Qualifier` with `@Autowired` or using `@Resource`.

