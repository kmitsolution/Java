### **Conditional Statements in Java**

Conditional statements allow us to make decisions in code based on certain conditions. In Java, there are several types of conditional statements: **`if`**, **`else`**, **`else if`**, and **`switch`**. These statements are used to control the flow of the program based on conditions.

### **1. `if` Statement**
The `if` statement evaluates a condition and executes the block of code inside it if the condition is `true`.

**Syntax**:
```java
if (condition) {
    // Code to execute if condition is true
}
```

**Example:**
```java
public class IfExample {
    public static void main(String[] args) {
        int number = 10;
        
        if (number > 0) {
            System.out.println("The number is positive.");
        }
    }
}
```

**Output:**
```
The number is positive.
```

---

### **2. `if`-`else` Statement**
The `if-else` statement provides an alternative set of actions. If the condition evaluates to `true`, the first block of code is executed, otherwise, the second block (else part) is executed.

**Syntax**:
```java
if (condition) {
    // Code to execute if condition is true
} else {
    // Code to execute if condition is false
}
```

**Example:**
```java
public class IfElseExample {
    public static void main(String[] args) {
        int number = -5;
        
        if (number > 0) {
            System.out.println("The number is positive.");
        } else {
            System.out.println("The number is negative.");
        }
    }
}
```

**Output:**
```
The number is negative.
```

---

### **3. `if`-`else if`-`else` Statement**
The `if-else if-else` statement is used when there are multiple conditions to check. The program will check each condition in sequence, and execute the block corresponding to the first `true` condition. If no condition is true, the `else` block is executed.

**Syntax**:
```java
if (condition1) {
    // Code to execute if condition1 is true
} else if (condition2) {
    // Code to execute if condition2 is true
} else {
    // Code to execute if neither condition1 nor condition2 is true
}
```

**Example:**
```java
public class IfElseIfExample {
    public static void main(String[] args) {
        int number = 0;
        
        if (number > 0) {
            System.out.println("The number is positive.");
        } else if (number < 0) {
            System.out.println("The number is negative.");
        } else {
            System.out.println("The number is zero.");
        }
    }
}
```

**Output:**
```
The number is zero.
```

---

### **4. `switch` Statement**
The `switch` statement is used to execute one out of many blocks of code based on the value of an expression. It is often used when there are multiple possible conditions that would each require different actions.

**Syntax**:
```java
switch (expression) {
    case value1:
        // Code to execute if expression equals value1
        break;
    case value2:
        // Code to execute if expression equals value2
        break;
    default:
        // Code to execute if expression doesn't match any case
}
```

- `expression`: The value or variable being tested.
- `case`: Each possible value that the expression could match.
- `break`: Ends the `switch` statement (if omitted, the program will "fall through" to the next case).
- `default`: An optional block that runs if no case matches.

**Example:**
```java
public class SwitchExample {
    public static void main(String[] args) {
        int day = 3;
        
        switch (day) {
            case 1:
                System.out.println("Monday");
                break;
            case 2:
                System.out.println("Tuesday");
                break;
            case 3:
                System.out.println("Wednesday");
                break;
            case 4:
                System.out.println("Thursday");
                break;
            case 5:
                System.out.println("Friday");
                break;
            case 6:
                System.out.println("Saturday");
                break;
            case 7:
                System.out.println("Sunday");
                break;
            default:
                System.out.println("Invalid day");
        }
    }
}
```

**Output:**
```
Wednesday
```

---

### **Key Differences Between `if` and `switch`**

- **`if`** is more flexible as it can evaluate more complex expressions and conditions, including logical operations and ranges.
- **`switch`** is useful for checking a single variable against a series of constant values. It is more efficient when there are many possible conditions for a single variable, especially if it's an integer or string.

### **Conclusion**

- **`if`** and **`else`** statements are used to execute code based on boolean conditions.
- **`else if`** allows checking multiple conditions.
- **`switch`** is used to select one block of code to execute from multiple possible options, based on the value of an expression.
  
These control flow statements are fundamental to creating conditional logic in Java programs, enabling dynamic and responsive behavior based on different inputs or conditions.
