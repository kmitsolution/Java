### **📌 Understanding `System.out`, `System.in`, and `Scanner` in Java I/O Streams**  

In Java, **`System.out`**, **`System.in`**, and **`Scanner`** are fundamental for handling **input and output streams**. Let's break them down clearly.  

---

## **1️⃣ What is `System.out`?**  
🔹 **`System.out` is an instance of `PrintStream`**, which is used to output data to the console (**stdout**).  
🔹 It is a **byte stream** (not character-based), but it can print characters, numbers, and objects using its built-in methods.  
🔹 It is connected to the **console (monitor)** by default.  

### **Common Methods of `System.out`**
| Method | Description |
|--------|--------------|
| `print()` | Prints data without a newline |
| `println()` | Prints data with a newline |
| `printf()` | Formats and prints data |

### **Example: Using `System.out`**
```java
public class SystemOutExample {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");  // Prints with newline
        System.out.print("This is ");       // Prints without newline
        System.out.println("System.out");
        System.out.printf("The value of PI: %.2f%n", Math.PI);
    }
}
```

---

## **2️⃣ What is `System.in`?**  
🔹 **`System.in` is an instance of `InputStream`**, which is used to take input from the user (**stdin**).  
🔹 It reads **raw bytes** from the keyboard, which is why we often wrap it with `Scanner` or `BufferedReader`.  

### **Example: Reading Bytes from `System.in` (Not Recommended)**
```java
import java.io.IOException;

public class SystemInExample {
    public static void main(String[] args) throws IOException {
        System.out.println("Enter a character:");
        int data = System.in.read();  // Reads a single byte (ASCII value)
        System.out.println("You entered: " + (char) data);
    }
}
```
💡 **Limitation**: It reads only one byte at a time and does not handle full words or lines efficiently.  

---

## **3️⃣ Scanner Class (`java.util.Scanner`)**  
🔹 **`Scanner` is a wrapper around `System.in`** that makes reading user input **easier and more efficient**.  
🔹 It can read **integers, floating-point numbers, strings, and even full lines**.  
🔹 It **converts raw byte input into meaningful data types** automatically.  

### **🛠 Common Scanner Methods**
| Method | Description |
|--------|--------------|
| `nextInt()` | Reads an integer |
| `nextDouble()` | Reads a double value |
| `next()` | Reads a single word (ignores spaces) |
| `nextLine()` | Reads the entire line |
| `hasNextInt()` | Checks if next input is an integer |

### **Example: Using `Scanner` to Read Input**
```java
import java.util.Scanner;

public class ScannerExample {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = sc.nextLine(); // Reads full line

        System.out.print("Enter your age: ");
        int age = sc.nextInt(); // Reads an integer

        System.out.print("Enter your GPA: ");
        double gpa = sc.nextDouble(); // Reads a double value

        System.out.println("Hello " + name + ", you are " + age + " years old with a GPA of " + gpa);

        sc.close(); // Always close the scanner to prevent memory leaks
    }
}
```
💡 **`nextLine()` vs. `next()` Issue**:  
- `nextLine()` reads **entire lines** including spaces.  
- `next()` reads **only one word** (stops at spaces).  

---

## **4️⃣ Difference Between `System.in`, `System.out`, and `Scanner`**
| Feature | `System.out` | `System.in` | `Scanner` |
|---------|-------------|-------------|-----------|
| **Type** | Output Stream (`PrintStream`) | Input Stream (`InputStream`) | Wrapper around `System.in` |
| **Purpose** | Prints data to console | Reads raw bytes from keyboard | Reads formatted input (int, double, String, etc.) |
| **Data Handling** | Text (Characters) | Bytes (Raw Data) | Structured (Numbers, Words, Lines) |
| **Usage** | `System.out.println("Hello");` | `System.in.read();` | `Scanner sc = new Scanner(System.in);` |

---

## **5️⃣ Summary & Best Practices**
✔ Use **`System.out`** for output printing (`println`, `print`, `printf`).  
✔ Avoid using **`System.in.read()`** directly as it reads only one byte.  
✔ Use **`Scanner`** for user input (handles numbers, words, lines efficiently).  
✔ Always **close `Scanner`** after use (`sc.close()`).  

---

Would you like a **comparison with `BufferedReader` or file handling next?** 🚀
