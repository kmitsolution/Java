### **Inner Class in Java**

An **inner class** in Java is a class that is declared **inside another class**. Inner classes are used for better encapsulation and organization of code, providing a logical grouping of related functionality.

#### **Types of Inner Classes in Java**
1. **Member Inner Class**
2. **Static Nested Class**
3. **Local Inner Class**
4. **Anonymous Inner Class**

---

### **1. Member Inner Class**
A **member inner class** is a non-static class defined inside another class. It has access to all members of the outer class, including private members.

#### **Example:**
```java
class Outer {
    private String message = "Hello from Outer class";

    class Inner {
        void display() {
            System.out.println(message); // Accessing private member of Outer class
        }
    }

    public static void main(String[] args) {
        Outer outer = new Outer();
        Outer.Inner inner = outer.new Inner(); // Creating Inner class object
        inner.display();
    }
}
```
**Output:**
```
Hello from Outer class
```

---

### **2. Static Nested Class**
A **static nested class** is a static member of the outer class. Unlike a regular inner class, it **does not have access to instance members** of the outer class.

#### **Example:**
```java
class Outer {
    static String staticMessage = "Hello from Static Nested Class";

    static class StaticInner {
        void display() {
            System.out.println(staticMessage);
        }
    }

    public static void main(String[] args) {
        Outer.StaticInner inner = new Outer.StaticInner(); // Directly creating object
        inner.display();
    }
}
```
**Output:**
```
Hello from Static Nested Class
```

---

### **3. Local Inner Class**
A **local inner class** is defined inside a method and is only accessible within that method.

#### **Example:**
```java
class Outer {
    void outerMethod() {
        class LocalInner {
            void display() {
                System.out.println("Inside Local Inner Class");
            }
        }
        LocalInner local = new LocalInner();
        local.display();
    }

    public static void main(String[] args) {
        Outer outer = new Outer();
        outer.outerMethod();
    }
}
```
**Output:**
```
Inside Local Inner Class
```

---

### **4. Anonymous Inner Class**
An **anonymous inner class** is an unnamed class that is instantiated in a single expression. It is commonly used with **interfaces or abstract classes**.

#### **Example:**
```java
abstract class AnonymousDemo {
    abstract void display();
}

public class Test {
    public static void main(String[] args) {
        AnonymousDemo obj = new AnonymousDemo() { // Anonymous Inner Class
            void display() {
                System.out.println("Inside Anonymous Inner Class");
            }
        };
        obj.display();
    }
}
```
**Output:**
```
Inside Anonymous Inner Class
```

---

### **When to Use Inner Classes?**
- When a class is useful only to **one** other class.
- When you want to increase **encapsulation**.
- When you want to logically group classes that belong together.
- Anonymous inner classes are useful for event handling and callbacks.

Would you like more details on any of these? 🚀
