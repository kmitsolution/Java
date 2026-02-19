# ✅ Why Field Injection Breaks Immutability in Spring

Let’s understand this step by step in simple terms.

---

# 🔹 What is Immutability?

An object is **immutable** if:

1. Its state (data) cannot change after creation.
2. All fields are `final`.
3. Values are set only once (inside constructor).

Example of immutable class:

```java
public class Student {

    private final String name;

    public Student(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

✔ `name` is final
✔ Cannot change after object creation
✔ Fully immutable

---

# 🔴 Now Let’s See Field Injection

Example:

```java
@Component
public class SearchService {

    @Autowired
    private SortAlgorithm sortAlgorithm;

}
```

Here Spring:

1. Creates object first
2. Then injects dependency using reflection
3. Sets the field value AFTER object creation

---

# ❌ Why This Breaks Immutability

## 1️⃣ Field Cannot Be `final`

If you write:

```java
@Autowired
private final SortAlgorithm sortAlgorithm;
```

It will NOT work.

Because Spring sets the field after constructor runs.

So field injection forces you to:

```
Remove final keyword
```

That makes object mutable.

---

## 2️⃣ Object is Created Without Dependency

Field injection happens in two steps:

```
Step 1 → Object created
Step 2 → Dependency injected
```

So temporarily the object exists in incomplete state.

This violates immutability principle.

---

## 3️⃣ Reflection-Based Injection

Spring uses reflection to modify private fields.

Immutability means:

> Object should not change after construction.

But field injection changes object state after construction.

---

# 🟢 Now Compare With Constructor Injection

Example:

```java
@Component
public class SearchService {

    private final SortAlgorithm sortAlgorithm;

    public SearchService(SortAlgorithm sortAlgorithm) {
        this.sortAlgorithm = sortAlgorithm;
    }
}
```

Here:

✔ Dependency injected during construction
✔ Field can be final
✔ Object fully initialized when created
✔ Cannot change later

This preserves immutability.

---

# 🔥 Visual Comparison

## Field Injection

```
Create object → Empty dependency
      ↓
Inject dependency later
      ↓
State changed after construction
```

❌ Mutable

---

## Constructor Injection

```
Dependency provided
      ↓
Object created fully initialized
      ↓
State never changes
```

✅ Immutable

---

# 🏗 Real Example

Imagine:

```
Car needs Engine
```

Field Injection:

```
Create Car (no engine)
Later insert engine
```

Constructor Injection:

```
Car is created WITH engine
```

Which one is safer?
👉 Constructor injection.

---

# 🎯 Why Immutability Is Important?

1. Thread safety
2. Predictable behavior
3. Easier debugging
4. Better design
5. Cleaner testing

---

# 🏆 Final Summary

Field injection breaks immutability because:

* Fields cannot be `final`
* Object is created without dependencies
* State changes after construction
* Uses reflection to modify private fields

Constructor injection preserves immutability because:

* Dependencies provided at creation time
* Fields can be `final`
* Object fully initialized once
* State cannot change

---

# 🎓 Interview Answer (Short)

> Field injection breaks immutability because dependencies are injected after object creation using reflection, so fields cannot be declared final. Constructor injection ensures dependencies are provided at object creation, allowing immutable design.

---

