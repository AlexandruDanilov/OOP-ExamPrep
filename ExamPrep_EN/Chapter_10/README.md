# 🏷️ Lab 10: Generics

## 1. Why Generics?
Before Java 5, collections used `Object`, leading to runtime type errors and dangerous manual casts.
Generics move type checking to **compile time**.

* **Without Generics (Raw Types):**
    ```java
    List list = new ArrayList();
    list.add("Hello");
    Integer i = (Integer) list.get(0); // Runtime Error: ClassCastException
    ```
* **With Generics:**
    ```java
    List<String> list = new ArrayList<>();
    // list.add(10); // Compile Error! (Safety)
    String s = list.get(0); // Cast not needed
    ```

## 2. Parameterized Types
Classes and interfaces can receive types as parameters (`<T>`, `<E>`, `<K, V>`).

### A. Generic Classes
```java
public class Box<T> {
    private T value;
    public void set(T val) { this.value = val; }
    public T get() { return value; }
}
// Usage: Box<Integer> intBox = new Box<>();
```

### B. Generic Methods
Can have their own type parameters, independent of the enclosing class.
```java
// <T> before return type marks method as generic
public static <T> T identity(T val) { return val; }
```

### C. Bounded Generics (Constraints)
Can restrict accepted types using `extends`.
* `<T extends Number>`: T must be `Number` or a subclass (Integer, Double).
* `<T extends Comparable<T>>`: T must be comparable.

---

## 3. Wildcards (?)
Used when we don't know (or don't care about) the exact type of the collection.

### A. Unbounded (`?`)
`List<?>`: List of anything.
* Can read only `Object`.
* **Cannot** add anything (except `null`), because we don't know what type the list accepts.

### B. Upper Bounded (`? extends T`) - Producer
`List<? extends Number>`: List contains `Number` or subclasses.
* **Reading:** Safe (read as `Number`).
* **Writing:** Forbidden (don't know if list is `Integer` or `Double`).

### C. Lower Bounded (`? super T`) - Consumer
`List<? super Integer>`: List contains `Integer` or parents (`Number`, `Object`).
* **Reading:** Only as `Object` (not useful).
* **Writing:** Safe (can add `Integer` or subclasses).

> **PECS Rule:** **P**roducer **E**xtends, **C**onsumer **S**uper.

---

## 4. Type Erasure (Type Elimination) ⚠️
Generics exist **only at compile time**. At runtime, JVM erases generic types (`List<String>` becomes `List`, and `T` becomes `Object` or its bound).

**Consequences and Restrictions:**
1.  **Cannot** instantiate generic type: `new T()` ❌.
2.  **Cannot** create generic arrays: `new T[10]` ❌.
3.  **Cannot** use primitives: `List<int>` ❌ (use `List<Integer>`).
4.  **Cannot** use `instanceof List<String>` (only `instanceof List<?>`).
5.  **Invariance:** `List<Object>` is **NOT** parent of `List<String>`.
    * Arrays are covariant (`Object[]` = `String[]`), but generics are invariant.

---

## 5. Generics Glossary
* **T** (Type), **E** (Element), **K** (Key), **V** (Value).
* **Raw Type:** `List l = new ArrayList();` (Avoid!).
* **Reified:** Types that exist at runtime (Arrays). Generics are **Non-reified**.
