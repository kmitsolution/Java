### **FAQ on Interfaces in Java**  

#### **1. What is an interface in Java?**  
An **interface** in Java is a collection of **abstract methods** that a class can implement. It defines a contract that implementing classes must follow.

#### **2. How do you declare an interface?**  
An interface is declared using the `interface` keyword:  
```java
interface Animal {
    void makeSound(); // Abstract method (no body)
}
```

#### **3. Can an interface have a constructor?**  
❌ **No**, interfaces **cannot have constructors** because they cannot have instance variables.

#### **4. Can an interface have variables?**  
✅ **Yes**, but all variables are **public, static, and final** by default:  
```java
interface Test {
    int VALUE = 10; // Equivalent to: public static final int VALUE = 10;
}
```

#### **5. Can a class implement multiple interfaces?**  
✅ **Yes**, Java allows multiple interface implementations.  
```java
interface A { void methodA(); }
interface B { void methodB(); }

class C implements A, B {
    public void methodA() { System.out.println("Method A"); }
    public void methodB() { System.out.println("Method B"); }
}
```

#### **6. Can an interface extend another interface?**  
✅ **Yes**, an interface can extend multiple interfaces.  
```java
interface A { void methodA(); }
interface B extends A { void methodB(); }
```

#### **7. What is a default method in an interface?**  
A **default method** (Java 8+) allows interfaces to have method implementations.  
```java
interface Vehicle {
    default void show() {
        System.out.println("Default method in interface.");
    }
}
```

#### **8. What is a functional interface?**  
A **functional interface** has **exactly one abstract method** (used in Lambda expressions).  
```java
@FunctionalInterface
interface Calculator {
    int add(int a, int b);
}
```

#### **9. What is a marker interface?**  
A **marker interface** has **no methods** but provides metadata. Example: `Serializable`.  
```java
class Student implements Serializable { }
```

#### **10. Can an interface contain static methods?**  
✅ **Yes**, interfaces can have **static methods** (Java 8+).  
```java
interface Demo {
    static void show() {
        System.out.println("Static method in interface.");
    }
}
```

---

## **Difference Between Interface and Abstract Class**
| Feature | Interface | Abstract Class |
|---------|----------|---------------|
| **Methods** | Only abstract (Java 8+ allows default/static) | Can have abstract & concrete methods |
| **Constructors** | ❌ No | ✅ Yes |
| **Variables** | Public, static, final | Can have instance variables |
| **Inheritance** | Can be implemented by multiple classes | Only one class can extend it |
| **Usage** | Defines behavior, contract | Used for code reuse and partial abstraction |

## **Difference Between Variables in Interface and Abstract Class**  

### **Key Differences:**
| Feature | Interface | Abstract Class |
|---------|----------|---------------|
| **Variable Type** | `public static final` by default (constant) | Can be `private`, `protected`, `public`, and non-final |
| **Instance Variables** | ❌ Not allowed | ✅ Allowed |
| **Static Variables** | ✅ Always static | ✅ Can be static or non-static |
| **Modification** | ❌ Cannot change (final) | ✅ Can be modified |

---

## **Example: Variables in Interface vs Abstract Class**

### **1. Interface Variables Example**
```java
interface Animal {
    int LEGS = 4; // public static final by default

    void sound();
}

class Dog implements Animal {
    public void sound() {
        System.out.println("Dog barks");
    }
    
    void showLegs() {
        // LEGS = 5; // ❌ Error: Cannot modify final variable
        System.out.println("A dog has " + LEGS + " legs.");
    }
}

public class Test {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.sound();
        d.showLegs();
    }
}
```
### **Output:**
```
Dog barks
A dog has 4 legs.
```
✅ **Key Takeaway:**  
- `LEGS` is **final** (cannot be changed).  
- It's **static**, so it belongs to the interface and not the implementing class.

---

### **2. Abstract Class Variables Example**
```java
abstract class Animal {
    int legs = 4;  // Instance variable (modifiable)
    static int staticVar = 10; // Static variable

    abstract void sound();
}

class Cat extends Animal {
    public void sound() {
        System.out.println("Cat meows");
    }

    void showLegs() {
        legs = 3; // ✅ Allowed, can modify instance variables
        System.out.println("A cat has " + legs + " legs.");
    }
}

public class Test {
    public static void main(String[] args) {
        Cat c = new Cat();
        c.sound();
        c.showLegs();
        
        Animal.staticVar = 20; // ✅ Can modify static variables
        System.out.println("Static variable: " + Animal.staticVar);
    }
}
```
### **Output:**
```
Cat meows
A cat has 3 legs.
Static variable: 20
```
✅ **Key Takeaway:**  
- Abstract classes can have **instance variables** that can be modified.  
- **Static variables** can be changed.

---

## **Conclusion**
| Feature | Interface | Abstract Class |
|---------|----------|---------------|
| **Default Modifier** | `public static final` | Can be `private`, `protected`, `public` |
| **Instance Variables** | ❌ Not allowed | ✅ Allowed |
| **Static Variables** | ✅ Always static | ✅ Can be static or non-static |
| **Modifiable?** | ❌ No (final) | ✅ Yes |

