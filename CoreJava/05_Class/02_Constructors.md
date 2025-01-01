### Constructors in Java

In Java, a constructor is a special method used to initialize objects. A constructor is invoked when an object of a class is created. There are two main types of constructors in Java:

1. **Default Constructor**: A constructor that does not take any parameters. If you don’t define a constructor, Java provides a default one.
2. **Parameterized Constructor**: A constructor that takes parameters to initialize an object with specific values.
3. **Constructor Overloading**: When a class has multiple constructors with different parameter lists. Java uses the number and type of parameters to distinguish between constructors.

---

### **1. Default Constructor:**
A default constructor is provided by Java if no constructor is explicitly defined. It initializes object fields to default values (null for objects, 0 for integers, etc.).

#### Example:
```java
class Car {
    private String brand;
    private String model;
    private int year;

    // Default constructor
    public Car() {
        brand = "Unknown";
        model = "Unknown";
        year = 0;
    }

    public void displayDetails() {
        System.out.println(year + " " + brand + " " + model);
    }
}
```

#### Object Creation with Default Constructor:
```java
public class Main {
    public static void main(String[] args) {
        Car car1 = new Car();  // Using default constructor
        car1.displayDetails();  // Output: 0 Unknown Unknown
    }
}
```

### **2. Parameterized Constructor:**
A parameterized constructor allows us to pass values when creating an object, providing more flexibility in initializing the object.

#### Example:
```java
class Car {
    private String brand;
    private String model;
    private int year;

    // Parameterized constructor
    public Car(String brand, String model, int year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
    }

    public void displayDetails() {
        System.out.println(year + " " + brand + " " + model);
    }
}
```

#### Object Creation with Parameterized Constructor:
```java
public class Main {
    public static void main(String[] args) {
        Car car1 = new Car("Toyota", "Camry", 2022);  // Using parameterized constructor
        car1.displayDetails();  // Output: 2022 Toyota Camry
    }
}
```

### **3. Constructor Overloading:**
Constructor overloading in Java occurs when a class has multiple constructors, each with different parameter lists. Java will call the constructor based on the arguments passed during object creation.

#### Example:
```java
class Car {
    private String brand;
    private String model;
    private int year;

    // Constructor with no parameters
    public Car() {
        this.brand = "Unknown";
        this.model = "Unknown";
        this.year = 0;
    }

    // Constructor with parameters
    public Car(String brand, String model, int year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
    }

    // Constructor with brand and model only
    public Car(String brand, String model) {
        this.brand = brand;
        this.model = model;
        this.year = 0;  // Default year
    }

    public void displayDetails() {
        System.out.println(year + " " + brand + " " + model);
    }
}
```

#### Object Creation with Constructor Overloading:
```java
public class Main {
    public static void main(String[] args) {
        Car car1 = new Car();  // Using default constructor
        Car car2 = new Car("Honda", "Civic", 2021);  // Using parameterized constructor
        Car car3 = new Car("Ford", "Mustang");  // Using overloaded constructor

        car1.displayDetails();  // Output: 0 Unknown Unknown
        car2.displayDetails();  // Output: 2021 Honda Civic
        car3.displayDetails();  // Output: 0 Ford Mustang
    }
}
```

---

### **Class and Object Diagrams:**

#### **Class Diagram (for Car class):**

```
+----------------------+
|         Car           |
+----------------------+
| - brand: String      |
| - model: String      |
| - year: int          |
+----------------------+
| + Car()              |  --> Default constructor
| + Car(brand: String, |  --> Parameterized constructor
|   model: String,     |
|   year: int)         |
| + Car(brand: String, |  --> Constructor overloading
|   model: String)     |
| + displayDetails():  |
|   void               |
+----------------------+
```

#### **Object Diagram (for 3 car objects):**

Let's assume the following objects:

1. `car1`: Created with the default constructor.
2. `car2`: Created with the parameterized constructor.
3. `car3`: Created using the overloaded constructor (brand and model only).

```
+-----------------------------------+
|           car1: Car               |
+-----------------------------------+
| brand: "Unknown"                  |
| model: "Unknown"                  |
| year: 0                           |
+-----------------------------------+

+-----------------------------------+
|           car2: Car               |
+-----------------------------------+
| brand: "Honda"                    |
| model: "Civic"                    |
| year: 2021                        |
+-----------------------------------+

+-----------------------------------+
|           car3: Car               |
+-----------------------------------+
| brand: "Ford"                     |
| model: "Mustang"                  |
| year: 0                           |
+-----------------------------------+
```

### **Summary:**

- **Default Constructor** initializes objects with default values.
- **Parameterized Constructor** allows initializing objects with specific values at the time of creation.
- **Constructor Overloading** allows multiple constructors with different parameter lists.
