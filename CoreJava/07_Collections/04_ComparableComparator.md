### **`Comparable` and `Comparator` Interfaces in Java**

In Java, **`Comparable`** and **`Comparator`** are two interfaces used to define how objects should be compared to each other, typically for sorting purposes.

### **1. `Comparable` Interface:**

The `Comparable` interface is used to define the natural ordering of objects. A class that implements `Comparable` has to override the `compareTo()` method, which allows the class instances to be compared with each other.

#### **`compareTo()` Method:**
```java
int compareTo(T o);
```
- It returns a negative value if the current object is less than the specified object.
- It returns zero if the current object is equal to the specified object.
- It returns a positive value if the current object is greater than the specified object.

### **When to use `Comparable`:**
- When you want to define a natural order for a class.
- This order will be used by default in sorting operations.

---

### **2. `Comparator` Interface:**

The `Comparator` interface allows you to define multiple custom sorting orders for a class. Unlike `Comparable`, which defines a **single natural ordering**, `Comparator` can be used to define various ways to compare objects.

#### **`compare()` Method:**
```java
int compare(T o1, T o2);
```
- It returns a negative value if `o1` is less than `o2`.
- It returns zero if `o1` is equal to `o2`.
- It returns a positive value if `o1` is greater than `o2`.

### **When to use `Comparator`:**
- When you need multiple ways to sort objects of a class.
- It allows sorting based on different fields or properties of the object.

---

### **Example: `Student` Class with Both `Comparable` and `Comparator`**

Let's create a `Student` class with fields like `adm_id`, `name`, `city`, and `marks`. We will demonstrate sorting using both **`Comparable`** (natural order) and **`Comparator`** (custom sorting).

#### **Step 1: `Student` Class Implementation**
```java
import java.util.*;

class Student implements Comparable<Student> {
    private int adm_id;
    private String name;
    private String city;
    private int marks;

    // Constructor
    public Student(int adm_id, String name, String city, int marks) {
        this.adm_id = adm_id;
        this.name = name;
        this.city = city;
        this.marks = marks;
    }

    // Getter methods
    public int getAdm_id() {
        return adm_id;
    }

    public String getName() {
        return name;
    }

    public String getCity() {
        return city;
    }

    public int getMarks() {
        return marks;
    }

    // Implementing Comparable: Sorting by adm_id (natural ordering)
    @Override
    public int compareTo(Student other) {
        return Integer.compare(this.adm_id, other.adm_id); // Compare by adm_id
    }

    @Override
    public String toString() {
        return "Student{adm_id=" + adm_id + ", name='" + name + "', city='" + city + "', marks=" + marks + "}";
    }
}
```

#### **Step 2: Comparator for Custom Sorting**
Now, let's implement some **custom comparators** using the `Comparator` interface. For instance, we can sort students by `name`, `marks`, or `city`.

```java
class NameComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.getName().compareTo(s2.getName()); // Compare by name
    }
}

class MarksComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return Integer.compare(s1.getMarks(), s2.getMarks()); // Compare by marks
    }
}

class CityComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.getCity().compareTo(s2.getCity()); // Compare by city
    }
}
```

#### **Step 3: Sorting with Collections**
Let's now use both `Comparable` and `Comparator` to sort a list of students.

```java
public class StudentSortExample {
    public static void main(String[] args) {
        // Create a list of students
        List<Student> students = new ArrayList<>();
        students.add(new Student(101, "John", "New York", 85));
        students.add(new Student(102, "Alice", "Los Angeles", 90));
        students.add(new Student(103, "Bob", "Chicago", 75));
        students.add(new Student(104, "Charlie", "Miami", 95));

        // Sort using Comparable (by adm_id)
        System.out.println("Sorting by Admission ID (Natural Order):");
        Collections.sort(students);  // Uses compareTo() method
        for (Student student : students) {
            System.out.println(student);
        }

        // Sort using Comparator (by name)
        System.out.println("\nSorting by Name:");
        students.sort(new NameComparator());
        for (Student student : students) {
            System.out.println(student);
        }

        // Sort using Comparator (by marks)
        System.out.println("\nSorting by Marks:");
        students.sort(new MarksComparator());
        for (Student student : students) {
            System.out.println(student);
        }

        // Sort using Comparator (by city)
        System.out.println("\nSorting by City:");
        students.sort(new CityComparator());
        for (Student student : students) {
            System.out.println(student);
        }
    }
}
```

