# **Enums in Java**  

An **enum (enumeration)** in Java is a special data type that represents a **fixed set of constant values**. It is used when you need to define a collection of constants with meaningful names.

---

## **1. Declaring an Enum**
Enums are defined using the `enum` keyword.

### **Example: Basic Enum**
```java
enum Day {
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY;
}

public class Test {
    public static void main(String[] args) {
        Day today = Day.MONDAY;
        System.out.println("Today is: " + today);
    }
}
```
### **Output:**
```
Today is: MONDAY
```
✅ **Key Points:**  
- Enum constants are **public, static, and final** by default.  
- Enums **cannot be instantiated** like regular classes.

---

## **2. Using Enums in a Switch Statement**
Enums work well with `switch` statements.

```java
enum Size {
    SMALL, MEDIUM, LARGE;
}

public class Test {
    public static void main(String[] args) {
        Size tshirtSize = Size.MEDIUM;

        switch (tshirtSize) {
            case SMALL:
                System.out.println("Small size selected.");
                break;
            case MEDIUM:
                System.out.println("Medium size selected.");
                break;
            case LARGE:
                System.out.println("Large size selected.");
                break;
        }
    }
}
```
### **Output:**
```
Medium size selected.
```

---

## **3. Enum with Methods**
Enums can have **constructors, fields, and methods**.

```java
enum Color {
    RED("#FF0000"),
    GREEN("#00FF00"),
    BLUE("#0000FF");

    private String hexCode; // Variable inside enum

    // Constructor
    Color(String hexCode) {
        this.hexCode = hexCode;
    }

    public String getHexCode() {
        return hexCode;
    }
}

public class Test {
    public static void main(String[] args) {
        System.out.println("Color RED Hex Code: " + Color.RED.getHexCode());
    }
}
```
### **Output:**
```
Color RED Hex Code: #FF0000
```
✅ **Key Points:**  
- Enums can have **fields and methods**.  
- Enum constructors are **private** (cannot create new instances).  

---

## **4. Iterating Over Enum Values**
You can loop through enum values using `values()`.

```java
enum Fruit {
    APPLE, BANANA, ORANGE;
}

public class Test {
    public static void main(String[] args) {
        for (Fruit f : Fruit.values()) {
            System.out.println(f);
        }
    }
}
```
### **Output:**
```
APPLE
BANANA
ORANGE
```

---

## **5. Enum Implementing an Interface**
Enums can implement interfaces, but cannot extend classes.

```java
interface Shape {
    void draw();
}

enum ShapeType implements Shape {
    CIRCLE, SQUARE;

    public void draw() {
        System.out.println("Drawing: " + this.name());
    }
}

public class Test {
    public static void main(String[] args) {
        ShapeType.CIRCLE.draw();
    }
}
```
### **Output:**
```
Drawing: CIRCLE
```

---

## **6. Difference Between Enum and Constants (`final static`)**
| Feature | Enum | `final static` Constants |
|---------|------|------------------|
| **Type Safety** | ✅ Type-safe | ❌ No type safety |
| **Grouping** | ✅ Groups related constants together | ❌ Scattered constants |
| **Methods** | ✅ Can have methods | ❌ Only values |
| **Switch Support** | ✅ Works in `switch` | ✅ Works in `switch` |

### **Example: Enum vs `final static` Constants**
#### **Using `final static` Constants (Not Recommended)**
```java
class Constants {
    public static final int RED = 1;
    public static final int GREEN = 2;
    public static final int BLUE = 3;
}
```
❌ **Issue:** Can accidentally assign any integer value, causing errors.

#### **Using Enums (Recommended)**
```java
enum Color {
    RED, GREEN, BLUE;
}
```
✅ **Benefit:** Prevents invalid values.

---

## **Conclusion**
| Feature | Enum |
|---------|------|
| **Purpose** | Defines a set of constants |
| **Type Safety** | ✅ Yes |
| **Allows Methods** | ✅ Yes |
| **Used in Switch** | ✅ Yes |
| **Prevents Modification** | ✅ Yes (Constants are final) |

Enums provide **type safety, better organization, and flexibility** over traditional constants. Would you like more details or examples? 🚀
