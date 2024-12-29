# Java First Program

Let's break down the process of writing a simple Java program, explaining the code, and showing how to compile and run it from the command line using `javac` and `java`. We'll also explain the use of the `public static void main(String[] args)` method.

### **Simple Java Program**

Here's a simple Java program:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### **Explanation of the Java Code**

1. **Class Declaration**:
   ```java
   public class HelloWorld {
   ```
   - This line declares a class named `HelloWorld`. 
   - In Java, every program must have a class, and the class name **must match the file name**. Since the class name is `HelloWorld`, the file must be saved as `HelloWorld.java` (case-sensitive).
   - The `public` keyword means that this class can be accessed by any other class in any package.

2. **The main Method**:
   ```java
   public static void main(String[] args) {
   ```
   - This is the entry point of every Java application. When you run a Java program, the `main` method is executed first.
   - **`public`**: The `main` method is public, meaning it can be accessed from outside the class.
   - **`static`**: The `main` method is static, which means it can be called without creating an instance (object) of the `HelloWorld` class.
   - **`void`**: The `main` method does not return any value. Therefore, it is declared as `void`.
   - **`String[] args`**: This is an array of `String` values that allows the user to pass command-line arguments when running the program. It's a way to input data to the program when you start it from the command line.

   **Why does `String[] args` (an argument of type `String[]`) exist?**
   - The `String[] args` allows the program to accept arguments when it is executed. These arguments are passed from the command line when you run the program.
   - For example, if you run the program as `java HelloWorld arg1 arg2`, then `args` will contain `["arg1", "arg2"]`. You can use these arguments in your program.
   - **Note**: The `main` method is required to accept a `String[] args` even if you're not using command-line arguments.

3. **Printing Output**:
   ```java
   System.out.println("Hello, World!");
   ```
   - This line outputs the text `Hello, World!` to the console. The `System.out.println()` method is used to print a message to the console followed by a newline.

4. **Closing the class**:
   ```java
   }
   ```

### **Saving the File**
- Save the file as `HelloWorld.java`. Remember, the filename must match the class name and have the `.java` extension.

### **Steps to Compile and Execute the Java Program Using Command Line**

#### Step 1: Open Command Line or Terminal
- **Windows**: Open **Command Prompt** (`cmd`) or **PowerShell**.
- **Linux/macOS**: Open the **Terminal**.

#### Step 2: Navigate to the Directory where the `.java` file is saved
Use the `cd` command to navigate to the folder where `HelloWorld.java` is saved. For example:

```bash
cd path/to/directory
```

#### Step 3: Compile the Java Program
To compile the Java program, use the `javac` command followed by the filename:

```bash
javac HelloWorld.java
```

- `javac` is the Java compiler that converts your `.java` source file into bytecode (a `.class` file that the JVM can execute).
- If there are no errors in your code, this will generate a file named `HelloWorld.class` in the same directory.

#### Step 4: Run the Java Program
To run the compiled Java program, use the `java` command followed by the class name (without the `.class` extension):

```bash
java HelloWorld
```

- The `java` command launches the Java Runtime Environment (JRE) and executes the bytecode contained in the `HelloWorld.class` file.
- You should see the output `Hello, World!` printed on the console.

### **Summary of Commands**

Here’s a summary of the steps on the command line:

1. **Navigate to the directory containing `HelloWorld.java`:**
   ```bash
   cd path/to/directory
   ```

2. **Compile the Java file using `javac`:**
   ```bash
   javac HelloWorld.java
   ```

3. **Run the compiled Java program using `java`:**
   ```bash
   java HelloWorld
   ```

### **Why Do We Need `String[] args` in the Main Method?**
- The argument `String[] args` in the `main` method is there to allow users to pass arguments to the program when executing it from the command line.
- Although you don't need to use this feature in a simple program like `HelloWorld`, it is crucial when writing more complex programs that might require inputs at runtime. For example, if you're creating a program that processes a file or performs calculations based on user input, `String[] args` can be used to pass the filename or parameters to the program.
  
**Example:**
If you modify the program to use command-line arguments, you can do something like this:

```java
public class HelloWorld {
    public static void main(String[] args) {
        if (args.length > 0) {
            System.out.println("Hello, " + args[0] + "!");
        } else {
            System.out.println("Hello, World!");
        }
    }
}
```

- If you run the program with a command like `java HelloWorld Alice`, the output will be `Hello, Alice!`.
- If you run it without any arguments, the output will be `Hello, World!`.

### **Conclusion**
- The `main` method in Java is the entry point of any Java application. It must always have the signature `public static void main(String[] args)`.
- `String[] args` allows the program to receive command-line arguments, which is useful for dynamic input.
- To execute a Java program, you must compile it using `javac` and then run it with `java`.
