## **Collection Interface in Java**
The **Collection** interface in Java is the root interface of the Java Collections Framework (JCF) and is part of the `java.util` package. It provides a general framework for working with groups of objects, such as **lists, sets, and queues**.

### **Hierarchy of Collection Interface**
```
Collection (Interface)
    ├── List (Interface) → [ArrayList, LinkedList, Vector, Stack]
    ├── Set (Interface) → [HashSet, LinkedHashSet, TreeSet]
    ├── Queue (Interface) → [PriorityQueue, Deque (ArrayDeque, LinkedList)]
```
> **Note:** `Map` (HashMap, TreeMap, etc.) is **not** a child of `Collection` because it deals with key-value pairs.

---

## **Methods in Collection Interface**
The **Collection** interface defines a set of methods that are inherited and implemented by all its child interfaces (List, Set, and Queue). Here are the key methods:

### **1. Basic Operations**
| Method | Description |
|--------|------------|
| `boolean add(E e)` | Adds an element to the collection |
| `boolean addAll(Collection<? extends E> c)` | Adds all elements from another collection |
| `void clear()` | Removes all elements from the collection |
| `boolean contains(Object o)` | Checks if the collection contains a specific element |
| `boolean containsAll(Collection<?> c)` | Checks if all elements exist in the collection |
| `boolean isEmpty()` | Returns `true` if the collection is empty |
| `int size()` | Returns the number of elements in the collection |
| `boolean remove(Object o)` | Removes a specific element |
| `boolean removeAll(Collection<?> c)` | Removes all elements present in another collection |
| `boolean retainAll(Collection<?> c)` | Retains only the elements that exist in another collection |

---

### **2. Iteration Methods**
| Method | Description |
|--------|------------|
| `Iterator<E> iterator()` | Returns an iterator for the collection |
| `Spliterator<E> spliterator()` | Returns a spliterator for parallel processing |
| `void forEach(Consumer<? super E> action)` | Iterates over elements using a lambda expression |

---

### **3. Array Conversion**
| Method | Description |
|--------|------------|
| `Object[] toArray()` | Converts the collection into an Object array |
| `<T> T[] toArray(T[] a)` | Converts the collection into a typed array |

---

## **Child Interfaces and Implemented Methods**
The `Collection` interface is implemented by **List, Set, and Queue**, which provide additional specialized methods.

### **1. `List` Interface (Ordered Collection)**
- Implementations: `ArrayList`, `LinkedList`, `Vector`, `Stack`
- Unique methods:
  - `void add(int index, E element)`
  - `E get(int index)`
  - `E remove(int index)`
  - `E set(int index, E element)`
  - `int indexOf(Object o)`
  - `int lastIndexOf(Object o)`
  - `ListIterator<E> listIterator()`

---

### **2. `Set` Interface (No Duplicates)**
- Implementations: `HashSet`, `LinkedHashSet`, `TreeSet`
- Unique properties:
  - No additional methods (inherits from `Collection`)
  - Does **not** allow duplicate elements

---

### **3. `Queue` Interface (FIFO)**
- Implementations: `PriorityQueue`, `ArrayDeque`
- Unique methods:
  - `boolean offer(E e)` – Adds an element (returns `false` if queue is full)
  - `E poll()` – Retrieves and removes the head (returns `null` if empty)
  - `E peek()` – Retrieves the head without removing (returns `null` if empty) 

---

## **Example Usage**
### **List Example**
```java
import java.util.*;

public class ListExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");

        System.out.println("List: " + list); // Output: [Apple, Banana, Cherry]
    }
}
```

### **Set Example**
```java
import java.util.*;

public class SetExample {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        set.add("Apple");
        set.add("Banana");
        set.add("Apple");  // Duplicate ignored

        System.out.println("Set: " + set); // Output: [Apple, Banana]
    }
}
```

### **Queue Example**
```java
import java.util.*;

public class QueueExample {
    public static void main(String[] args) {
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(10);
        queue.offer(20);
        queue.offer(30);

        System.out.println("Queue: " + queue);
        System.out.println("Poll: " + queue.poll()); // Removes 10
        System.out.println("Peek: " + queue.peek()); // Shows 20
    }
}
```

---

## **Summary**
- `Collection` is the **base interface** for `List`, `Set`, and `Queue`.
- It provides **core methods** like `add()`, `remove()`, `contains()`, and `size()`.
- `List` allows **ordered elements** with duplicates.
- `Set` allows **unique elements** with no ordering guarantees.
- `Queue` follows **FIFO** for processing elements.


