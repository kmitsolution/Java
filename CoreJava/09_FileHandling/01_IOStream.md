### **📌 What is a Stream in Java?**  
A **stream** in Java is a sequence of data that flows from a source to a destination. It is used to **read or write data** efficiently.  

✅ **Unidirectional Flow** → Data flows **in one direction** (Input or Output).  
✅ **Abstracts Data Handling** → Java hides complex file handling logic.  
✅ **Two Main Types** → **Byte Stream** (Binary Data) and **Character Stream** (Text Data).  

---

## **1️⃣ What is an I/O Stream?**  
I/O (**Input/Output**) Stream represents the flow of **data between Java programs and files, networks, or other sources**.  

### **🛠 Types of I/O Streams**
| Type | Description | Example |
|------|------------|---------|
| **Input Stream** | Reads data from a source (File, Keyboard, Network, etc.) | `FileInputStream` |
| **Output Stream** | Writes data to a destination (File, Console, Network, etc.) | `FileOutputStream` |

---

## **2️⃣ Byte Stream (Binary Data - Images, Videos, etc.)**  
Byte Streams handle **raw binary data** (e.g., images, PDFs, audio, videos). They use **8-bit bytes** to process data.  

✅ Used for **non-text files** (e.g., images, audio, video).  
✅ Uses **InputStream** and **OutputStream** classes.  

### **🛠 Byte Stream Classes**
| Class | Description |
|--------|--------------|
| `FileInputStream` | Reads byte data from a file |
| `FileOutputStream` | Writes byte data to a file |
| `BufferedInputStream` | Reads byte data with buffering (faster) |
| `BufferedOutputStream` | Writes byte data with buffering |
| `DataInputStream` | Reads primitive data types (int, double, etc.) |
| `DataOutputStream` | Writes primitive data types (int, double, etc.) |

### **🔍 Example: Reading a File Using `FileInputStream`**
```java
import java.io.FileInputStream;
import java.io.IOException;

public class ByteStreamExample {
    public static void main(String[] args) {
        try (FileInputStream fis = new FileInputStream("image.png")) {
            int data;
            while ((data = fis.read()) != -1) {
                System.out.print(data + " ");  // Prints byte values
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### **🔍 Example: Writing to a File Using `FileOutputStream`**
```java
import java.io.FileOutputStream;
import java.io.IOException;

public class ByteStreamWriteExample {
    public static void main(String[] args) {
        try (FileOutputStream fos = new FileOutputStream("output.dat")) {
            byte[] data = {65, 66, 67}; // Writes 'A', 'B', 'C'
            fos.write(data);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

## **3️⃣ Character Stream (Text Data - `.txt`, `.csv`)**  
Character Streams handle **text data**, processing characters using **16-bit Unicode**.

✅ Used for **text files (.txt, .csv, .json, .xml)**.  
✅ Uses **Reader** and **Writer** classes.  

### **🛠 Character Stream Classes**
| Class | Description |
|--------|--------------|
| `FileReader` | Reads character data from a file |
| `FileWriter` | Writes character data to a file |
| `BufferedReader` | Reads text data efficiently (line-by-line) |
| `BufferedWriter` | Writes text data efficiently (line-by-line) |

### **🔍 Example: Reading a File Using `FileReader`**
```java
import java.io.FileReader;
import java.io.IOException;

public class CharacterStreamExample {
    public static void main(String[] args) {
        try (FileReader fr = new FileReader("sample.txt")) {
            int ch;
            while ((ch = fr.read()) != -1) {
                System.out.print((char) ch);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### **🔍 Example: Writing to a File Using `FileWriter`**
```java
import java.io.FileWriter;
import java.io.IOException;

public class CharacterStreamWriteExample {
    public static void main(String[] args) {
        try (FileWriter fw = new FileWriter("output.txt")) {
            fw.write("Hello, Java File I/O!");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

## **4️⃣ Difference Between ByteStream and CharacterStream**
| Feature | Byte Stream | Character Stream |
|---------|------------|-----------------|
| **Data Type** | Handles **binary** data (0s & 1s) | Handles **text** data (characters) |
| **Class Hierarchy** | Uses `InputStream` & `OutputStream` | Uses `Reader` & `Writer` |
| **File Type** | Used for **images, videos, PDFs** | Used for **text-based files** |
| **Example Class** | `FileInputStream`, `FileOutputStream` | `FileReader`, `FileWriter` |
| **Encoding Support** | No encoding support (reads raw bytes) | Supports character encoding |

---

## **5️⃣ Summary**
✔ **Streams** help in reading/writing data efficiently.  
✔ **Byte Streams** handle binary data like images, videos, and PDFs.  
✔ **Character Streams** handle text-based data like `.txt`, `.csv`.  
✔ **Buffered Streams** improve performance.  

Would you like an example with **BufferedReader or file compression?** 🚀
