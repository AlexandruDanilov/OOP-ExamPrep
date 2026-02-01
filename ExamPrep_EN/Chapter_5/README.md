# 🪆 Lab 5: Inner Classes and Strings

## 1. Inner Classes (Nested Classes)
Classes defined inside another class to logically group closely related entities.

### A. Types of Inner Classes
1.  **Normal Inner Classes (Non-static Inner Classes):**
    * Have access to the outer class instance members (even `private`).
    * **Instantiation:** Requires an outer class instance.
        ```java
        Outer outer = new Outer();
        Outer.Inner inner = outer.new Inner();
        ```
    * Access outer `this`: `OuterClassName.this`.

2.  **Static Nested Classes:**
    * Behave like a normal class, just "nested" in another.
    * **Cannot** access non-static members of the outer class.
    * **Instantiation:** Doesn't require outer instance.
        ```java
        Outer.StaticInner inner = new Outer.StaticInner();
        ```

3.  **Anonymous Inner Classes:**
    * Classes without name, defined and instantiated on the spot.
    * Used for quick implementations of interfaces/abstract classes (ex: Event Listeners).
    * **Limitations:** No constructors. Can access local variables only if they're `final` or *effectively final*.
    * **Lambda:** `() -> {}` (replaces anonymous classes for functional interfaces).

4.  **Local Inner Classes:**
    * Defined inside a method. Visible only there.

## 2. Strings (Character Strings) 🧶
`String` is an immutable object in Java.

### A. Creation and Memory
* **Literal:** `String s = "Java";` -> Stored in **String Pool** (Heap). Reuses identical objects (memory-efficient).
* **Constructor:** `String s = new String("Java");` -> Forces creation of a **NEW** object in Heap (inefficient).

### B. Immutability
* Once created, a String's content **CANNOT** be changed.
* Methods that seem to modify (`concat`, `toUpperCase`) actually return a **new** object.
    ```java
    String s = "a";
    s.concat("b"); // s remains "a"
    s = s.concat("b"); // s becomes "ab" (new reference)
    ```

### C. Comparison
* `==` : Compares **references** (memory addresses).
    * `"A" == "A"` -> `true` (same object from Pool).
    * `new String("A") == "A"` -> `false`.
* `.equals()` : Compares **content** (text). **Always use `.equals()`!**

### D. Performance: StringBuilder
* For repeated concatenations (ex: in loops), `String` is slow (creates thousands of temporary objects).
* **Solution:** Use `StringBuilder` (mutable).
    * `sb.append("x")` modifies the internal buffer without creating new objects.

### E. Utilities
* `String.valueOf(x)`: Converts anything to String (safe for null).
* `Integer.parseInt("123")`: String -> int.
* `split(regex)`: Splits text into tokens.
* `regex`: Regular expressions (`\\d+` digits, `\\s` spaces).
