### **What is a Process in Java?**  

A **process** in Java is an independent program in execution. It has its own memory space, resources, and execution environment. Java processes are managed by the operating system and can run multiple threads within them.  

---

### **Key Characteristics of a Process in Java:**  
1. **Independent Execution** → Each process runs separately and does not share memory with other processes.  
2. **Resource Allocation** → Every process has its own memory space and system resources.  
3. **Inter-Process Communication (IPC)** → Processes communicate using IPC mechanisms like sockets, files, or shared memory.  
4. **Multiple Processes** → A Java program can create multiple processes using the `ProcessBuilder` or `Runtime` class.  

---

### **Example of Creating a Process in Java (Opening Notepad)**  
```java
import java.io.IOException;

public class ProcessExample {
    public static void main(String[] args) {
        try {
            // Creating a new process (Opening Notepad)
            Process process = Runtime.getRuntime().exec("notepad.exe");
            System.out.println("Process started: Notepad");

            // Waiting for the process to exit
            process.waitFor();
            System.out.println("Process exited.");
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
### **Explanation:**  
- `Runtime.getRuntime().exec("notepad.exe")` → Starts Notepad as a separate process.  
- `process.waitFor()` → Waits for the Notepad process to complete before proceeding.  

---

### **ProcessBuilder in Java - Explanation & Examples**  

`ProcessBuilder` is a Java class used to create and manage operating system processes. It provides **better control** over process execution compared to `Runtime.exec()`, allowing us to:  
✅ Modify environment variables  
✅ Redirect input/output streams  
✅ Start and control multiple processes  

---

## **1. Basic Example: Opening Calculator (`calc.exe`)**  
```java
import java.io.IOException;

public class ProcessBuilderExample {
    public static void main(String[] args) {
        try {
            // Create a ProcessBuilder to open Calculator
            ProcessBuilder processBuilder = new ProcessBuilder("calc.exe");
            Process process = processBuilder.start(); // Start the process
            
            System.out.println("Calculator started!");
            
            // Wait for the process to complete
            process.waitFor();
            System.out.println("Calculator closed.");
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
### **Explanation:**
- `ProcessBuilder("calc.exe")` → Creates a process to open Calculator.  
- `start()` → Launches the process.  
- `waitFor()` → Waits for the process to complete before continuing execution.  

---

## **2. Running a System Command (`ping google.com`) and Capturing Output**
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class ProcessBuilderOutputExample {
    public static void main(String[] args) {
        try {
            // Run system command: ping google.com
            ProcessBuilder processBuilder = new ProcessBuilder("ping", "google.com");
            Process process = processBuilder.start();
            
            // Capture process output
            BufferedReader reader = new BufferedReader(new InputStreamReader(process.getInputStream()));
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line); // Print output line by line
            }
            
            process.waitFor(); // Wait for process to complete
            System.out.println("Ping command executed.");
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
### **Explanation:**
- `ProcessBuilder("ping", "google.com")` → Runs the ping command.  
- `getInputStream()` → Captures and prints the output of the command.  
- `BufferedReader` → Reads and prints output line by line.  

---

## **3. Redirecting Process Output to a File**
```java
import java.io.File;
import java.io.IOException;

public class ProcessBuilderRedirectExample {
    public static void main(String[] args) {
        try {
            // Create a ProcessBuilder to list directory contents and redirect output to a file
            ProcessBuilder processBuilder = new ProcessBuilder("cmd.exe", "/c", "dir");
            
            // Redirect output to a file
            File outputFile = new File("output.txt");
            processBuilder.redirectOutput(outputFile);
            
            Process process = processBuilder.start();
            process.waitFor();
            System.out.println("Command executed. Check 'output.txt' for results.");
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
### **Explanation:**
- `redirectOutput(outputFile)` → Redirects command output to `output.txt`.  
- `cmd.exe /c dir` → Runs the `dir` command (lists directory contents).  

---

## **4. Setting Environment Variables for a Process**
```java
import java.io.IOException;
import java.util.Map;

public class ProcessBuilderEnvironmentExample {
    public static void main(String[] args) {
        try {
            ProcessBuilder processBuilder = new ProcessBuilder("cmd.exe", "/c", "echo %MY_ENV_VAR%");
            
            // Set an environment variable
            Map<String, String> environment = processBuilder.environment();
            environment.put("MY_ENV_VAR", "Hello from Java!");

            Process process = processBuilder.start();

            // Capture and print output
            new BufferedReader(new InputStreamReader(process.getInputStream()))
                    .lines().forEach(System.out::println);

            process.waitFor();
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
### **Explanation:**
- `processBuilder.environment().put("MY_ENV_VAR", "Hello from Java!")` → Sets an environment variable.  
- The command `echo %MY_ENV_VAR%` prints the environment variable value.  

---

### **Why Use `ProcessBuilder` Instead of `Runtime.exec()`?**
| Feature | `Runtime.exec()` | `ProcessBuilder` |
|---------|-----------------|------------------|
| **Flexibility** | Limited | More control over process execution |
| **I/O Handling** | Difficult | Can redirect input/output easily |
| **Environment Variables** | Hard to modify | Easily set using `.environment()` |
| **Command Arguments** | Requires manual formatting | Uses `List<String>` for arguments |

Would you like an advanced example, such as **running multiple processes in parallel**? 🚀
