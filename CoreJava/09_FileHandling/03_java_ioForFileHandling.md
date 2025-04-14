`java.io` for **file handling** in Java

---

## 📁 **File Handling in Java using `java.io`**

The `java.io` package provides essential **classes for reading from and writing to files**. Here are some of the most commonly used ones:

---

### 📂 1. **`File` Class**
Used to **create**, **delete**, and get **info** about files/directories.

```java
import java.io.File;

public class FileExample {
    public static void main(String[] args) {
        File file = new File("example.txt");

        if (file.exists()) {
            System.out.println("File name: " + file.getName());
            System.out.println("Absolute path: " + file.getAbsolutePath());
            System.out.println("Writable: " + file.canWrite());
            System.out.println("Readable: " + file.canRead());
            System.out.println("File size: " + file.length());
        } else {
            System.out.println("The file does not exist.");
        }
    }
}
```

---

### 📝 2. **`FileWriter` and `BufferedWriter`**
Used to **write data to files**.

```java
import java.io.FileWriter;
import java.io.IOException;

public class WriteToFile {
    public static void main(String[] args) {
        try {
            FileWriter writer = new FileWriter("output.txt");
            writer.write("Hello, file handling in Java!");
            writer.close();
            System.out.println("Successfully wrote to the file.");
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }
    }
}
```

---

### 📖 3. **`FileReader` and `BufferedReader`**
Used to **read data from files**.

```java
import java.io.FileReader;
import java.io.BufferedReader;
import java.io.IOException;

public class ReadFromFile {
    public static void main(String[] args) {
        try {
            FileReader fr = new FileReader("output.txt");
            BufferedReader br = new BufferedReader(fr);

            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }

            br.close();
            fr.close();
        } catch (IOException e) {
            System.out.println("Error reading file.");
            e.printStackTrace();
        }
    }
}
```

---

### 🗑️ 4. **Delete a File**
```java
File myFile = new File("output.txt");
if (myFile.delete()) {
    System.out.println("Deleted the file: " + myFile.getName());
} else {
    System.out.println("Failed to delete the file.");
}
```

---

### ⚠️ Notes:
- Always close your file streams to avoid resource leaks.
- Use **try-with-resources** (Java 7+) for better file handling.
- For larger files or performance-sensitive apps, use **BufferedReader/Writer**.

---

