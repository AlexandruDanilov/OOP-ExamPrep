# 🌀 Lab 4: Abstraction, Special Classes and Restrictions

## 1. Abstraction
OOP principle that hides implementation details and exposes only essential functionality.

### A. Abstract Methods
* Declared with `abstract`.
* Have **NO** body (implementation), only signature (ending with `;`).
* Can exist **only** in abstract classes or interfaces.
* *Purpose:* Forces subclasses to provide their own implementation.

### B. Abstract Classes
* Declared with `abstract class`.
* **Cannot** be instantiated (`new Vehicle()` ❌).
* Can contain:
    * Abstract methods.
    * Concrete methods (with code).
    * Fields (instance variables).
    * Constructors (called by children via `super()` for initialization).
* *Use:* When classes share lots of code (IS-A relationship), but some behaviors differ.

## 2. Interfaces
Define a **contract** ("What it can do", not "What it is").
* Declared with `interface`.
* **Cannot** have constructors or state (instance variables).
* **Implicit members:**
    * Methods are `public abstract` (until Java 8).
    * Variables are `public static final` (constants).
* **Inheritance:**
    * A class can implement **multiple** interfaces (`implements A, B`).
    * An interface can extend other interfaces (`extends X, Y`).

### Java 8+ Interface News
1.  **`default` Methods:** Have implementation (body) in the interface.
    * *Purpose:* Compatibility (adding new method without "breaking" existing classes).
2.  **`static` Methods:** Utility methods related to the interface.

### ⚔️ Abstract Class vs Interface
| Feature | Abstract Class | Interface |
| :--- | :--- | :--- |
| **Relationship** | **IS-A** (Kind of...) | **CAN-DO** (Ability/Contract) |
| **Inheritance** | Single (`extends`) | Multiple (`implements`) |
| **Constructor** | Yes | No |
| **Variables** | Any type | Only constants (`static final`) |

## 3. Special Classes & Immutability

### A. Immutable Objects
* Their state **CANNOT** be modified after creation.
* *Examples:* `String`, `LocalDate`, Wrapper classes (`Integer`).
* **Recipe:** `final` class, `private final` fields, no setters, constructor that sets everything.
* *Advantage:* Thread-safe, good for HashMap keys.

### B. Enums (Enumerations)
* Fixed set of named constants (`enum Direction { NORTH, SOUTH }`).
* Are real classes: can have constructors (private!), methods, and fields.
* Useful methods: `values()` (array with all), `valueOf("NAME")`, `ordinal()`.

### C. Records (Java 16+)
* `public record User(String name, int age) {}`
* Automatically creates an **immutable** and **final** class.
* Auto-generates:
    * Constructor (canonical).
    * `equals()`, `hashCode()`, `toString()`.
    * Getters (without the `get` prefix, ex: `user.name()`).
* *Use:* Ideal for **DTO** (Data Transfer Objects) - data carriers without logic.

## 4. Pitfalls (Exam Tips) ⚠️
1.  **Diamond Problem:** If you implement two interfaces with same `default` method, you're **forced** to override the method in your class to resolve conflict (`A.super.method()`).
2.  **Variables in Interfaces:** If you write `int x = 5;` in an interface, it's automatically `public static final`. You can't change it.
3.  **Records:** Cannot extend other classes (already extend `Record`), but can implement interfaces.
