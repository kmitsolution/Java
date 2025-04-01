# **FAQ on Wrapper Classes in Java**  

---

## **1. What are wrapper classes in Java?**
Wrapper classes **convert primitive data types** (`int`, `double`, `char`, etc.) into objects. They are useful when we need **primitives to behave as objects**, for example, in **collections (ArrayList, HashMap)**.

Each primitive type has a corresponding **wrapper class** in `java.lang` package.

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

## **2. Why do we need wrapper classes?**
- **To use primitives in collections** (`ArrayList<Integer>` instead of `int[]`).
- **To use built-in methods** (`Integer.parseInt("100")` to convert string to number).
- **To perform type conversion** (`Integer to Double`, etc.).
- **To store null values**, which primitives **cannot**.

---

## **3. What is autoboxing and unboxing?**
Java **automatically** converts between **primitive types and their wrapper classes**.

### **Autoboxing (Primitive → Object)**
```java
Integer num = 10; // Autoboxing: int → Integer
Double dNum = 5.5; // Autoboxing: double → Double
```

### **Unboxing (Object → Primitive)**
```java
int value = num; // Unboxing: Integer → int
double dValue = dNum; // Unboxing: Double → double
```

---

## **4. What are some useful methods in wrapper classes?**
Each wrapper class provides **methods** to convert and manipulate values.

| **Method** | **Description** | **Example** |
|------------|---------------|-------------|
| `parseXxx(String s)` | Converts String to primitive | `int x = Integer.parseInt("100");` |
| `valueOf(String s)` | Converts String to wrapper object | `Integer obj = Integer.valueOf("200");` |
| `xxxValue()` | Converts wrapper to another type | `Double d = 5.5; d.intValue(); // 5` |
| `compareTo(T t)` | Compares two values | `Integer(5).compareTo(3); // 1` |
| `equals(Object o)` | Checks if two objects are equal | `new Integer(10).equals(10); // true` |

### **Example:**
```java
public class WrapperMethods {
    public static void main(String[] args) {
        Integer x = Integer.valueOf("100");
        int y = Integer.parseInt("200");

        System.out.println(x + y); // Output: 300
    }
}
```

---

## **5. What is the inheritance hierarchy of wrapper classes?**
All numeric wrapper classes (`Integer`, `Double`, etc.) inherit from the **abstract class `Number`**, except `Character` and `Boolean`, which extend `Object`.

### **Wrapper Class Hierarchy**
```
         Object
            │
         Number
        ┌──┼──┬──┬──┐
     Integer Long Float Double Short Byte
```
- `Integer`, `Double`, etc. **extend `Number`**.
- `Character` and `Boolean` **extend `Object`**.

---

## **6. Can wrapper classes store `null` values?**
Yes, since wrapper classes are **objects**, they can store `null`.

```java
Integer num = null; // Allowed
int x = null; // ❌ Compilation error (primitives can't be null)
```

---

## **7. What is the difference between primitives and wrapper classes?**

| Feature | Primitive Type | Wrapper Class |
|---------|---------------|--------------|
| **Stored in** | Stack | Heap (object) |
| **Default Value** | `0`, `false` | `null` |
| **Methods available?** | ❌ No | ✅ Yes (`parseInt`, `valueOf`, etc.) |
| **Used in collections?** | ❌ No | ✅ Yes (`ArrayList<Integer>`) |
| **Performance** | Faster | Slower (because of object creation) |

---

## **8. Why can’t we use primitives in collections?**
Java collections (`ArrayList`, `HashMap`) work with **objects** only. Since primitives are not objects, we must use wrapper classes.

```java
List<Integer> list = new ArrayList<>();
list.add(10); // Autoboxing: int → Integer
int num = list.get(0); // Unboxing: Integer → int
```

---

## **9. How do wrapper classes handle comparisons?**
Wrapper classes use **`==`** and **`.equals()`** differently.

### **Example:**
```java
Integer a = 127;
Integer b = 127;
System.out.println(a == b); // true (within cached range)

Integer x = 128;
Integer y = 128;
System.out.println(x == y); // false (outside cached range)

System.out.println(x.equals(y)); // true (compares values)
```

### **Explanation:**
- Java **caches** integers from `-128 to 127`, so `a == b` is `true` for small values.
- For values **outside** this range, `==` compares **object references**, so it returns `false`.
- `.equals()` always compares **values**, so it returns `true`.

---

## **10. What is the performance impact of using wrapper classes?**
- **Wrapper classes** require **more memory** because they are stored in the **heap**.
- **Autoboxing & unboxing** can cause **extra overhead**.

### **Example: Performance Difference**
```java
long startTime = System.nanoTime();

int sum = 0;
for (int i = 0; i < 1_000_000; i++) {
    sum += i; // Fast (primitive addition)
}

long endTime = System.nanoTime();
System.out.println("Time taken: " + (endTime - startTime));

long startTime2 = System.nanoTime();

Integer sumObj = 0;
for (int i = 0; i < 1_000_000; i++) {
    sumObj += i; // Slow (Autoboxing + Unboxing)
}

long endTime2 = System.nanoTime();
System.out.println("Time taken: " + (endTime2 - startTime2));
```
- Using `Integer` takes **more time** than `int` because of **autoboxing/unboxing**.

