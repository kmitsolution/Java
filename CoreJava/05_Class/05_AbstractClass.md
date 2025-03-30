### **Abstract Class in Java**

An **abstract class** in Java is a class that cannot be instantiated on its own and is meant to be subclassed by other classes. It can contain both abstract methods (methods without implementation) and concrete methods (methods with implementation). Abstract classes are useful when you want to provide a common base for other classes to extend, while still allowing each subclass to provide its specific implementation of certain methods.

Here's a breakdown of the key concepts and an example of how to use **abstract classes** in Java:

1. **Abstract Method**: A method that has no body and must be implemented by subclasses.
2. **Concrete Method**: A method that has a body (implementation) and may or may not be overridden by subclasses.
3. **Constructor**: Abstract classes can have constructors that can be called by subclasses during instantiation.
4. **Destructor**: Java does not have destructors in the traditional sense, but you can define the `finalize()` method (which is part of garbage collection) if you need cleanup before an object is destroyed (although its use is discouraged).

### **Example of Abstract Class in Java**

Let's go step by step through the example:

#### **1. Define the Abstract Class**

```java
// Abstract class Animal
abstract class Animal {
    // Instance variables (fields)
    String name;
    int age;

    // Constructor of the abstract class
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Abstract method (doesn't have a body)
    public abstract void sound();

    // Concrete method
    public void sleep() {
        System.out.println(name + " is sleeping.");
    }

    // Concrete method with a default behavior
    public void introduce() {
        System.out.println("I am " + name + " and I am " + age + " years old.");
    }
}
```

- `sound()` is an **abstract method**, so it doesn't have a body, and it must be implemented by any subclass.
- `sleep()` and `introduce()` are **concrete methods** with actual behavior.

#### **2. Create Subclasses that Extend the Abstract Class**

Now, let's create specific subclasses (e.g., `Dog` and `Cat`) that extend the abstract class `Animal` and provide implementations for the abstract method `sound()`.

```java
// Dog class inherits from Animal
class Dog extends Animal {

    // Constructor for Dog class
    public Dog(String name, int age) {
        super(name, age); // Call the parent class constructor
    }

    // Implement the abstract method sound
    @Override
    public void sound() {
        System.out.println(name + " says Woof!");
    }

    // A specific method for Dog class
    public void fetch() {
        System.out.println(name + " is fetching the ball.");
    }
}

// Cat class inherits from Animal
class Cat extends Animal {

    // Constructor for Cat class
    public Cat(String name, int age) {
        super(name, age); // Call the parent class constructor
    }

    // Implement the abstract method sound
    @Override
    public void sound() {
        System.out.println(name + " says Meow!");
    }

    // A specific method for Cat class
    public void scratch() {
        System.out.println(name + " is scratching.");
    }
}
```

- Both `Dog` and `Cat` **extend** the `Animal` class and provide an implementation for the abstract `sound()` method.
- They also have their own specific methods (`fetch()` for `Dog` and `scratch()` for `Cat`).

#### **3. Demonstrating Abstract Class Usage**

Now let's create a test class where we create instances of `Dog` and `Cat` and call their methods.

```java
public class TestAnimal {
    public static void main(String[] args) {
        // Create Dog and Cat objects
        Dog dog = new Dog("Rex", 5);
        Cat cat = new Cat("Whiskers", 3);

        // Calling methods
        dog.introduce();    // Calls the method from Animal
        dog.sound();        // Calls the overridden method in Dog
        dog.sleep();        // Calls the method from Animal
        dog.fetch();        // Calls the specific method in Dog

        System.out.println(); // Print a blank line between animal outputs

        cat.introduce();     // Calls the method from Animal
        cat.sound();         // Calls the overridden method in Cat
        cat.sleep();         // Calls the method from Animal
        cat.scratch();       // Calls the specific method in Cat
    }
}
```

### **Explanation of the Output:**

1. When the `dog.introduce()` is called, it uses the `introduce()` method from the `Animal` class to print the dog's name and age.
2. When `dog.sound()` is called, it invokes the `sound()` method that is overridden in the `Dog` class to print "Woof!".
3. Similarly, `cat.sound()` will print "Meow!" since it’s implemented in the `Cat` class.

### **Sample Output:**
```plaintext
I am Rex and I am 5 years old.
Rex says Woof!
Rex is sleeping.
Rex is fetching the ball.

I am Whiskers and I am 3 years old.
Whiskers says Meow!
Whiskers is sleeping.
Whiskers is scratching.
```

### **Key Points:**
- **Abstract Class**: Can't be instantiated, but can contain both abstract and concrete methods.
- **Abstract Method**: Must be implemented in subclasses.
- **Constructor in Abstract Class**: Can be used to initialize fields in the abstract class, and is called from the constructor of the subclass.
- **Destructor**: Java does not use destructors explicitly, but you can override `finalize()` for resource cleanup (though its usage is discouraged in modern Java).

### **Summary:**
- Abstract classes provide a base class with common functionality while allowing subclasses to customize or override specific behaviors.
- Use **abstract methods** to enforce subclasses to provide specific behavior, and use **concrete methods** for default behavior that might be shared across subclasses.
- Subclasses of abstract classes must implement the abstract methods, but they can also call the concrete methods from the parent abstract class.