#### **Output:**

```
Sorting by Admission ID (Natural Order):
Student{adm_id=101, name='John', city='New York', marks=85}
Student{adm_id=102, name='Alice', city='Los Angeles', marks=90}
Student{adm_id=103, name='Bob', city='Chicago', marks=75}
Student{adm_id=104, name='Charlie', city='Miami', marks=95}

Sorting by Name:
Student{adm_id=102, name='Alice', city='Los Angeles', marks=90}
Student{adm_id=103, name='Bob', city='Chicago', marks=75}
Student{adm_id=104, name='Charlie', city='Miami', marks=95}
Student{adm_id=101, name='John', city='New York', marks=85}

Sorting by Marks:
Student{adm_id=103, name='Bob', city='Chicago', marks=75}
Student{adm_id=101, name='John', city='New York', marks=85}
Student{adm_id=102, name='Alice', city='Los Angeles', marks=90}
Student{adm_id=104, name='Charlie', city='Miami', marks=95}

Sorting by City:
Student{adm_id=103, name='Bob', city='Chicago', marks=75}
Student{adm_id=102, name='Alice', city='Los Angeles', marks=90}
Student{adm_id=104, name='Charlie', city='Miami', marks=95}
Student{adm_id=101, name='John', city='New York', marks=85}
```

### **Summary of Usage:**

1. **`Comparable`**:
   - Use `Comparable` when you want to define a natural order for your objects. For example, we sorted students by their `adm_id` because it's their unique identifier.
   - The **natural ordering** is defined in the `compareTo()` method.

2. **`Comparator`**:
   - Use `Comparator` when you want **multiple ways** to compare or sort objects.
   - We created several custom comparators to sort students by **name**, **marks**, and **city**.
   - `Comparator` is especially useful when you want different sorting logic for the same class.

3. **`Collections.sort()`** and **`List.sort()`**:  
   - These methods rely on either `Comparable` (natural order) or `Comparator` (custom order) to sort the collection.

### **When to Use Each:**
- Use **`Comparable`** if there is only **one default sorting order** for the objects (e.g., by `adm_id`).
- Use **`Comparator`** when you need **multiple sorting orders** (e.g., sorting by `name`, `marks`, or `city`).

Let's dive deeper into **advanced examples** using the `Comparable` and `Comparator` interfaces. In these examples, we'll cover:

1. **Chaining Comparators** (multiple criteria).
2. **Using `Comparator` with Collections in Java** (like `TreeSet`, `TreeMap`).
3. **Sorting with Lambdas** (using Java 8+ `Comparator` API).
4. **Sorting with Reverse Order**.

### **1. Chaining Comparators** (Multiple Sorting Criteria)

In this example, we'll sort students first by **marks**, and if marks are the same, by **name**.

#### **Step 1: Define the `Student` Class**
```java
import java.util.*;

class Student implements Comparable<Student> {
    private int adm_id;
    private String name;
    private String city;
    private int marks;

    public Student(int adm_id, String name, String city, int marks) {
        this.adm_id = adm_id;
        this.name = name;
        this.city = city;
        this.marks = marks;
    }

    // Getters for student properties
    public int getAdm_id() { return adm_id; }
    public String getName() { return name; }
    public String getCity() { return city; }
    public int getMarks() { return marks; }

    @Override
    public int compareTo(Student other) {
        return Integer.compare(this.adm_id, other.adm_id); // Sort by adm_id by default
    }

    @Override
    public String toString() {
        return "Student{adm_id=" + adm_id + ", name='" + name + "', city='" + city + "', marks=" + marks + "}";
    }
}

class MarksAndNameComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        // First compare by marks
        int marksCompare = Integer.compare(s2.getMarks(), s1.getMarks()); // Descending order
        if (marksCompare != 0) {
            return marksCompare;
        }
        // If marks are equal, compare by name (alphabetical order)
        return s1.getName().compareTo(s2.getName());
    }
}
```

