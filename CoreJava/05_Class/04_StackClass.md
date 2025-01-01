### **Stack Class in Java**

A **stack** is a linear data structure that follows the **LIFO (Last In, First Out)** principle, meaning that the last element added to the stack is the first one to be removed. In this class, we’ll implement a stack with a maximum capacity of 10 elements. We will also create methods for pushing and popping elements.

Let's break down the class and implement it:

### **Code Implementation:**
```java
// This class defines an integer stack that can hold 10 values
class Stack {
    int stck[] = new int[10];  // Array to hold stack elements
    int tos;  // Variable to track top-of-stack (tos)

    // Initialize top-of-stack
    Stack() {
        tos = -1;  // Set tos to -1 when stack is empty
    }

    // Push an item onto the stack
    void push(int item) {
        if (tos == 9) {
            System.out.println("Stack is full.");
        } else {
            stck[++tos] = item;  // Increment tos and add item to stack
        }
    }

    // Pop an item from the stack
    int pop() {
        if (tos < 0) {
            System.out.println("Stack underflow.");
            return 0;  // Return 0 if stack is empty
        } else {
            return stck[tos--];  // Return the item and decrement tos
        }
    }

    // Check if the stack is empty
    boolean isEmpty() {
        return tos < 0;
    }

    // Display the stack content (from top to bottom)
    void display() {
        if (tos == -1) {
            System.out.println("Stack is empty.");
        } else {
            System.out.print("Stack elements: ");
            for (int i = tos; i >= 0; i--) {
                System.out.print(stck[i] + " ");
            }
            System.out.println();
        }
    }
}

public class Main {
    public static void main(String[] args) {
        // Create a stack object
        Stack stack = new Stack();

        // Push items onto the stack
        stack.push(10);
        stack.push(20);
        stack.push(30);
        stack.push(40);
        
        // Display stack content
        stack.display();  // Output: Stack elements: 40 30 20 10 

        // Pop items from the stack
        System.out.println("Popped item: " + stack.pop());  // Output: Popped item: 40
        System.out.println("Popped item: " + stack.pop());  // Output: Popped item: 30

        // Display stack content again
        stack.display();  // Output: Stack elements: 20 10
    }
}
```

### **Explanation of the Code:**

1. **Stack Class:**
    - `stck[]`: An array that holds the stack elements (maximum of 10 integers).
    - `tos`: The variable `tos` (top-of-stack) keeps track of the index of the topmost element in the stack.
    - **Constructor**: The constructor `Stack()` initializes `tos` to `-1`, indicating that the stack is empty.
    - **push() Method**: Adds an element to the stack. If the stack is full (`tos == 9`), it prints an error message.
    - **pop() Method**: Removes and returns the top element from the stack. If the stack is empty (`tos < 0`), it prints an error message.
    - **isEmpty() Method**: Checks if the stack is empty.
    - **display() Method**: Displays the stack elements from top to bottom. If the stack is empty, it prints "Stack is empty."

2. **Main Class:**
    - In the `main` method, a `Stack` object is created, and several operations are performed: pushing and popping elements, and displaying the stack.

### **Class Diagram for Stack:**

The class diagram below shows the structure of the `Stack` class, its fields, and its methods.

```
+---------------------+
|       Stack         |
+---------------------+
| - stck[]: int[10]   |
| - tos: int          |
+---------------------+
| + Stack()           |
| + push(item: int)   |
| + pop(): int        |
| + isEmpty(): boolean|
| + display(): void   |
+---------------------+
```

- **Fields**:
  - `stck[]`: Array of integers (maximum 10 elements) to store stack elements.
  - `tos`: An integer to track the top of the stack.
  
- **Methods**:
  - `Stack()`: Constructor to initialize the stack.
  - `push(item)`: Method to push an item onto the stack.
  - `pop()`: Method to pop an item from the stack.
  - `isEmpty()`: Checks if the stack is empty.
  - `display()`: Displays the contents of the stack.

### **Object Diagram for the Stack Class:**

Let's create an object diagram assuming we push and pop some values into/from the stack:

1. Initially, when the `stack` object is created, it has an empty stack:
```
+-------------------------+
| stack: Stack            |
+-------------------------+
| stck[]: [0, 0, 0, 0, 0, |
|        0, 0, 0, 0, 0]   |
| tos: -1                 |
+-------------------------+
```

2. After pushing `10`, `20`, `30`, and `40` onto the stack:
```
+-------------------------+
| stack: Stack            |
+-------------------------+
| stck[]: [10, 20, 30, 40, |
|        0, 0, 0, 0, 0]   |
| tos: 3                  |
+-------------------------+
```

3. After popping two elements (40 and 30):
```
+-------------------------+
| stack: Stack            |
+-------------------------+
| stck[]: [10, 20, 30, 40, |
|        0, 0, 0, 0, 0]   |
| tos: 1                  |
+-------------------------+
```

The stack now holds the elements `10` and `20`, and the top of the stack (`tos`) is at index `1`.

### **Conclusion:**
- This `Stack` class models a simple stack with basic operations like **push** and **pop**.
- The class supports the **LIFO** behavior of a stack.
- The `tos` variable keeps track of the top of the stack, and the stack can hold up to 10 elements.
- The `push` and `pop` methods modify the stack, and `display` provides a way to view the current state of the stack.
