### **Garbage Collection in Java**

**Garbage Collection** in Java is the process of automatically reclaiming memory by deleting objects that are no longer in use (i.e., objects that are no longer reachable via any reference). This helps prevent memory leaks and ensures efficient memory management in applications.

#### Key Concepts:
- **Heap Memory**: All objects in Java are stored in the heap memory, which is dynamically managed.
- **Automatic Process**: The Java **Garbage Collector (GC)** runs in the background and handles memory management without requiring explicit intervention from the programmer.
- **Unreachable Objects**: An object becomes unreachable when there are no references pointing to it.
- **Finalization**: Before an object is garbage collected, Java can invoke a method called `finalize()` to allow the object to release resources (e.g., closing files, network connections).

#### Example of Garbage Collection:
```java
class Car {
    private String brand;

    public Car(String brand) {
        this.brand = brand;
    }

    public void displayDetails() {
        System.out.println("Car Brand: " + brand);
    }
}

public class Main {
    public static void main(String[] args) {
        Car car1 = new Car("Toyota");
        car1.displayDetails();

        // Setting car1 to null makes it eligible for garbage collection
        car1 = null;

        // Suggesting the JVM to run garbage collection (Note: This is not guaranteed to execute immediately)
        System.gc();  
    }
}
```

**Explanation**:
- Initially, `car1` is pointing to an object of type `Car`.
- When `car1` is set to `null`, the object becomes unreachable and is eligible for garbage collection.
- `System.gc()` is a **suggestion** to the JVM to run garbage collection, but it is not guaranteed to execute immediately or at all.

#### Output:
```
Car Brand: Toyota
```
The garbage collector will run in the background and free up memory occupied by the `Car` object once it's determined that the object is no longer in use.

---

### **finalize() Method in Java**

The **`finalize()`** method is a special method in the `Object` class that can be overridden by subclasses. It is called by the garbage collector before an object is reclaimed. This method can be used to perform cleanup tasks, such as releasing external resources (like closing file streams or database connections), just before the object is destroyed.

#### **Important Notes**:
- **Unpredictable**: The `finalize()` method is called by the garbage collector when it determines that an object is eligible for garbage collection. There is no guarantee of when or even whether `finalize()` will be invoked.
- **Deprecated in Java 9**: The `finalize()` method is considered unreliable and has been deprecated in newer versions of Java (Java 9 and later) in favor of using `try-with-resources` and explicitly managing resources.

#### Example of `finalize()` method:
```java
class Car {
    private String brand;

    public Car(String brand) {
        this.brand = brand;
    }

    public void displayDetails() {
        System.out.println("Car Brand: " + brand);
    }

    // Override finalize method to clean up resources before object is garbage collected
    @Override
    protected void finalize() {
        System.out.println("Finalizing resources for Car: " + brand);
    }
}

public class Main {
    public static void main(String[] args) {
        Car car1 = new Car("Toyota");
        car1.displayDetails();

        // Nullifying the reference to car1
        car1 = null;

        // Requesting garbage collection
        System.gc(); // Suggests garbage collection
    }
}
```

#### Explanation:
1. A `Car` object is created with the brand "Toyota".
2. The `car1` reference is set to `null`, which makes the `Car` object eligible for garbage collection.
3. The `finalize()` method is called by the garbage collector just before the object is destroyed, allowing any necessary cleanup to be performed.

#### Output (when garbage collection occurs):
```
Car Brand: Toyota
Finalizing resources for Car: Toyota
```

- In the output, the `finalize()` method is invoked before the object is garbage collected.
- The message "Finalizing resources for Car: Toyota" is printed when the garbage collector calls `finalize()`.

### **Important Considerations for `finalize()`**:
- **No Guarantee**: There is no guarantee that `finalize()` will be called. The JVM may decide not to call `finalize()` if it’s under memory pressure or if it doesn't need to collect the object.
- **Unpredictability**: The exact time when `finalize()` is invoked depends on when the garbage collector runs, which is not something you can control.
- **Resource Management**: It’s not recommended to rely on `finalize()` for resource management (e.g., closing files, database connections), as the timing is uncertain. Instead, Java provides other mechanisms like `try-with-resources` and explicit resource management.

---

### **Alternative to `finalize()` — `try-with-resources`**

Instead of relying on the `finalize()` method, Java introduced the **try-with-resources** statement in Java 7 to automatically manage resources like files, sockets, and database connections. Classes that need automatic cleanup should implement the `AutoCloseable` interface, and the resources will be automatically closed when the block finishes.

#### Example of try-with-resources:
```java
import java.io.*;

class Car implements AutoCloseable {
    private String brand;

    public Car(String brand) {
        this.brand = brand;
    }

    public void displayDetails() {
        System.out.println("Car Brand: " + brand);
    }

    @Override
    public void close() {
        System.out.println("Car object resources closed.");
    }
}

public class Main {
    public static void main(String[] args) {
        try (Car car1 = new Car("Toyota")) {
            car1.displayDetails();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

#### Explanation:
- The `Car` class implements the `AutoCloseable` interface and overrides the `close()` method to release resources.
- The `try-with-resources` block ensures that `car1` is automatically closed when the block completes.

#### Output:
```
Car Brand: Toyota
Car object resources closed.
```

---

### Conclusion:

- **Garbage Collection**: Java’s garbage collector automatically reclaims memory by collecting objects that are no longer in use. You can suggest garbage collection using `System.gc()`, but you cannot guarantee when it will occur.
- **finalize() Method**: The `finalize()` method is called before an object is garbage collected and can be used to perform cleanup tasks. However, it is unreliable and deprecated in newer versions of Java.
- **Resource Management**: Instead of relying on `finalize()`, it’s recommended to use `try-with-resources` and `AutoCloseable` for proper resource management.
