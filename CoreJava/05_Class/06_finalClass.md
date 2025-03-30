### **What is a `final` class in Java?**

In Java, the `final` keyword can be applied to a class, method, or variable. When applied to a class, the `final` keyword means that the class **cannot be subclassed or inherited**. In other words, you cannot extend a `final` class.

A `final` class is typically used when you want to make sure that the behavior of that class cannot be altered by subclasses. This is useful in situations where you want to maintain the integrity of the class and prevent modification of its behavior.

### **Key Points About Final Classes:**
1. **No Inheritance**: A `final` class cannot be extended. Attempting to subclass a `final` class results in a compile-time error.
2. **Cannot Be Subclassed**: You cannot create subclasses of a `final` class, which helps ensure that the class's behavior remains unchanged.
3. **Used for Immutable Classes**: `final` classes are often used to create immutable objects, where the state of the object should never change after it is created.

---

### **Example of a `final` Class in Java:**

```java
final class MathUtils {
    
    // Static utility method to calculate the square of a number
    public static int square(int number) {
        return number * number;
    }
    
    // Static utility method to calculate the cube of a number
    public static int cube(int number) {
        return number * number * number;
    }
    
    // Constructor (optional, final classes can have constructors)
    private MathUtils() {
        // Private constructor to prevent instantiation
        throw new UnsupportedOperationException("Cannot instantiate this class.");
    }
}

public class TestFinalClass {
    public static void main(String[] args) {
        // Accessing the static methods without instantiating the class
        System.out.println("Square of 4: " + MathUtils.square(4));
        System.out.println("Cube of 3: " + MathUtils.cube(3));
    }
}
```

### **Explanation:**
- The `MathUtils` class is declared as `final`, which means it cannot be subclassed.
- It provides utility methods `square()` and `cube()`.
- The constructor is private, which prevents instantiation of the class because the class is only meant to be used for its static methods.
- The class `MathUtils` is used directly in the `TestFinalClass` by calling its static methods.

### **Real-Time Use Cases of `final` Classes:**

1. **Utility or Helper Classes:**
   - Classes like `MathUtils` in the example are often made `final` to ensure that they cannot be extended. These classes are designed to provide utility methods or constants that do not require subclassing.
   - **Example:** The `java.lang.Math` class in Java is a real-world example of a `final` class. It contains methods like `Math.sqrt()`, `Math.pow()`, etc., that provide mathematical functions. It is declared as `final` so no one can subclass and modify its behavior.

2. **Immutable Classes:**
   - An immutable class is a class whose state cannot be changed once it is created. A `final` class helps in achieving immutability by preventing subclassing.
   - **Example:** The `String` class in Java is immutable and also `final`. This means you cannot subclass the `String` class, and its state (its content) cannot be changed after it is created.
   
   ```java
   public final class Employee {
       private final String name;
       private final int age;

       public Employee(String name, int age) {
           this.name = name;
           this.age = age;
       }

       public String getName() {
           return name;
       }

       public int getAge() {
           return age;
       }

       // Employee class cannot be subclassed, and its state is immutable
   }
   ```

3. **Security:**
   - `final` classes are often used in security-related applications where the class's behavior should not be tampered with or extended. By preventing subclassing, it reduces the risk of modifying important methods or adding unwanted behavior.
   - **Example:** The `java.security` package contains several `final` classes to prevent subclassing and modification of critical security functionality.

4. **Singleton Pattern:**
   - In the Singleton design pattern, a `final` class is often used for the singleton class to prevent subclassing. Additionally, the constructor is made `private`, ensuring that only one instance of the class can be created.
   - **Example:** A class managing a database connection might use the Singleton pattern, and by marking it `final`, you ensure that no subclass can change its behavior.

---

### **Example: Singleton Class with `final` Modifier**

