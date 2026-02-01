# 🧱 Lab 2: Classes, Objects, and Memory

## 1. Fundamental Concepts
* **Class:** It's the "blueprint". Defines structure (fields) and behavior (methods).
* **Object:** Is the **instance** of the class (a house built from the blueprint). Exists physically in memory.
* **Reference:** A variable that holds the address of an object.
    * `Student s;` -> Declare reference (value `null`, object doesn't exist).
    * `s = new Student();` -> Instantiation (Memory Allocation + Initialization).

## 2. Class Members
### A. Fields (State)
* Variables declared inside the class.
* **Default values:** If not initialized, JVM gives them default values:
    * Numeric: `0`
    * Boolean: `false`
    * Objects: `null`
* **Shadowing:** When a parameter has the same name as a field (`x`). Resolved with `this.x`.

### B. Methods (Behavior)
* **Overloading:** Multiple methods with the **same name** but **different parameters** (type or number).
    * *Note:* Return type does NOT matter for overloading.
* **Pass-by-value:** Java sends parameters by copying.
    * For objects, the **value of the reference** (address) is copied.
    * If you modify object fields in the method -> visible outside.
    * If you reassign the reference (`s = new Student()`) in the method -> NOT visible outside.

### C. Constructors
* Special methods called at `new`.
* **Rules:** Have the same name as the class and **NO** return type (not even `void`).
* **Default Constructor:** If you don't write any constructor, Java gives you an empty one (`Student() {}`).
    * **Attention:** If you write a constructor with parameters, the default one disappears!
* **Copy Constructor:** Receives an object of the same type to copy values.
* **Constructor Chaining:** `this(...)` calls another constructor in the same class. Must be **first instruction**.

## 3. 💾 Memory Management
### Stack (Stack)
* Fast, temporary memory.
* Here live: local variables (primitives) and **references** to objects.

### Heap (Heap)
* Dynamic memory, managed by **Garbage Collector (GC)**.
* Here live **Objects** themselves (everything created with `new`).
* **GC:** Automatically deletes objects that have no active references.

## 4. 🪨 The `static` Keyword
Static members belong to the **Class**, not instances.
* **Static fields:** A single copy in memory, shared by all objects (ex: `Apple.gravAccel`).
* **Static methods:**
    * Called via `ClassName.method()`.
    * **Cannot** access `this` or non-static members.
* **Static blocks:** `static { ... }`. Execute once, when the class is loaded into memory (before any constructor).

## 5. Encapsulation
Hiding internal details.
* **Access Modifiers:**
    * `private`: Visible only in the class.
    * `default` (missing): Visible only in the package.
    * `protected`: Package + Subclasses.
    * `public`: Visible everywhere.
* **Getter/Setter:** Public methods to control access to private fields.

## 6. Tips & Tricks (Pitfalls)
1.  **String:** Is an immutable object. Preferred initialization: `String s = "Text";`.
2.  **`this`:**
    * `this.x`: access field.
    * `method(this)`: pass current reference.
    * `this()`: call constructor (only first line).
