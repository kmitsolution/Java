# Factory Design Pattern
Factory Design Pattern is a creational design pattern that provides an interface for creating objects in a superclass but allows subclasses to alter the type of objects that will be created. In Java, this pattern is commonly implemented using either a simple Factory or a Factory Method.

Here's an example of a Factory Method pattern:
# Example 1

```java
// Interface for the product
interface Shape {
    void draw();
}

// Concrete implementations of the product
class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Inside Circle::draw() method.");
    }
}

class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Inside Square::draw() method.");
    }
}

// Factory class to create objects based on input
class ShapeFactory {
    public Shape getShape(String shapeType) {
        if (shapeType == null) {
            return null;
        }
        if (shapeType.equalsIgnoreCase("CIRCLE")) {
            return new Circle();
        } else if (shapeType.equalsIgnoreCase("SQUARE")) {
            return new Square();
        }
        return null;
    }
}

// Usage example
public class FactoryPatternExample {
    public static void main(String[] args) {
        ShapeFactory shapeFactory = new ShapeFactory();

        // Create a circle
        Shape circle = shapeFactory.getShape("CIRCLE");
        circle.draw();

        // Create a square
        Shape square = shapeFactory.getShape("SQUARE");
        square.draw();
    }
}
```

In this example:

- `Shape` is the interface representing the products (different shapes).
- `Circle` and `Square` are concrete implementations of the `Shape` interface.
- `ShapeFactory` is the factory class responsible for creating objects based on the input provided.

By calling `getShape()` method of `ShapeFactory` with different arguments, you can create different types of shapes without exposing the creation logic. This allows for easy extension when new shapes need to be added - you simply create a new class implementing `Shape` and update the factory to handle its creation.

This pattern helps in decoupling the object creation logic from the client code, making the code more maintainable and scalable.


# Example 2
Factory Design Pattern could be a `Logger` system in a software application.

Consider a scenario where you have different types of loggers - `FileLogger`, `DatabaseLogger`, and `ConsoleLogger`, each responsible for logging information to a different destination.

Here's a simplified example using the Factory Design Pattern:

```java
// Logger interface
interface Logger {
    void log(String message);
}

// Concrete implementations of Logger
class FileLogger implements Logger {
    @Override
    public void log(String message) {
        // Log message to a file
        System.out.println("Logging to file: " + message);
    }
}

class DatabaseLogger implements Logger {
    @Override
    public void log(String message) {
        // Log message to a database
        System.out.println("Logging to database: " + message);
    }
}

class ConsoleLogger implements Logger {
    @Override
    public void log(String message) {
        // Log message to the console
        System.out.println("Logging to console: " + message);
    }
}

// Logger Factory
class LoggerFactory {
    public Logger getLogger(String loggerType) {
        if (loggerType == null) {
            return null;
        }
        if (loggerType.equalsIgnoreCase("FILE")) {
            return new FileLogger();
        } else if (loggerType.equalsIgnoreCase("DATABASE")) {
            return new DatabaseLogger();
        } else if (loggerType.equalsIgnoreCase("CONSOLE")) {
            return new ConsoleLogger();
        }
        return null;
    }
}

// Usage example
public class LoggerExample {
    public static void main(String[] args) {
        LoggerFactory loggerFactory = new LoggerFactory();

        // Get File Logger
        Logger fileLogger = loggerFactory.getLogger("FILE");
        fileLogger.log("This is logged to a file.");

        // Get Database Logger
        Logger databaseLogger = loggerFactory.getLogger("DATABASE");
        databaseLogger.log("This is logged to a database.");

        // Get Console Logger
        Logger consoleLogger = loggerFactory.getLogger("CONSOLE");
        consoleLogger.log("This is logged to the console.");
    }
}
```

In this example:

- `Logger` is an interface that defines the contract for different loggers.
- `FileLogger`, `DatabaseLogger`, and `ConsoleLogger` are concrete implementations of the `Logger` interface.
- `LoggerFactory` is responsible for creating instances of different loggers based on the input provided.

This design allows the client to obtain the desired logger without knowing the exact implementation details. If a new type of logger needs to be added in the future, you can create a new implementation of `Logger` and update the `LoggerFactory` accordingly, without changing the client code.
