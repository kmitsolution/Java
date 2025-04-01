# **Template (Generic Type) in Java**
### **What are Generics?**
Generics in Java allow you to define classes, interfaces, and methods **with type parameters**. This enables **type safety** and **code reusability** while working with different data types.

Before generics, developers used **Object type**, which required type casting and was prone to **ClassCastException** errors.

---

## **Advantages of Generics**
1. **Type Safety** – Prevents `ClassCastException` at runtime.
2. **Code Reusability** – The same code works for multiple data types.
3. **Eliminates Type Casting** – No need to manually cast objects.

---

## **1. Generic Class Example**
A generic class defines a **type parameter** `<T>` (T can be any type).

```java
// Generic class with type parameter <T>
class Box<T> {
    private T value;

    // Constructor
    public Box(T value) {
        this.value = value;
    }

    // Getter
    public T getValue() {
        return value;
    }
}

public class GenericExample {
    public static void main(String[] args) {
        // Using Integer type
        Box<Integer> intBox = new Box<>(10);
        System.out.println("Integer Value: " + intBox.getValue());

        // Using String type
        Box<String> strBox = new Box<>("Hello Generics");
        System.out.println("String Value: " + strBox.getValue());
    }
}
```
### **Output**
```
Integer Value: 10
String Value: Hello Generics
```
> **Without Generics:** We would need to cast `Object` to `Integer` or `String`, which can cause runtime errors.

---

## **2. Generic Method Example**
A method can be generic **even if the class is not generic**.

```java
class Utility {
    // Generic method
    public static <T> void printArray(T[] array) {
        for (T item : array) {
            System.out.print(item + " ");
        }
        System.out.println();
    }
}

public class GenericMethodExample {
    public static void main(String[] args) {
        Integer[] intArr = {1, 2, 3, 4, 5};
        String[] strArr = {"Java", "Python", "C++"};

        // Calling generic method
        Utility.printArray(intArr);
        Utility.printArray(strArr);
    }
}
```
### **Output**
```
1 2 3 4 5 
Java Python C++ 
```
> The method `printArray(T[] array)` works with any type **without overloading**.

---

## **3. Generics with Inheritance**
Generics support **inheritance** just like normal classes.

### **Example: Generic Parent & Child Classes**
```java
// Generic Parent Class
class Parent<T> {
    T value;

    Parent(T value) {
        this.value = value;
    }

    void showValue() {
        System.out.println("Value: " + value);
    }
}

// Generic Child Class with the same type parameter
class Child<T> extends Parent<T> {
    Child(T value) {
        super(value);
    }

    void display() {
        System.out.println("Child class value: " + value);
    }
}

public class GenericInheritanceExample {
    public static void main(String[] args) {
        Child<Integer> intChild = new Child<>(100);
        intChild.showValue();  // Calls Parent method
        intChild.display();    // Calls Child method
    }
}
```
### **Output**
```
Value: 100
Child class value: 100
```
> The child class **inherits** the generic type `<T>` from the parent.

---

## **4. Bounded Type Generics (`extends` Keyword)**
We can **restrict** generic types using `extends` (for classes) or `implements` (for interfaces).

### **Example: Restrict to `Number` and Subclasses**
```java
// Bounded Generic Class (only for Number and its subclasses)
class Calculator<T extends Number> {
    private T num;

    Calculator(T num) {
        this.num = num;
    }

    void display() {
        System.out.println("Number: " + num);
    }
}

public class BoundedGenericExample {
    public static void main(String[] args) {
        Calculator<Integer> intCalc = new Calculator<>(10);
        Calculator<Double> doubleCalc = new Calculator<>(5.5);

        intCalc.display();
        doubleCalc.display();

        // Calculator<String> strCalc = new Calculator<>("Test"); // ❌ Compilation Error
    }
}
```
### **Output**
```
Number: 10
Number: 5.5
```
> `Calculator<T extends Number>` ensures that only **Integer, Double, Float, etc.** can be used.

---

## **5. Wildcards (`?`) in Generics**
Wildcards allow **flexibility** when working with generics.

### **Example: Upper Bounded Wildcard (`? extends T`)**
```java
import java.util.*;

class WildcardExample {
    public static void printList(List<? extends Number> list) {
        for (Number num : list) {
            System.out.print(num + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        List<Integer> intList = Arrays.asList(1, 2, 3);
        List<Double> doubleList = Arrays.asList(1.1, 2.2, 3.3);

        printList(intList);   // ✅ Allowed
        printList(doubleList); // ✅ Allowed
    }
}
```
### **Output**
```
1 2 3 
1.1 2.2 3.3 
```
> `? extends Number` allows `Integer`, `Double`, etc., but prevents `String`.

---

## **Summary**
| Concept | Description |
|---------|------------|
| **Generic Class** | A class with a type parameter `<T>` to support multiple data types |
| **Generic Method** | A method with a type parameter `<T>`, independent of class generics |
| **Generic Inheritance** | Generic child classes can extend generic parent classes |
| **Bounded Type (`extends`)** | Restricts generics to specific types (e.g., `T extends Number`) |
| **Wildcard (`?`)** | Allows flexibility in method arguments (`? extends Number`, `? super T`) |

---

## **Conclusion**
- **Generics make Java more type-safe** by preventing runtime type errors.
- **Code reusability** improves since one class/method works with multiple data types.
- **Bounded generics and wildcards** allow flexible yet safe type control.

