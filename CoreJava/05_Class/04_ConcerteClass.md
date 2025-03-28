### Concrete Class in Java

A **concrete class** is a class that has a complete implementation of all its methods. It is not abstract, meaning it can be instantiated directly. Concrete classes can contain fields, methods, constructors, and implement interfaces or extend abstract classes.

In contrast, an **abstract class** contains abstract methods (methods without implementation), which must be implemented by subclasses. Concrete classes provide the full implementation of all methods and can be instantiated without the need for subclassing.

### Example of a Concrete Class in Java:

```java
// Concrete class
public class Car {

    // Fields (Instance variables)
    private String make;
    private String model;
    private int year;
    
    // Constructor
    public Car(String make, String model, int year) {
        this.make = make;
        this.model = model;
        this.year = year;
    }
    
    // Getter methods
    public String getMake() {
        return make;
    }
    
    public String getModel() {
        return model;
    }
    
    public int getYear() {
        return year;
    }

    // Method to display car details
    public void displayCarDetails() {
        System.out.println("Car Details:");
        System.out.println("Make: " + make);
        System.out.println("Model: " + model);
        System.out.println("Year: " + year);
    }
    
    // Main method to create and use the Car class
    public static void main(String[] args) {
        // Create an instance (object) of the Concrete class Car
        Car car1 = new Car("Toyota", "Corolla", 2021);
        car1.displayCarDetails();  // Calling method of the concrete class
        
        // Create another instance of the Concrete class Car
        Car car2 = new Car("Honda", "Civic", 2020);
        car2.displayCarDetails();  // Calling method of the concrete class
    }
}
```

### Explanation:

1. **Fields/Variables**: The class has three instance variables: `make`, `model`, and `year` to represent the car's attributes.
2. **Constructor**: The constructor initializes these instance variables when a new object of `Car` is created.
3. **Methods**: 
   - Getter methods (`getMake`, `getModel`, `getYear`) are used to access the private fields.
   - `displayCarDetails` is a method that prints out the details of the car.
4. **Instantiation**: In the `main` method, two `Car` objects (`car1` and `car2`) are created, and their details are displayed.

### Output of the Program:
```
Car Details:
Make: Toyota
Model: Corolla
Year: 2021

Car Details:
Make: Honda
Model: Civic
Year: 2020
```

### Key Points:
- **Concrete class**: The `Car` class is a concrete class because it has fully implemented methods and can be instantiated.
- It does not contain any abstract methods, and you can create objects of this class directly.
