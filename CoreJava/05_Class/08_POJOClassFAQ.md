### **FAQ: POJO (Plain Old Java Object) Class**  

#### **1. What is a POJO class in Java?**  
A **POJO (Plain Old Java Object)** is a simple Java class that follows standard object-oriented principles without any special restrictions or dependencies. It is primarily used to represent data.

#### **2. What are the characteristics of a POJO class?**  
A POJO class should:  
- Be **public** and have a **default (no-argument) constructor**.  
- Contain **private fields** (variables).  
- Provide **getter and setter methods** for accessing fields.  
- Not extend any **specific class** (other than `Object`).  
- Not implement any **specific interfaces** unless required for functionality.  
- Avoid using special annotations, except for serialization or ORM (optional).  

#### **3. How do you create a POJO class?**  
Example of a **POJO class**:
```java
public class Person {
    private String name;
    private int age;

    // Default Constructor
    public Person() {}

    // Parameterized Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getters and Setters
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

#### **4. What is the difference between a POJO and a JavaBean?**  
| Feature      | POJO | JavaBean |
|-------------|------|----------|
| Getter/Setter | Optional | Required |
| Default Constructor | Optional | Required |
| Serializable | Not required | Should implement `Serializable` |
| Special Annotations | Not required | Might use annotations in frameworks |
| Naming Convention | No strict convention | Follows JavaBean naming conventions |

#### **5. Why do we use POJO classes?**  
POJO classes are used to:  
- Represent **entities or models** in applications.  
- Store and **transfer data** between different layers.  
- Work with **ORM frameworks** like Hibernate.  
- Maintain a **clean separation of concerns** in applications.

#### **6. Can a POJO class have a constructor with arguments?**  
Yes, a POJO class can have **both a no-argument constructor and parameterized constructors**.

#### **7. Does a POJO class have to implement `Serializable`?**  
No, but if you need to **serialize** the object (e.g., save it to a file or send it over a network), it should implement `Serializable`.

Example:
```java
import java.io.Serializable;

public class Employee implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private int id;

    // Getters, Setters, and Constructors...
}
```

#### **8. Can a POJO class contain methods other than getters and setters?**  
Yes, a POJO class can have **utility methods** such as `toString()`, `equals()`, and `hashCode()`.  

Example:
```java
@Override
public String toString() {
    return "Person{name='" + name + "', age=" + age + "}";
}
```

#### **9. Is a POJO class required to follow a naming convention?**  
No, there are **no strict naming rules** for POJO classes, but it is recommended to follow Java conventions (CamelCase for class names, lowercase for variables).

#### **10. What is the advantage of using POJO over normal Java classes?**  
- **Easier to read and maintain.**  
- **Decoupled from frameworks** (unlike JavaBeans).  
- **Works well with ORM tools** (Hibernate, JPA).  
- **Simple and reusable** across different projects.

---

Would you like examples for specific use cases? 🚀