#### **Step 2: Sorting Using the Chained `Comparator`**
```java
public class AdvancedComparatorExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student(101, "John", "New York", 85));
        students.add(new Student(102, "Alice", "Los Angeles", 90));
        students.add(new Student(103, "Bob", "Chicago", 90));
        students.add(new Student(104, "Charlie", "Miami", 85));

        // Sorting students by Marks (Descending), and by Name (Ascending) if marks are the same
        students.sort(new MarksAndNameComparator());

        // Print sorted students
        System.out.println("Sorted Students by Marks and Name:");
        for (Student student : students) {
            System.out.println(student);
        }
    }
}
```

#### **Output:**
```
Sorted Students by Marks and Name:
Student{adm_id=102, name='Alice', city='Los Angeles', marks=90}
Student{adm_id=103, name='Bob', city='Chicago', marks=90}
Student{adm_id=101, name='John', city='New York', marks=85}
Student{adm_id=104, name='Charlie', city='Miami', marks=85}
```

In this case, students are first sorted by **marks** in **descending order**, and if two students have the same marks, they are then sorted by **name** in **ascending order**.

---

### **2. Using `Comparator` with `TreeSet` and `TreeMap`**

#### **`TreeSet` Example**:
A **`TreeSet`** is a collection that stores elements in **sorted order**. It uses a comparator (or the **natural ordering** of objects if the comparator is not provided) to sort the elements.

```java
import java.util.*;

public class TreeSetExample {
    public static void main(String[] args) {
        Set<Student> studentSet = new TreeSet<>(new MarksAndNameComparator()); // Using custom comparator
        studentSet.add(new Student(101, "John", "New York", 85));
        studentSet.add(new Student(102, "Alice", "Los Angeles", 90));
        studentSet.add(new Student(103, "Bob", "Chicago", 90));
        studentSet.add(new Student(104, "Charlie", "Miami", 85));

        System.out.println("Students in TreeSet (Sorted by Marks and Name):");
        for (Student student : studentSet) {
            System.out.println(student);
        }
    }
}
```

#### **Output:**
```
Students in TreeSet (Sorted by Marks and Name):
Student{adm_id=102, name='Alice', city='Los Angeles', marks=90}
Student{adm_id=103, name='Bob', city='Chicago', marks=90}
Student{adm_id=101, name='John', city='New York', marks=85}
Student{adm_id=104, name='Charlie', city='Miami', marks=85}
```

In this example, we used the custom **`MarksAndNameComparator`** to sort the `Student` objects in the `TreeSet` based on **marks** and **name**.

---

#### **`TreeMap` Example**:
A **`TreeMap`** is a map that stores **key-value pairs** in a sorted order. You can use `Comparator` to control the ordering of keys in the map.

```java
import java.util.*;

public class TreeMapExample {
    public static void main(String[] args) {
        Map<Student, String> studentMap = new TreeMap<>(new MarksAndNameComparator());

        studentMap.put(new Student(101, "John", "New York", 85), "Student 1");
        studentMap.put(new Student(102, "Alice", "Los Angeles", 90), "Student 2");
        studentMap.put(new Student(103, "Bob", "Chicago", 90), "Student 3");
        studentMap.put(new Student(104, "Charlie", "Miami", 85), "Student 4");

        System.out.println("TreeMap (Sorted by Marks and Name):");
        for (Map.Entry<Student, String> entry : studentMap.entrySet()) {
            System.out.println(entry.getKey() + " => " + entry.getValue());
        }
    }
}
```

