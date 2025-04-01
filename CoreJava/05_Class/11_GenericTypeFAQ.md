# **FAQ on Generic Types in Java**

---

### **1. What are generics in Java?**
**Generics** allow Java classes, interfaces, and methods to work with **different data types** while ensuring **type safety** at compile time. Instead of using `Object` and performing manual casting, generics provide a way to define type parameters (`<T>`, `<E>`, etc.).

---

### **2. Why should we use generics?**
Generics offer several advantages:
- **Type Safety** – Prevents `ClassCastException` at runtime.
- **Code Reusability** – Write one generic class/method that works with multiple types.
- **Eliminates Type Casting** – No need to manually cast objects.

Example **without** generics:
```java
List list = new ArrayList();
list.add("Hello");
// Requires casting
String str = (String) list.get(0);
```
Example **with** generics:
```java
List<String> list = new ArrayList<>();
list.add("Hello");
// No casting needed
String str = list.get(0);
```

---

### **3. What is the syntax for a generic class?**
A generic class uses **angle brackets `<T>`** to define a type parameter.

Example:
```java
class Box<T> {
    private T value;

    public Box(T value) { this.value = value; }

    public T getValue() { return value; }
}
```

Usage:
```java
Box<Integer> intBox = new Box<>(10);
Box<String> strBox = new Box<>("Hello");
```

---

### **4. Can we have multiple type parameters in generics?**
Yes, you can use multiple type parameters.

Example:
```java
class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() { return key; }
    public V getValue() { return value; }
}
```
Usage:
```java
Pair<Integer, String> pair = new Pair<>(1, "One");
System.out.println(pair.getKey() + " = " + pair.getValue());
```

---

### **5. What is a generic method?**
A generic method has its **own type parameter** independent of the class.

Example:
```java
class Utility {
    public static <T> void printArray(T[] arr) {
        for (T item : arr) {
            System.out.print(item + " ");
        }
        System.out.println();
    }
}
```
Usage:
```java
Integer[] numbers = {1, 2, 3};
String[] words = {"Java", "Python"};

Utility.printArray(numbers);
Utility.printArray(words);
```

---

### **6. What is bounded type in generics (`extends` keyword)?**
Bounded types restrict generics to a specific **class hierarchy** using `extends`.

Example:
```java
class Calculator<T extends Number> { // Only Number and subclasses allowed
    private T num;

    public Calculator(T num) {
        this.num = num;
    }

    public double square() {
        return num.doubleValue() * num.doubleValue();
    }
}
```
Usage:
```java
Calculator<Integer> intCalc = new Calculator<>(4);
Calculator<Double> doubleCalc = new Calculator<>(5.5);
```
> **❌ Error:** `Calculator<String> strCalc = new Calculator<>("Hello");`  
> **Reason:** `String` is not a subclass of `Number`.

---

### **7. What are wildcards (`?`) in generics?**
Wildcards allow generics to be more flexible in method arguments.

#### **(a) Upper Bounded Wildcard (`? extends T`)**
Allows any type that **is T or a subclass of T**.
```java
void display(List<? extends Number> list) { ... }
```
Usage:
```java
display(Arrays.asList(10, 20, 30)); // List<Integer>
display(Arrays.asList(5.5, 6.6));   // List<Double>
```

#### **(b) Lower Bounded Wildcard (`? super T`)**
Allows any type that **is T or a superclass of T**.
```java
void addNumbers(List<? super Integer> list) {
    list.add(10);
}
```
Usage:
```java
addNumbers(new ArrayList<Number>()); // Allowed
addNumbers(new ArrayList<Object>()); // Allowed
```

#### **(c) Unbounded Wildcard (`?`)**
Allows **any** type.
```java
void printList(List<?> list) { ... }
```
Usage:
```java
printList(new ArrayList<String>());
printList(new ArrayList<Integer>());
```

---

### **8. Can we create an array of generic types?**
No, Java **does not allow** generic array creation due to **type erasure**.

❌ **Invalid:**
```java
T[] arr = new T[10];  // Compilation error
```

✅ **Solution:** Use `Array.newInstance()`
```java
T[] arr = (T[]) java.lang.reflect.Array.newInstance(clazz, 10);
```

---

### **9. Can a generic class extend a non-generic class?**
Yes, a generic class can extend a non-generic class.

Example:
```java
class Parent { }
class Child<T> extends Parent { }
```

---

### **10. What is type erasure in generics?**
**Type Erasure** is a process where Java **removes generic type information** at runtime to maintain **backward compatibility**.

Example:
```java
List<String> list1 = new ArrayList<>();
List<Integer> list2 = new ArrayList<>();
```
At runtime, both `list1` and `list2` **become**:
```java
List list = new ArrayList();
```
This is why **generics are checked at compile time** but erased at runtime.

---

### **11. Can we use primitives with generics?**
No, generics **only work with reference types**, not primitives.

❌ **Invalid:** `List<int> list = new ArrayList<>();`  
✅ **Solution:** Use wrapper classes: `List<Integer> list = new ArrayList<>();`

---

### **12. What is the difference between `List<Object>` and `List<?>`?**
| Feature | `List<Object>` | `List<?>` |
|---------|--------------|------------|
| Accepts | Only `Object` and subclasses | Any type |
| Can add elements? | ✅ Yes | ❌ No (except `null`) |
| Example | `List<Object> list = new ArrayList<>();` | `List<?> list = new ArrayList<>();` |

---

### **13. Can a generic class implement an interface?**
Yes, a generic class can implement a generic or non-generic interface.

Example:
```java
interface MyInterface<T> {
    void show(T value);
}

class MyClass<T> implements MyInterface<T> {
    public void show(T value) {
        System.out.println(value);
    }
}
```
Usage:
```java
MyClass<String> obj = new MyClass<>();
obj.show("Hello Generics");
```

---

### **14. Can we use generics with exceptions?**
No, you **cannot** create generic exceptions because Java requires all exceptions to be **reifiable** (fully known at runtime).

❌ **Invalid:**
```java
class MyException<T> extends Exception { } // Compilation error
```

✅ **Solution:** Use generic methods instead.
```java
class ExceptionHandler {
    public static <T extends Exception> void throwException(T ex) throws T {
        throw ex;
    }
}
```

---

### **15. What are some commonly used generic classes in Java?**
Some common generic classes in Java’s **Collections Framework**:
- `List<E>` (ArrayList, LinkedList)
- `Set<E>` (HashSet, TreeSet)
- `Map<K, V>` (HashMap, TreeMap)
- `Queue<E>` (PriorityQueue, LinkedList)

---

## **Conclusion**
- Generics improve **type safety** and **code reusability**.
- `T`, `E`, `K, V` are commonly used **type parameters**.
- **Bounded types** (`extends`) restrict types.
- **Wildcards** (`?`) provide flexibility in method arguments.
- **Type erasure** removes generic types at runtime.

---

Let me know if you need more details! 🚀🔥
