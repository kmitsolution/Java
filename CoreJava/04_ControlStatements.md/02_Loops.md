### **Loops in Java**

Loops are fundamental control flow statements that allow a block of code to be executed repeatedly based on a condition. Java provides several types of loops: **`for` loop**, **`for-each` loop**, **`while` loop**, **`do-while` loop**. Additionally, Java also provides control statements like **`break`** and **`continue`** that can alter the flow of loops.

### **1. `for` Loop**
The `for` loop is used when the number of iterations is known beforehand. It consists of three parts: initialization, condition, and increment/decrement.

**Syntax**:
```java
for (initialization; condition; update) {
    // Code to be executed
}
```

- **Initialization**: Executed once at the beginning.
- **Condition**: Checked before every iteration. If true, the loop continues; if false, the loop terminates.
- **Update**: Executes after each iteration (typically used for incrementing/decrementing a variable).

**Example**:
```java
public class ForLoopExample {
    public static void main(String[] args) {
        // Print numbers from 1 to 5
        for (int i = 1; i <= 5; i++) {
            System.out.println(i);
        }
    }
}
```

**Output**:
```
1
2
3
4
5
```

---

### **2. `for-each` Loop (Enhanced `for` Loop)**
The `for-each` loop is a special type of `for` loop used for iterating over elements in an array or a collection like a list. It's a cleaner and more concise way to loop through elements, particularly when you don't need to know the index of the element.

**Syntax**:
```java
for (datatype var : array) {
    // Code to be executed
}
```

**Example**:
```java
public class ForEachLoopExample {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5};
        
        // Iterate through array using for-each loop
        for (int num : numbers) {
            System.out.println(num);
        }
    }
}
```

**Output**:
```
1
2
3
4
5
```

---

### **3. `while` Loop**
The `while` loop is used when the number of iterations is not known in advance and the condition is evaluated before the execution of the loop body.

**Syntax**:
```java
while (condition) {
    // Code to be executed
}
```

- The loop will execute as long as the **condition** is true.

**Example**:
```java
public class WhileLoopExample {
    public static void main(String[] args) {
        int i = 1;
        
        // Print numbers from 1 to 5
        while (i <= 5) {
            System.out.println(i);
            i++;  // Increment i
        }
    }
}
```

**Output**:
```
1
2
3
4
5
```

---

### **4. `do-while` Loop**
The `do-while` loop is similar to the `while` loop, but it guarantees at least one execution of the loop body because the condition is evaluated **after** the loop body is executed.

**Syntax**:
```java
do {
    // Code to be executed
} while (condition);
```

- The loop will execute the block of code once, and then check the condition.

**Example**:
```java
public class DoWhileLoopExample {
    public static void main(String[] args) {
        int i = 1;
        
        // Print numbers from 1 to 5
        do {
            System.out.println(i);
            i++;  // Increment i
        } while (i <= 5);
    }
}
```

**Output**:
```
1
2
3
4
5
```

---

### **5. `break` Statement**
The `break` statement is used to exit from the loop prematurely. It can be used in `for`, `while`, `do-while`, and `switch` statements to stop the execution of the loop.

**Example**:
```java
public class BreakExample {
    public static void main(String[] args) {
        for (int i = 1; i <= 10; i++) {
            if (i == 6) {
                break;  // Exit the loop when i is 6
            }
            System.out.println(i);
        }
    }
}
```

**Output**:
```
1
2
3
4
5
```

In this example, the loop terminates when `i` reaches 6 due to the `break` statement.

---

### **6. `continue` Statement**
The `continue` statement is used to skip the current iteration of a loop and move to the next iteration, without terminating the loop.

**Example**:
```java
public class ContinueExample {
    public static void main(String[] args) {
        for (int i = 1; i <= 5; i++) {
            if (i == 3) {
                continue;  // Skip the iteration when i is 3
            }
            System.out.println(i);
        }
    }
}
```

**Output**:
```
1
2
4
5
```

In this example, the number `3` is skipped because the `continue` statement is executed when `i` equals `3`, causing the loop to skip that iteration.

---

### **7. Labeled `break` and `continue` Statements**
Both `break` and `continue` can also be labeled in Java. This allows you to control the flow of nested loops.

- **Labeled `break`**: Exits from a specific outer loop.
- **Labeled `continue`**: Skips the current iteration of a specific outer loop.

**Syntax**:
```java
labelName: 
for (initialization; condition; update) {
    // loop code
    break labelName;  // Breaks out of the labeled loop
    continue labelName;  // Skips to next iteration of the labeled loop
}
```

**Example of Labeled `break`**:
```java
public class LabeledBreakExample {
    public static void main(String[] args) {
        outerLoop:
        for (int i = 1; i <= 3; i++) {
            for (int j = 1; j <= 3; j++) {
                if (i == 2 && j == 2) {
                    break outerLoop;  // Exit the outer loop
                }
                System.out.println("i = " + i + ", j = " + j);
            }
        }
    }
}
```

**Output**:
```
i = 1, j = 1
i = 1, j = 2
i = 1, j = 3
```

The outer loop terminates when `i == 2` and `j == 2` due to the labeled `break`.

**Example of Labeled `continue`**:
```java
public class LabeledContinueExample {
    public static void main(String[] args) {
        outerLoop:
        for (int i = 1; i <= 3; i++) {
            for (int j = 1; j <= 3; j++) {
                if (i == 2 && j == 2) {
                    continue outerLoop;  // Skip to the next iteration of the outer loop
                }
                System.out.println("i = " + i + ", j = " + j);
            }
        }
    }
}
```

**Output**:
```
i = 1, j = 1
i = 1, j = 2
i = 1, j = 3
i = 2, j = 1
i = 2, j = 3
i = 3, j = 1
i = 3, j = 2
i = 3, j = 3
```

In this example, when `i == 2` and `j == 2`, the inner loop is skipped, and the program jumps to the next iteration of the outer loop.

---

### **Conclusion**
- **`for` loop**: Used for a known number of iterations.
- **`for-each` loop**: Simplifies iteration over arrays or collections.
- **`while` loop**: Executes as long as the condition is true.
- **`do-while` loop**: Executes at least once before checking the condition.
- **`break`**: Terminates the loop early.
- **`continue`**: Skips the current iteration and continues with the next one.
- **Labeled `break` and `continue`**: Provide control over nested loops.

These looping and control statements are essential for iterating through collections, managing program flow, and performing repetitive tasks in Java.