---

## **11. Can we create our own wrapper class?**
Yes! We can create custom wrapper classes.

```java
class MyInt {
    private int value;

    public MyInt(int value) { this.value = value; }

    public int getValue() { return value; }
}
```

---

## **12. Can wrapper classes be serialized?**
Yes, all wrapper classes **implement `Serializable`**, so they can be saved and retrieved.

```java
Integer x = 100;
try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("data.ser"))) {
    out.writeObject(x);
}
```

---

## **13. What happens if we compare `null` with an unboxed primitive?**
It throws **NullPointerException**.

```java
Integer num = null;
int x = num; // ❌ NullPointerException
```

---

## **14. What happens if we use a wrapper class in a `switch` statement?**
From **Java 7 onwards**, wrapper classes (`Integer`, `Character`, etc.) **can be used in `switch`**.

```java
Integer choice = 2;
switch (choice) {
    case 1 -> System.out.println("One");
    case 2 -> System.out.println("Two");
}
```

---

## **15. What are some common mistakes when using wrapper classes?**
- **Using `==` instead of `.equals()`**  
  ```java
  Integer x = 200;
  Integer y = 200;
  System.out.println(x == y); // false (different objects)
  System.out.println(x.equals(y)); // true (same value)
  ```
- **NullPointerException when unboxing `null`**  
  ```java
  Integer num = null;
  int x = num; // ❌ Throws NullPointerException
  ```

---


### **Value Range for Wrapper Classes in Java**  

Each **wrapper class** in Java represents a **primitive data type** and has a **fixed range** of values. Here’s a table showing the **minimum and maximum values** for each wrapper class:

| **Wrapper Class** | **Primitive Type** | **Minimum Value** | **Maximum Value** | **Constant Field** |
|------------------|-------------------|------------------|------------------|-----------------|
| `Byte`          | `byte`             | `-128`           | `127`            | `Byte.MIN_VALUE`, `Byte.MAX_VALUE` |
| `Short`         | `short`            | `-32,768`        | `32,767`         | `Short.MIN_VALUE`, `Short.MAX_VALUE` |
| `Integer`       | `int`              | `-2,147,483,648` | `2,147,483,647`  | `Integer.MIN_VALUE`, `Integer.MAX_VALUE` |
| `Long`          | `long`             | `-9,223,372,036,854,775,808` | `9,223,372,036,854,775,807` | `Long.MIN_VALUE`, `Long.MAX_VALUE` |
| `Float`         | `float`            | `1.4E-45`        | `3.4028235E+38`  | `Float.MIN_VALUE`, `Float.MAX_VALUE` |
| `Double`        | `double`           | `4.9E-324`       | `1.7976931348623157E+308` | `Double.MIN_VALUE`, `Double.MAX_VALUE` |
| `Character`     | `char`             | `'\u0000'` (0)   | `'\uffff'` (65,535) | `Character.MIN_VALUE`, `Character.MAX_VALUE` |
| `Boolean`       | `boolean`          | `false`          | `true`           | N/A |

---

### **How to Get the Value Range in Java?**
You can use **constant fields** (`MIN_VALUE`, `MAX_VALUE`) in Java to check these ranges dynamically.

#### **Example: Printing Min & Max Values**
```java
public class WrapperRange {
    public static void main(String[] args) {
        System.out.println("Byte Range: " + Byte.MIN_VALUE + " to " + Byte.MAX_VALUE);
        System.out.println("Short Range: " + Short.MIN_VALUE + " to " + Short.MAX_VALUE);
        System.out.println("Integer Range: " + Integer.MIN_VALUE + " to " + Integer.MAX_VALUE);
        System.out.println("Long Range: " + Long.MIN_VALUE + " to " + Long.MAX_VALUE);
        System.out.println("Float Range: " + Float.MIN_VALUE + " to " + Float.MAX_VALUE);
        System.out.println("Double Range: " + Double.MIN_VALUE + " to " + Double.MAX_VALUE);
        System.out.println("Character Range: " + (int) Character.MIN_VALUE + " to " + (int) Character.MAX_VALUE);
    }
}
```

#### **Output:**
```
Byte Range: -128 to 127
Short Range: -32768 to 32767
Integer Range: -2147483648 to 2147483647
Long Range: -9223372036854775808 to 9223372036854775807
Float Range: 1.4E-45 to 3.4028235E38
Double Range: 4.9E-324 to 1.7976931348623157E308
Character Range: 0 to 65535
```

---

### **Key Points**
- **Integer types (`Byte`, `Short`, `Integer`, `Long`)**: Store whole numbers.
- **Floating-point types (`Float`, `Double`)**: Store decimal numbers.
- **Character (`Character`)**: Uses Unicode values from `0` to `65535`.
- **Boolean (`Boolean`)**: Only two values: `true` and `false`.

## **Conclusion**
- Wrapper classes **convert primitives into objects**.
- They **provide useful methods** (`parseInt`, `valueOf`, etc.).
- **Autoboxing and unboxing** simplify conversion.
- They **inherit from `Number`**, except `Boolean` & `Character`.
- Using `==` with wrapper classes **may give unexpected results**.
