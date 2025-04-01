# **Wrapper Classes in Java**

### **What are Wrapper Classes?**
Wrapper classes are **object representations of primitive data types** in Java. They allow primitives (`int`, `double`, `char`, etc.) to be used as **objects** when needed (e.g., in collections like `ArrayList`).  

Each primitive type has a corresponding **wrapper class** in the `java.lang` package.

### **List of Wrapper Classes**
| **Primitive Type** | **Wrapper Class** |
|--------------------|------------------|
| `byte`            | `Byte`            |
| `short`           | `Short`           |
| `int`             | `Integer`         |
| `long`            | `Long`            |
| `float`           | `Float`           |
| `double`          | `Double`          |
| `char`            | `Character`       |
| `boolean`         | `Boolean`         |

---

## **1. Why Use Wrapper Classes?**
- **Allows Primitives to be Used in Collections**  
  Collections like `ArrayList<Integer>` can’t store primitive `int`, so `Integer` is used.
- **Provides Utility Methods**  
  Example: `Integer.parseInt("100")` converts a string to an integer.
- **Supports Autoboxing and Unboxing**  
  Java automatically converts between primitives and wrapper objects.

---

## **2. Autoboxing and Unboxing**
### **Autoboxing (Primitive → Object)**
Automatically converts a primitive to a wrapper object.
```java
Integer obj = 10; // Autoboxing: int → Integer
Double dObj = 5.5; // Autoboxing: double → Double
```

### **Unboxing (Object → Primitive)**
Automatically converts a wrapper object back to a primitive.
```java
int num = obj; // Unboxing: Integer → int
double dNum = dObj; // Unboxing: Double → double
```

---

## **3. Wrapper Class Methods**
Each wrapper class provides useful methods.

| **Method** | **Description** |
|------------|---------------|
| `parseXxx(String s)` | Converts string to primitive (`Integer.parseInt("100") → 100`) |
| `valueOf(String s)` | Converts string to wrapper (`Integer.valueOf("200") → Integer(200)`) |
| `xxxValue()` | Converts wrapper to another type (`Double d = 5.5; d.intValue() → 5`) |
| `compareTo(T t)` | Compares values (`Integer(5).compareTo(3) → 1`) |
| `equals(Object o)` | Checks if two objects are equal (`new Integer(10).equals(10) → true`) |

**Example:**
```java
public class WrapperExample {
    public static void main(String[] args) {
        Integer x = Integer.valueOf(100);
        int y = Integer.parseInt("200");

        System.out.println(x + y); // Output: 300
    }
}
```

---

## **4. Wrapper Class Hierarchy**
In Java, all wrapper classes extend the `Number` class **except** `Character` and `Boolean`.

### **Wrapper Class Inheritance Structure**
```
         Object
            │
         Number
        ┌──┼──┬──┬──┐
     Integer Long Float Double Short Byte
```
- `Integer`, `Long`, `Float`, `Double`, `Short`, and `Byte` **inherit from `Number`**.
- `Character` and `Boolean` **directly extend `Object`** (not `Number`).

### **Example: `Integer` Class Inheritance**
```java
public class InheritanceExample {
    public static void main(String[] args) {
        Integer num = 100;
        Number n = num;  // Upcasting (Integer → Number)
        Object obj = num; // Upcasting (Integer → Object)

        System.out.println(n.doubleValue()); // Converts Integer to Double
    }
}
```

---

## **5. `Number` Class in Java**
The `Number` class is an **abstract class** that provides methods for numeric wrapper classes.

### **Methods in `Number` Class**
| **Method** | **Description** |
|------------|---------------|
| `intValue()` | Returns value as `int` |
| `longValue()` | Returns value as `long` |
| `floatValue()` | Returns value as `float` |
| `doubleValue()` | Returns value as `double` |

Example:
```java
Number num = new Integer(50);
System.out.println(num.doubleValue()); // Output: 50.0
```

---

## **6. Difference Between Wrapper Classes and Primitives**
| Feature | Primitive Type | Wrapper Class |
|---------|---------------|--------------|
| **Storage** | Stored in stack | Stored in heap |
| **Default Value** | `0` for numbers, `false` for boolean | `null` |
| **Supports Methods?** | ❌ No methods | ✅ Has methods (`parseInt`, `compareTo`) |
| **Used in Collections?** | ❌ No | ✅ Yes |
| **Performance** | Faster | Slower (because of object creation) |

---

## **7. Example: Using Wrapper Classes in Collections**
```java
import java.util.*;

public class WrapperInCollection {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        list.add(10); // Autoboxing
        list.add(20);

        int num = list.get(0); // Unboxing
        System.out.println("First element: " + num);
    }
}
```
### **Output**
```
First element: 10
```

---

## **Conclusion**
- Wrapper classes convert **primitives into objects**.
- They provide **utility methods** for conversions and comparisons.
- **Autoboxing** and **unboxing** simplify primitive-to-object conversion.
- `Integer`, `Double`, etc., **inherit from `Number`**, while `Character` and `Boolean` do not.

Would you like more details on a specific topic? 😊🚀