```java
public final class DatabaseConnection {

    // The only instance of the class (Singleton pattern)
    private static DatabaseConnection instance;

    // Private constructor to prevent instantiation from other classes
    private DatabaseConnection() {
        System.out.println("Database Connection Established.");
    }

    // Method to provide access to the single instance of the class
    public static DatabaseConnection getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection();
        }
        return instance;
    }

    // Method to simulate some functionality
    public void queryDatabase() {
        System.out.println("Running database query...");
    }
}

public class TestSingleton {
    public static void main(String[] args) {
        // Accessing the single instance of the DatabaseConnection class
        DatabaseConnection connection = DatabaseConnection.getInstance();
        connection.queryDatabase();
        
        // Trying to create a second instance will return the same instance
        DatabaseConnection secondConnection = DatabaseConnection.getInstance();
        secondConnection.queryDatabase();
    }
}
```

### **Explanation of the Singleton Example:**
- The class `DatabaseConnection` is declared as `final` to prevent subclassing.
- The class has a **private static instance** which ensures that only one instance of the class is created (Singleton pattern).
- The **private constructor** prevents other classes from creating instances of `DatabaseConnection`.
- The `getInstance()` method ensures that only one instance of the class is returned.
- In the `TestSingleton` class, both `connection` and `secondConnection` refer to the same object, enforcing the Singleton design.

### **Advantages of Using `final` Class:**

1. **Immutability**: The `final` class guarantees that the class cannot be subclassed, and if it is designed to be immutable, it ensures that no one can change its state.
2. **Security**: By making a class `final`, you ensure that no subclass can alter its critical methods or override its functionality, which is important in security-related classes.
3. **Predictability**: A `final` class ensures that its behavior remains consistent throughout the application, as it cannot be subclassed or changed.
4. **Optimization**: The Java compiler can optimize `final` classes better since the class hierarchy is fixed.

---

### **When Not to Use a `final` Class:**
1. **If you need to allow subclassing**: If you want your class to be extended and have custom implementations, you should not declare it as `final`.
2. **If you want to allow polymorphism**: Declaring a class as `final` would prevent other classes from inheriting and using polymorphism.

---

### **Conclusion:**

A `final` class in Java is a class that cannot be subclassed. It is often used for utility classes, immutable classes, security purposes, and patterns like Singleton. By using `final`, you ensure that the behavior of the class remains unchanged and predictable. However, it should be used carefully when you do not need the class to be extended by other classes.

## final method
In Java, a **`final` method** is a method that cannot be overridden by any subclass. This is useful when you want to ensure that the behavior of a method remains consistent and is not altered by any subclass.

### **Key Points about `final` Methods:**
- A method declared as `final` cannot be overridden by any subclass.
- It can still be inherited by subclasses, but its implementation cannot be changed.
- The `final` keyword ensures that the method’s behavior remains unchanged in subclasses, which is useful for providing a **guaranteed implementation**.

### **Syntax:**
```java
public final returnType methodName() {
    // method body
}
```

### **Example of a `final` Method in Java:**

```java
class Animal {
    // A final method that cannot be overridden
    public final void sound() {
        System.out.println("This animal makes a sound.");
    }
}

class Dog extends Animal {
    // This will cause a compile-time error because the sound method is final in the Animal class
    // public void sound() {
    //     System.out.println("The dog barks.");
    // }

    public void display() {
        System.out.println("This is a dog.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.sound();  // Calls the final method from the parent class
        dog.display();  // Calls the non-final method from the Dog class
    }
}
```

### **Output:**
```
This animal makes a sound.
This is a dog.
```

### **Explanation:**
1. **`sound()` method in the `Animal` class**: This method is declared as `final`, so it cannot be overridden by any subclass (like the `Dog` class).
2. In the **`Dog` class**, if you try to override the `sound()` method, the code will not compile because the `sound()` method in the `Animal` class is `final`.
3. You can still call the `sound()` method from the `Dog` class because it inherits this method from the `Animal` class, but the method's implementation cannot be modified in `Dog`.

