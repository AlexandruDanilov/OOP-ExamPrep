# 🏗️ Lab 8: Design Patterns I

Design Patterns are reusable solutions for common software architecture problems. Split into:
1.  **Creational:** Object creation (Singleton, Factory).
2.  **Structural:** Class structure (Proxy).
3.  **Behavioral:** Communication between objects (Visitor).

---

## 1. Singleton (Creational) 🔒
Ensures a class has **only one instance** and provides a global point of access to it.

### Implementation
1.  **Private constructor** (blocks `new` from outside).
2.  **Static instance** (unique, stored internally).
3.  **Public static method** (`getInstance`) that returns the instance.

```java
// Most secure variant (Thread-safe, Serialization-safe)
public enum Singleton {
    INSTANCE;
    public void doSomething() { System.out.println("Working..."); }
}

// Classic variant (Lazy Initialization - not recommended without synchronization in multithreading)
public class Config {
    private static Config instance;
    private Config() {} // Private constructor
    
    public static Config getInstance() {
        if (instance == null) {
            instance = new Config(); // Created only on first use
        }
        return instance;
    }
}
```

* **Use:** Logger, Configuration, Database Connections.
* **Why is it Anti-Pattern?** Introduces hidden global state, creates tight coupling, makes **unit testing difficult** (hard to replace with mocks).
* **Alternative:** Dependency Injection (Aggregation).

---

## 2. Factory Patterns (Creational) 🏭

### A. Factory Method
Defines an interface for creating an object, but lets subclasses decide the exact class instantiated.
* **Problem:** Client code shouldn't depend on concrete classes (`Truck`, `Ship`) and the `new` keyword.
* **Solution:** `Transport t = logistics.createTransport();`
* **Advantage:** Respects Open/Closed Principle (can add new transport types without modifying client logic).

### B. Abstract Factory
Creates **families** of related (compatible) objects without specifying concrete classes.
* **Example:** `GUIFactory` that produces `Button` and `Checkbox`.
    * `WindowsFactory` -> produces `WindowsButton` + `WindowsCheckbox`.
    * `MacFactory` -> produces `MacButton` + `MacCheckbox`.
* **Difference:**
    * *Factory Method:* Creates a single product.
    * *Abstract Factory:* Creates a family of products that must work together.

---

## 3. Visitor (Behavioral) 🚶‍♂️
Allows adding new operations to an existing object structure (class hierarchy) without modifying the classes themselves.

### The Problem: Double Dispatch
In Java, overloading (Overloading) is static (decided at compile time).
```java
void export(Node n) { ... }
void export(City c) { ... }
...
Node n = new City();
exporter.export(n); // Calls export(Node), NOT export(City)!
```

### The Visitor Solution
Uses **Double Dispatch** to determine correct method at runtime.
1.  **Visitable (Element):** Has `accept(Visitor v)` method.
    * Implementation: `v.visit(this);` -> Here `this` is concrete type (`City`), so it binds correctly.
2.  **Visitor:** Has methods `visit(City)`, `visit(Industry)`.

* **Use:** Export (XML/JSON), Reporting, Validation on complex structures.

---

## 4. Proxy (Structural) 🛡️
An intermediary that controls access to an original object.
* **Virtual Proxy (Lazy Loading):** Loads the real object (expensive) only when needed. Ex: loading a large image only when it appears on screen.
* **Protection Proxy:** Checks access rights before delegating the request.
* **Remote Proxy:** Local representation of an object on another server.
