### **Class Fundamentals in Java**

In Java, **classes** are blueprints for creating objects. A class defines the properties (also called fields or attributes) and behaviors (also called methods or functions) of the objects created from it. Java is an **object-oriented programming** (OOP) language, and the concept of classes is a core aspect of OOP. 

### **Basic Structure of a Class**

A simple class in Java contains fields (properties) and methods (functions) that define the state and behavior of objects of that class.

### **Class Components**:
1. **Fields/Properties**: These are the attributes or variables that define the state of the object.
2. **Methods**: These define the behavior or actions that an object can perform.
3. **Constructor**: A special method used to initialize an object when it's created.
4. **Access Modifiers**: These control the visibility and access level of the fields and methods. The most common access modifiers are `public`, `private`, `protected`, and `default`.

### **Example: A Simple Java Class**

```java
public class Car {
    // Fields/Properties
    private String brand;
    private String model;
    private int year;

    // Constructor to initialize the object
    public Car(String brand, String model, int year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
    }

    // Getter methods to access private fields
    public String getBrand() {
        return brand;
    }

    public String getModel() {
        return model;
    }

    public int getYear() {
        return year;
    }

    // Method to display car details
    public void displayDetails() {
        System.out.println("Car Details: " + year + " " + brand + " " + model);
    }
}
```

### **Explanation of the Class Components**:

1. **Fields/Properties**:
   - `private String brand;` — This field stores the brand of the car. It is marked `private`, meaning it can only be accessed within the class.
   - `private String model;` — This field stores the model of the car.
   - `private int year;` — This field stores the year of manufacture of the car.
   
   By making the fields `private`, we ensure encapsulation (data hiding), which means the fields cannot be accessed directly outside the class.

2. **Constructor**:
   - The constructor `public Car(String brand, String model, int year)` initializes the fields with the values provided when creating a new `Car` object.
   
3. **Methods**:
   - `public String getBrand()`, `public String getModel()`, `public int getYear()` — These are **getter** methods that allow controlled access to the private fields of the class. These methods return the value of the respective fields.
   - `public void displayDetails()` — This is a regular method that displays the details of the car using the values of the fields.

### **Creating and Using a Class Object**

To create an object of the `Car` class and use its methods, we use the **`new` operator**. The `new` operator allocates memory for the object and invokes the constructor to initialize it.

**Example of Creating and Using an Object**:

```java
public class Main {
    public static void main(String[] args) {
        // Create an object of the Car class using the 'new' keyword
        Car myCar = new Car("Toyota", "Corolla", 2020);

        // Access object methods to display details
        myCar.displayDetails();  // This calls the method displayDetails
    }
}
```

### **Explanation**:

1. **Creating the Object**:
   - `Car myCar = new Car("Toyota", "Corolla", 2020);`
   - The `new` keyword is used to create a new instance of the `Car` class.
   - The constructor `Car(String brand, String model, int year)` is called to initialize the `myCar` object with the specified values: `"Toyota"`, `"Corolla"`, and `2020`.
   
2. **Accessing Object Methods**:
   - `myCar.displayDetails();` — This calls the `displayDetails()` method on the `myCar` object, which prints the car's details to the console.

**Output**:
```
Car Details: 2020 Toyota Corolla
```

---

### **Access Modifiers in Java**

Java provides four types of **access modifiers**:

1. **`public`**:
   - When a member (field, method, or class) is marked `public`, it is accessible from any other class.
   - Example: `public String brand;`
   
2. **`private`**:
   - When a member is marked `private`, it is accessible only within the class where it is defined. No other class can directly access it.
   - Example: `private String model;`
   
3. **`protected`**:
   - A `protected` member is accessible within its own package and by subclasses (even if they are in different packages).
   - Example: `protected int year;`
   
4. **Default (Package-Private)**:
   - If no access modifier is specified, the member is accessible only within its package (this is the default access level).
   
### **Summary of Key Points**:

1. **`public`**: Makes fields and methods accessible from any other class.
2. **`private`**: Restricts access to fields and methods only within the class.
3. **`new` keyword**: Used to create an instance (object) of a class.
4. **Encapsulation**: Using `private` for fields and providing public methods (getters and setters) for controlled access.
5. **Constructor**: Initializes an object when it's created.
6. **Methods**: Define behaviors that an object can perform.

This encapsulation and object-oriented design allow you to create more secure, maintainable, and flexible programs.