### **Key Takeaways:**
- A **`final` method** ensures that the behavior of the method cannot be changed in any subclass.
- It can be inherited, but not overridden.
- This feature is helpful in scenarios where you want to preserve the original behavior of a method and prevent subclasses from modifying it.

### **Real-World Example:**
In a security-related system, you may want to create a **`final` method** for logging, ensuring that the way logging is done in a parent class cannot be changed by subclasses to avoid tampering with the logging process.

```java
class Logger {
    // A final method to ensure logging behavior is fixed
    public final void logMessage(String message) {
        System.out.println("Logging message: " + message);
    }
}

class SpecialLogger extends Logger {
    // Trying to override the final method will cause a compile-time error
    // public void logMessage(String message) {
    //     System.out.println("Special logging: " + message);  // Error!
    // }
}
```

In this case, the `logMessage` method will always log the message in the same way, ensuring consistency and security across any subclass that inherits `Logger`.

## final variable (constant variable)
 **`final` variable** in Java is often used to create **constant variables**, but there are important nuances and distinctions. Let's break it down:

### **Similarities Between `final` Variables and Constants:**

1. **Immutability**: 
   - A `final` variable cannot be reassigned after it is initialized. This is similar to how a constant is defined (i.e., a value that should not change throughout the program).
   
2. **Value Cannot Change**:
   - Once you assign a value to a `final` variable, you cannot modify it. This is a characteristic of constants — their value remains the same throughout the program.

### **Key Differences Between `final` Variables and Constants**:

1. **Definition**:
   - A **constant** is a variable that holds a fixed value which doesn't change, usually associated with some specific value like `PI`, `MAX_VALUE`, etc.
   - A **`final` variable** is simply a variable whose value cannot be reassigned after initialization. You can have a `final` variable that isn't technically a constant (e.g., a `final` instance variable that can be initialized dynamically).

2. **Convention**:
   - While **`final` variables** can be used as constants, the **convention** for **constants** in Java is to use **uppercase letters** and words separated by underscores. For example, `final int MAX_USERS = 100;` is typically considered a **constant** in Java.
   - In Java, **constants** are generally declared as `public static final` to make them universally accessible across the application.

### **Creating Constants Using `final`**:

To define a constant in Java, we typically declare it as a **`public static final`** variable. The `static` keyword ensures that the constant belongs to the class rather than an instance of the class, and the `final` keyword ensures that the value cannot be changed once assigned.

### **Example**:

```java
public class MathConstants {
    // A constant PI
    public static final double PI = 3.14159;

    // A constant maximum number of users
    public static final int MAX_USERS = 100;
}

public class Main {
    public static void main(String[] args) {
        System.out.println("Value of PI: " + MathConstants.PI);
        System.out.println("Max Users: " + MathConstants.MAX_USERS);
        
        // These will cause a compile-time error
        // MathConstants.PI = 3.14;  // Error: Cannot assign a value to final variable 'PI'
        // MathConstants.MAX_USERS = 150;  // Error: Cannot assign a value to final variable 'MAX_USERS'
    }
}
```

### **Output**:
```
Value of PI: 3.14159
Max Users: 100
```

### **Key Points in the Example**:
- `PI` and `MAX_USERS` are both declared as **`public static final`**, meaning they are **constants**.
- The `final` keyword makes sure these variables cannot be modified after their initial assignment.
- The **`static` keyword** ensures that they belong to the class and are shared across all instances.

### **Summary**:
- A **`final` variable** can be considered a constant **if it follows the convention** (e.g., using `public static final` and uppercase letters).
- **Not all `final` variables are constants**; a `final` instance variable, for example, can still be initialized dynamically, and its value cannot change after initialization. 
- **Constants** are typically defined using `public static final` to ensure they are constant across the application.

In short: While **all constants are `final` variables**, **not all `final` variables are constants** (unless they are declared according to the constant naming conventions).
