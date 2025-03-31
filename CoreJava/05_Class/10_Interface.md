## **Interfaces in Java**  

An **interface** in Java is a **blueprint** for a class that defines a set of **abstract methods** (methods without implementation). A class that implements an interface must provide implementations for all its methods.

### **Key Features of Interfaces:**
✅ **Supports multiple inheritance** (since a class can implement multiple interfaces).  
✅ **Only method declarations** (before Java 8).  
✅ **Cannot have constructors** (because they cannot have instance variables).  
✅ **All methods are public and abstract by default**.  
✅ **All variables are public, static, and final by default**.  

---

## **1. Declaring an Interface**
An interface is declared using the `interface` keyword.

```java
interface Animal {
    void makeSound(); // Abstract method (no body)
}
```

---

## **2. Implementing an Interface**
A class uses the `implements` keyword to define methods of an interface.

```java
class Dog implements Animal {
    public void makeSound() {
        System.out.println("Bark! Bark!");
    }
}

public class Test {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.makeSound(); // Output: Bark! Bark!
    }
}
```

---

## **3. Multiple Interfaces in Java**
A class can implement multiple interfaces.

```java
interface Animal {
    void eat();
}

interface Mammal {
    void walk();
}

class Human implements Animal, Mammal {
    public void eat() {
        System.out.println("Humans eat food.");
    }
    public void walk() {
        System.out.println("Humans walk on two legs.");
    }
}

public class Test {
    public static void main(String[] args) {
        Human person = new Human();
        person.eat();
        person.walk();
    }
}
```

---

## **4. Default and Static Methods in Interfaces (Java 8+)**
Java 8 introduced **default methods** (with implementation) and **static methods** inside interfaces.

```java
interface Vehicle {
    void start();
    
    default void show() {
        System.out.println("This is a vehicle.");
    }
    
    static void stop() {
        System.out.println("Vehicle stopped.");
    }
}

class Car implements Vehicle {
    public void start() {
        System.out.println("Car is starting...");
    }
}

public class Test {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.start();
        myCar.show(); // Calling default method
        Vehicle.stop(); // Calling static method
    }
}
```
**Output:**
```
Car is starting...
This is a vehicle.
Vehicle stopped.
```

---

## **5. Functional Interfaces (Java 8)**
A **functional interface** is an interface that has **exactly one abstract method** (used in **Lambda Expressions**).

```java
@FunctionalInterface
interface Calculator {
    int add(int a, int b);
}

public class LambdaExample {
    public static void main(String[] args) {
        Calculator sum = (a, b) -> a + b; // Lambda expression
        System.out.println("Sum: " + sum.add(5, 10));
    }
}
```

---

## **6. Marker Interface**
A **marker interface** is an empty interface (with no methods), used to indicate a special property.

Example: `Serializable` in Java.

```java
import java.io.Serializable;

class Student implements Serializable {
    int id;
    String name;
}
```

---

## **7. Differences Between Interface and Abstract Class**
| Feature | Interface | Abstract Class |
|---------|----------|---------------|
| **Methods** | Only abstract (Java 8 allows default/static) | Can have abstract & concrete methods |
| **Constructors** | No | Yes |
| **Variables** | Public, static, and final | Can have instance variables |
| **Inheritance** | Can be implemented by multiple classes | Only one class can extend it |
| **Usage** | Used for behavior | Used for common base functionality |

---

## **When to Use an Interface?**
- When multiple classes share **common behavior** but don’t need to share code.  
- When you want **multiple inheritance**.  
- When defining a **contract** for classes (e.g., in API development).  