#### **Output:**
```
TreeMap (Sorted by Marks and Name):
Student{adm_id=102, name='Alice', city='Los Angeles', marks=90} => Student 2
Student{adm_id=103, name='Bob', city='Chicago', marks=90} => Student 3
Student{adm_id=101, name='John', city='New York', marks=85} => Student 1
Student{adm_id=104, name='Charlie', city='Miami', marks=85} => Student 4
```

In this example, **`TreeMap`** sorts the entries based on the **keys** (the `Student` objects) using the **custom comparator** `MarksAndNameComparator`.

---

### **3. Sorting with Lambdas (Java 8+)**

Java 8 introduced **lambda expressions**, which allow you to pass concise `Comparator` logic directly without the need to create separate comparator classes. This is especially useful when you want to sort collections by different properties.

```java
public class LambdaComparatorExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student(101, "John", "New York", 85));
        students.add(new Student(102, "Alice", "Los Angeles", 90));
        students.add(new Student(103, "Bob", "Chicago", 90));
        students.add(new Student(104, "Charlie", "Miami", 85));

        // Sorting by marks (descending) and name (ascending)
        students.sort((s1, s2) -> {
            int marksCompare = Integer.compare(s2.getMarks(), s1.getMarks()); // descending order
            if (marksCompare != 0) return marksCompare;
            return s1.getName().compareTo(s2.getName()); // ascending order by name
        });

        System.out.println("Sorted Students by Marks and Name (Lambda):");
        students.forEach(System.out::println);
    }
}
```

#### **Output:**
```
Sorted Students by Marks and Name (Lambda):
Student{adm_id=102, name='Alice', city='Los Angeles', marks=90}
Student{adm_id=103, name='Bob', city='Chicago', marks=90}
Student{adm_id=101, name='John', city='New York', marks=85}
Student{adm_id=104, name='Charlie', city='Miami', marks=85}
```

In this example, we used a **lambda expression** to directly pass sorting logic. This approach is concise and eliminates the need to write separate comparator classes.

---

### **4. Sorting in Reverse Order**

If you want to sort a collection in reverse order, you can use **`Comparator.reverseOrder()`** or **`Comparator.reversed()`**.

```java
public class ReverseOrderExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student(101, "John", "New York", 85));
        students.add(new Student(102, "Alice", "Los Angeles", 90));
        students.add(new Student(103, "Bob", "Chicago", 75));
        students.add(new Student(104, "Charlie", "Miami", 95));

        // Sorting in reverse order based on marks
        students.sort(Comparator.comparingInt(Student::getMarks).reversed());

        System.out.println("Students sorted in reverse order by Marks:");
        students.forEach(System.out::println);
    }
}
```

#### **Output:**
```
Students sorted in reverse order by Marks:
Student{adm_id=104, name='Charlie', city='Miami', marks=95}
Student{adm_id=102, name='Alice', city='Los Angeles', marks=90}
Student{adm_id=101, name='John', city='New York', marks=85}
Student{adm_id=103, name='Bob', city='Chicago', marks=75}
```

This sorts the students in **descending order** based on their marks using the `reversed()` method of `Comparator`.

---

### **Summary of Advanced Concepts:**

1. **Chaining Comparators**: Sort by multiple criteria (e.g., marks first, then name if marks are equal).
2. **`TreeSet` and `TreeMap`**: Use custom comparators to maintain sorted order in sets and maps.
3. **Sorting with Lambdas**: Use Java 8 lambda expressions to define sorting logic concisely.
4. **Reverse Sorting**: Easily reverse the order using `Comparator.reversed()`.

These advanced techniques give you a lot of flexibility when sorting complex objects. You can create **customized sorting logic** tailored to your specific needs. 
