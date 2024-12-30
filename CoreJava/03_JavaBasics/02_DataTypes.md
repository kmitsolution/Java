### Data Types in Java

Java provides a rich set of **data types** that are used to store values in variables. These data types are categorized into two main types:

1. **Primitive Data Types**: These are the most basic data types in Java, defined by the language and used to store simple values.
2. **Reference Data Types**: These are objects and arrays, which refer to the memory location where the actual data is stored.

### **1. Primitive Data Types**

Primitive data types are predefined by Java and represent the simplest forms of data. They are **not objects** and are stored directly in memory. There are **8 primitive data types** in Java.

#### 1.1 **byte**
- **Size**: 1 byte (8 bits)
- **Range**: -128 to 127
- **Default Value**: 0
- **Description**: Used for saving memory in large arrays, or when working with raw binary data or I/O operations.

**Example:**
```java
byte a = 100;
byte b = -50;
System.out.println(a + b);  // Output: 50
```

#### 1.2 **short**
- **Size**: 2 bytes (16 bits)
- **Range**: -32,768 to 32,767
- **Default Value**: 0
- **Description**: Used when you need a smaller range than `int` but don't want to use a `byte`.

**Example:**
```java
short x = 32000;
short y = -15000;
System.out.println(x + y);  // Output: 17000
```

#### 1.3 **int**
- **Size**: 4 bytes (32 bits)
- **Range**: -2^31 to 2^31 - 1 (i.e., -2,147,483,648 to 2,147,483,647)
- **Default Value**: 0
- **Description**: The most commonly used integer data type for general-purpose numbers. It has a large range of values.

**Example:**
```java
int num1 = 100;
int num2 = 50;
System.out.println(num1 + num2);  // Output: 150
```

#### 1.4 **long**
- **Size**: 8 bytes (64 bits)
- **Range**: -2^63 to 2^63 - 1 (i.e., -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807)
- **Default Value**: 0L
- **Description**: Used when a larger range than `int` is needed. Often used in time calculations (e.g., milliseconds since epoch).

**Example:**
```java
long largeNumber = 10000000000L;  // 'L' denotes a long literal
System.out.println(largeNumber);  // Output: 10000000000
```

#### 1.5 **float**
- **Size**: 4 bytes (32 bits)
- **Range**: Approx. ±3.40282347E+38F (6-7 decimal digits)
- **Default Value**: 0.0f
- **Description**: Used for decimal values (single-precision floating point). Requires `f` at the end of the number to indicate it's a `float`.

**Example:**
```java
float pi = 3.14f;  // 'f' denotes a float literal
System.out.println(pi);  // Output: 3.14
```

#### 1.6 **double**
- **Size**: 8 bytes (64 bits)
- **Range**: Approx. ±1.79769313486231570E+308 (15 decimal digits)
- **Default Value**: 0.0d
- **Description**: Used for decimal values (double-precision floating point). This is the default data type for decimals in Java.

**Example:**
```java
double pi = 3.141592653589793;
System.out.println(pi);  // Output: 3.141592653589793
```

#### 1.7 **char**
- **Size**: 2 bytes (16 bits)
- **Range**: 0 to 65,535 (Unicode characters)
- **Default Value**: '\u0000' (null character)
- **Description**: Used to store a single character. Java uses Unicode characters, so `char` can represent any character in almost any language.

**Example:**
```java
char letter = 'A';
System.out.println(letter);  // Output: A
```

#### 1.8 **boolean**
- **Size**: 1 bit (but typically represented as 1 byte in memory)
- **Range**: `true` or `false`
- **Default Value**: `false`
- **Description**: Represents truth values (`true` or `false`). Used for conditions and logic.

**Example:**
```java
boolean isJavaFun = true;
boolean isLearningEasy = false;
System.out.println(isJavaFun);  // Output: true
```

---

### **2. Reference Data Types**

Reference data types are used to store references to objects or arrays, rather than the data itself. They are **objects** created from classes.

#### 2.1 **Objects**
- Any instance of a class in Java is considered a reference type. For example, if you create an instance of a class like `String`, `ArrayList`, or any custom class, it is an object.

**Example:**
```java
String message = "Hello, World!";
System.out.println(message);  // Output: Hello, World!
```

#### 2.2 **Arrays**
- An array is a reference type that holds multiple values of the same type. The reference type is used to store the memory address of the array object.

**Example:**
```java
int[] numbers = {1, 2, 3, 4, 5};
System.out.println(numbers[2]);  // Output: 3
```

---

### **Comparison Between Primitive and Reference Types**

| **Feature**         | **Primitive Data Types**                           | **Reference Data Types**                            |
|---------------------|-----------------------------------------------------|-----------------------------------------------------|
| **Memory Allocation** | Stored directly in memory (stack)                   | Stored as references (memory location) in heap      |
| **Default Value**     | Has default values (e.g., `0`, `false`, `null`)     | Default is `null` for object references and arrays   |
| **Size**             | Fixed size (e.g., `int` is 4 bytes)                | Varies based on the object or array size            |
| **Examples**         | `int`, `char`, `float`, `boolean`, `long`, etc.     | Objects, Arrays, `String`, `Scanner`, `ArrayList`, etc. |
| **Usage**            | Used for simple values (numbers, characters, logic) | Used for complex objects and data structures        |

---

### **Type Casting in Java**

- **Implicit Casting (Widening):** Automatically done when converting a smaller type to a larger type.
    ```java
    int x = 10;
    double y = x;  // Implicit casting from int to double
    System.out.println(y);  // Output: 10.0
    ```

- **Explicit Casting (Narrowing):** Required when converting a larger type to a smaller type.
    ```java
    double x = 10.5;
    int y = (int) x;  // Explicit casting from double to int
    System.out.println(y);  // Output: 10
    ```

---

### **Summary Table:**

| **Data Type** | **Size** | **Range**                                      | **Default Value** |
|---------------|----------|------------------------------------------------|-------------------|
| `byte`        | 1 byte   | -128 to 127                                    | 0                 |
| `short`       | 2 bytes  | -32,768 to 32,767                              | 0                 |
| `int`         | 4 bytes  | -2^31 to 2^31 - 1                              | 0                 |
| `long`        | 8 bytes  | -2^63 to 2^63 - 1                              | 0L                |
| `float`       | 4 bytes  | ±3.40282347E+38F (6-7 decimal digits)          | 0.0f              |
| `double`      | 8 bytes  | ±1.79769313486231570E+308 (15 decimal digits)  | 0.0d              |
| `char`        | 2 bytes  | 0 to 65,535 (Unicode characters)               | '\u0000'          |
| `boolean`     | 1 byte   | `true` or `false`                              | false             |

#### **Key Takeaways:**
- **Primitive data types** are faster and more memory-efficient for simple data storage.
- **Reference data types** are more flexible, capable of holding complex data structures, and support methods and properties.

