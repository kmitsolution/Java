### **FAQ: Inner Classes in Java**  

#### **1. What is an inner class in Java?**  
An **inner class** is a class that is declared inside another class. It has access to the members (including private members) of the outer class.

#### **2. What are the different types of inner classes?**  
There are four types of inner classes:  
- **Member Inner Class** – A non-static class inside another class.  
- **Static Nested Class** – A static inner class that does not require an instance of the outer class.  
- **Local Inner Class** – A class declared inside a method, accessible only within that method.  
- **Anonymous Inner Class** – A class without a name, instantiated in a single expression.

#### **3. How do you create an object of a member inner class?**  
You need an instance of the outer class to create an object of a member inner class.  
```java
Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();
```

#### **4. Can an inner class access private members of the outer class?**  
Yes, an inner class can access **private members** of the outer class.  

#### **5. How is a static nested class different from a member inner class?**  
A **static nested class**:  
- Cannot access instance members of the outer class.  
- Can be instantiated without creating an instance of the outer class.  
A **member inner class**:  
- Can access all members of the outer class, including private ones.  
- Requires an instance of the outer class to be created.

#### **6. Can an inner class have a constructor?**  
Yes, an inner class can have its own **constructor**, just like any other class.

#### **7. Can an interface have an inner class?**  
Yes, an interface can contain a nested class, and it is implicitly **static**.  
```java
interface Example {
    class Inner {
        void show() {
            System.out.println("Inner class inside an Interface");
        }
    }
}
```

#### **8. What is the use of an anonymous inner class?**  
Anonymous inner classes are used for short-lived object creation, such as:  
- Implementing interfaces without creating a separate class.  
- Handling event listeners in GUI programming.  

Example:  
```java
Runnable r = new Runnable() {
    public void run() {
        System.out.println("Running thread");
    }
};
new Thread(r).start();
```

#### **9. Can an inner class extend another class or implement an interface?**  
Yes, an inner class can **extend another class** or **implement an interface** like any other class.

#### **10. Can we declare an interface inside a class?**  
Yes, an interface can be declared inside a class. This is called a **nested interface**.  
```java
class Outer {
    interface NestedInterface {
        void show();
    }
}
```

#### **11. When should I use inner classes?**  
Use inner classes when:  
- The inner class is logically associated with the outer class.  
- You need tighter encapsulation.  
- You want to improve code organization.  
- You want to create event listeners efficiently (e.g., anonymous inner classes).

#### **12. Can a method inside an inner class access a local variable from the enclosing method?**  
Yes, but the local variable must be **final** (Java 7) or **effectively final** (Java 8+).

#### **13. What are the advantages of inner classes?**  
- Improved encapsulation.  
- More readable and logically grouped code.  
- Can access all members of the outer class.

#### **14. What are the disadvantages of inner classes?**  
- Can make code more complex.  
- Difficult to debug if overused.  
- Increases memory usage (anonymous inner classes).  

---

Do you need more details on any specific topic? 😊
