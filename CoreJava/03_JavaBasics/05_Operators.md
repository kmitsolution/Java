### **Operators in Java**

In Java, **operators** are symbols or keywords used to perform operations on variables and values. Java operators are categorized into several types, each serving a specific purpose.

### **Types of Operators in Java**

1. **Arithmetic Operators**
2. **Relational Operators**
3. **Logical Operators**
4. **Bitwise Operators**
5. **Assignment Operators**
6. **Unary Operators**
7. **Ternary Operator**
8. **Instanceof Operator**

---

### **1. Arithmetic Operators**
Arithmetic operators are used to perform basic mathematical operations such as addition, subtraction, multiplication, division, and modulus.

**Operators**: `+`, `-`, `*`, `/`, `%`

**Example:**
```java
public class ArithmeticOperatorsExample {
    public static void main(String[] args) {
        int a = 10, b = 5;
        
        System.out.println("a + b = " + (a + b)); // 15
        System.out.println("a - b = " + (a - b)); // 5
        System.out.println("a * b = " + (a * b)); // 50
        System.out.println("a / b = " + (a / b)); // 2
        System.out.println("a % b = " + (a % b)); // 0 (remainder)
    }
}
```

**Output:**
```
a + b = 15
a - b = 5
a * b = 50
a / b = 2
a % b = 0
```

---

### **2. Relational Operators**
Relational operators are used to compare two values and determine the relationship between them, returning a boolean result (`true` or `false`).

**Operators**: `==`, `!=`, `>`, `<`, `>=`, `<=`

**Example:**
```java
public class RelationalOperatorsExample {
    public static void main(String[] args) {
        int a = 10, b = 5;
        
        System.out.println("a == b: " + (a == b)); // false
        System.out.println("a != b: " + (a != b)); // true
        System.out.println("a > b: " + (a > b));   // true
        System.out.println("a < b: " + (a < b));   // false
        System.out.println("a >= b: " + (a >= b)); // true
        System.out.println("a <= b: " + (a <= b)); // false
    }
}
```

**Output:**
```
a == b: false
a != b: true
a > b: true
a < b: false
a >= b: true
a <= b: false
```

---

### **3. Logical Operators**
Logical operators are used to combine multiple boolean expressions and return a boolean result.

**Operators**: `&&` (AND), `||` (OR), `!` (NOT)

**Example:**
```java
public class LogicalOperatorsExample {
    public static void main(String[] args) {
        boolean a = true, b = false;
        
        System.out.println("a && b: " + (a && b)); // false
        System.out.println("a || b: " + (a || b)); // true
        System.out.println("!a: " + !a);            // false
    }
}
```

**Output:**
```
a && b: false
a || b: true
!a: false
```

---

### **4. Bitwise Operators**
Bitwise operators are used to perform bit-level operations on integer values (binary digits).

**Operators**: `&` (AND), `|` (OR), `^` (XOR), `~` (NOT), `<<` (left shift), `>>` (right shift), `>>>` (unsigned right shift)

**Example:**
```java
public class BitwiseOperatorsExample {
    public static void main(String[] args) {
        int a = 5;  // 0101 in binary
        int b = 3;  // 0011 in binary
        
        System.out.println("a & b: " + (a & b)); // 1 (0001 in binary)
        System.out.println("a | b: " + (a | b)); // 7 (0111 in binary)
        System.out.println("a ^ b: " + (a ^ b)); // 6 (0110 in binary)
        System.out.println("~a: " + (~a));       // -6 (11111111111111111111111111111010 in binary)
        System.out.println("a << 1: " + (a << 1)); // 10 (1010 in binary)
        System.out.println("a >> 1: " + (a >> 1)); // 2 (0010 in binary)
    }
}
```

**Output:**
```
a & b: 1
a | b: 7
a ^ b: 6
~a: -6
a << 1: 10
a >> 1: 2
```

---

### **5. Assignment Operators**
Assignment operators are used to assign values to variables. The most common one is the `=` operator, but there are also shorthand operators for performing operations and assignment in one step.

**Operators**: `=`, `+=`, `-=`, `*=`, `/=`, `%=` (and more)

**Example:**
```java
public class AssignmentOperatorsExample {
    public static void main(String[] args) {
        int a = 10;
        
        a += 5; // a = a + 5 => 15
        System.out.println("a += 5: " + a);
        
        a -= 3; // a = a - 3 => 12
        System.out.println("a -= 3: " + a);
        
        a *= 2; // a = a * 2 => 24
        System.out.println("a *= 2: " + a);
        
        a /= 4; // a = a / 4 => 6
        System.out.println("a /= 4: " + a);
        
        a %= 3; // a = a % 3 => 0
        System.out.println("a %= 3: " + a);
    }
}
```

**Output:**
```
a += 5: 15
a -= 3: 12
a *= 2: 24
a /= 4: 6
a %= 3: 0
```

---

### **6. Unary Operators**
Unary operators are used to perform operations on a single operand.

**Operators**: `+`, `-`, `++`, `--`, `!`, `~`

**Example:**
```java
public class UnaryOperatorsExample {
    public static void main(String[] args) {
        int a = 10;
        System.out.println("++a: " + ++a);  // Pre-increment: a becomes 11, then printed
        System.out.println("a++: " + a++);  // Post-increment: prints 11, then a becomes 12
        System.out.println("--a: " + --a);  // Pre-decrement: a becomes 11, then printed
        System.out.println("a--: " + a--);  // Post-decrement: prints 11, then a becomes 10
        System.out.println("!true: " + !true); // NOT operator
    }
}
```

**Output:**
```
++a: 11
a++: 11
--a: 11
a--: 11
!true: false
```

---

### **7. Ternary Operator**
The ternary operator is a shorthand for `if-else` statement and is used to assign a value based on a condition.

**Syntax**:
```java
condition ? value_if_true : value_if_false
```

**Example:**
```java
public class TernaryOperatorExample {
    public static void main(String[] args) {
        int a = 10, b = 20;
        int max = (a > b) ? a : b;  // If a > b, max = a, otherwise max = b
        System.out.println("Maximum value is: " + max);
    }
}
```

**Output:**
```
Maximum value is: 20
```

---

### **8. Instanceof Operator**
The `instanceof` operator checks whether an object is an instance of a specific class or interface.

**Syntax**:
```java
object instanceof ClassName
```

**Example:**
```java
public class InstanceofExample {
    public static void main(String[] args) {
        String str = "Hello, World!";
        boolean result = str instanceof String;  // true because str is an instance of String
        System.out.println("Is str an instance of String? " + result);
    }
}
```

**Output:**
```
Is str an instance of String? true
```

---

### **Conclusion**

Operators in Java are a core part of programming and are used to manipulate data and variables. Understanding different types of operators—arithmetic, relational, logical, bitwise, assignment, unary, ternary, and instanceof—is crucial for writing effective Java code. These operators help perform basic mathematical calculations, compare values, combine boolean expressions, and more.
