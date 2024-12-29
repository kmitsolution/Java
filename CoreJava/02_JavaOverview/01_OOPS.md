# Object Oriented Concepts in Java

Java's object-oriented programming (OOP) principles—**Abstraction**, **Encapsulation**, **Polymorphism**, and **Inheritance**—are foundational to writing reusable and maintainable code. I'll explain each concept using an example based around an **Animal** class, and I'll also include a simple diagram for better understanding.

### 1. **Abstraction**
Abstraction refers to hiding the complexity of the system and exposing only the necessary details. It is achieved by using abstract classes or interfaces. In the case of the **Animal** class, we might create a generic representation of an animal without providing specific details about each type of animal. Instead, we provide abstract methods that are implemented by subclasses.

**Example**:

```java
abstract class Animal {
    // Abstract method (does not have a body)
    abstract void sound();

    // Regular method
    public void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal {
    // Providing implementation of the abstract method
    void sound() {
        System.out.println("Bark");
    }
}

class Cat extends Animal {
    // Providing implementation of the abstract method
    void sound() {
        System.out.println("Meow");
    }
}
```

**Explanation**:
- The `Animal` class is **abstract** and contains an abstract method `sound()`. This method doesn't have a body, meaning that the specific implementation will be provided by subclasses (`Dog` and `Cat`).
- The `eat()` method is a regular method and can be used by all subclasses of `Animal`.
- `Dog` and `Cat` both extend `Animal` and implement the `sound()` method in their own way.

### 2. **Encapsulation**
Encapsulation is the concept of hiding the internal state of an object and requiring all interaction to be performed through methods. This helps ensure that an object's data is protected from unauthorized access and modification. In Java, encapsulation is achieved by declaring fields as `private` and providing `public` getter and setter methods.

**Example**:

```java
class Animal {
    private String name;  // Private field
    private int age;      // Private field

    // Getter method
    public String getName() {
        return name;
    }

    // Setter method
    public void setName(String name) {
        this.name = name;
    }

    // Getter method
    public int getAge() {
        return age;
    }

    // Setter method
    public void setAge(int age) {
        this.age = age;
    }
}
```

**Explanation**:
- The fields `name` and `age` are **private**, which means they cannot be accessed directly outside the class.
- Public getter and setter methods (`getName`, `setName`, `getAge`, `setAge`) are used to access and modify these private fields safely.

### 3. **Polymorphism**
Polymorphism allows objects to be treated as instances of their parent class, and it enables methods to behave differently based on the object’s actual class. There are two types of polymorphism in Java: **method overriding** and **method overloading**.

- **Method Overriding**: When a subclass provides a specific implementation of a method defined in its superclass.
- **Method Overloading**: When multiple methods in the same class have the same name but differ in the number or type of parameters.

**Example** (Method Overriding):

```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Meow");
    }
}
```

**Explanation**:
- Both `Dog` and `Cat` override the `sound()` method of `Animal`, providing their specific implementations.

**Example** (Method Overloading):

```java
class Animal {
    // Overloaded method with one parameter
    void sound(String type) {
        System.out.println("The " + type + " makes a sound");
    }

    // Overloaded method with two parameters
    void sound(String type, int volume) {
        System.out.println("The " + type + " makes a sound at volume " + volume);
    }
}
```

**Explanation**:
- The `sound()` method is **overloaded** to handle different argument types. You can call `sound()` with either one or two parameters, and it will behave differently based on the number of arguments passed.

### 4. **Inheritance**
Inheritance allows a new class (subclass) to inherit properties and behaviors (fields and methods) from an existing class (superclass). It promotes code reuse.

**Example**:

```java
class Animal {
    void sleep() {
        System.out.println("This animal is sleeping");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Woof!");
    }
}

class Cat extends Animal {
    void meow() {
        System.out.println("Meow!");
    }
}
```

**Explanation**:
- The `Dog` and `Cat` classes inherit the `sleep()` method from the `Animal` class.
- Both `Dog` and `Cat` add their own specific behaviors (`bark()` and `meow()`, respectively).

### Diagram:

Here’s a simplified diagram illustrating how these concepts work together with the **Animal** class:

```
                 +----------------------+
                 |      Animal          |  <-- Superclass
                 +----------------------+
                 | - name: String        |
                 | - age: int            |
                 +----------------------+
                 | + sound(): void       |  <-- Abstract method
                 | + eat(): void         |  <-- Regular method
                 | + getName(): String   |
                 | + setName(String)     |
                 | + getAge(): int       |
                 | + setAge(int)         |
                 +----------------------+
                        /    \
            +-----------------+----------------+
            |                                   |
    +-------------------+              +-------------------+
    |       Dog         |              |       Cat         |  
    +-------------------+              +-------------------+  
    | + sound(): void   |              | + sound(): void   |
    | + bark(): void    |              | + meow(): void    |
    +-------------------+              +-------------------+
```

### Explanation of the Diagram:
- **Animal Class** is the superclass with both **abstract** and **regular** methods, along with private fields.
- **Dog** and **Cat** are subclasses that inherit from `Animal` and override the `sound()` method.
- Both `Dog` and `Cat` can use the `eat()` method from the `Animal` class, showcasing **inheritance**.
- Encapsulation is illustrated by the private `name` and `age` fields, with public getters and setters.
- Polymorphism is demonstrated by the ability to call the `sound()` method, which behaves differently depending on whether it's a `Dog` or a `Cat`.

These OOP concepts—**Abstraction**, **Encapsulation**, **Polymorphism**, and **Inheritance**—are fundamental to Java and enable the creation of modular, reusable, and maintainable software.
