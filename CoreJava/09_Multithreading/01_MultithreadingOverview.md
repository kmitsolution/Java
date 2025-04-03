### **What is Multithreading?**  

**Multithreading** is a feature in Java that allows multiple threads (smallest units of a process) to execute concurrently. It improves performance by utilizing CPU efficiently.  

### **Key Features of Multithreading in Java**  
- **Concurrent execution**: Multiple tasks run simultaneously.  
- **Resource sharing**: Threads share the same memory space.  
- **Faster execution**: Reduces CPU idle time.  
- **Independent tasks**: If one thread fails, others continue execution.  

---

### **Java Multithreading Example**  

#### **Example 1: Using the `Thread` Class**  
```java
class MyThread extends Thread {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + " - " + i);
            try {
                Thread.sleep(500); // Pause for 500 milliseconds
            } catch (InterruptedException e) {
                System.out.println(e);
            }
        }
    }

    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        
        t1.start(); // Start first thread
        t2.start(); // Start second thread
    }
}
```
### **Output (Order may vary due to concurrent execution)**
```
Thread-0 - 1
Thread-1 - 1
Thread-0 - 2
Thread-1 - 2
Thread-0 - 3
Thread-1 - 3
...
```
---

#### **Example 2: Using the `Runnable` Interface (Better Approach)**
```java
class MyRunnable implements Runnable {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + " - " + i);
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                System.out.println(e);
            }
        }
    }

    public static void main(String[] args) {
        Thread t1 = new Thread(new MyRunnable(), "Thread 1");
        Thread t2 = new Thread(new MyRunnable(), "Thread 2");
        
        t1.start();
        t2.start();
    }
}
```
### **Why Use `Runnable` Instead of `Thread`?**
- **Allows multiple inheritance** (since Java doesn't support multiple class inheritance).
- **More flexible** for real-world applications.

