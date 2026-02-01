# 🏛️ Lab 3: Advanced Class Design

## 1. Object Relationships (Has-A)
The fundamental difference between Aggregation and Composition is given by the **lifecycle** of objects.

### A. Aggregation (Weak Has-A)
* **Definition:** The "child" object can exist independently of the "parent".
* **Instantiation:** The object is created externally and passed through the constructor.
* **Example:** `Department` has `Employee[]`. If you delete the department, employees don't disappear (they just become unemployed).
* **Visual hint:** The object comes as a parameter in the constructor.

### B. Composition (Strong Has-A)
* **Definition:** The "child" object is created and managed exclusively by the "parent".
* **Dependency:** If parent is destroyed, child is destroyed too.
* **Example:** `House` has `Room[]`. If you demolish the house, rooms disappear.
* **Visual hint:** The `new` operator appears inside the container class.

## 2. Inheritance (Is-A)
Mechanism by which a class takes functionality from another class (`extends`).
* **Rule:** Java allows only **single inheritance** (one parent class).
* **Constructors:** Are NOT inherited!
    * Initialization order: `Parent` -> `Child`.
    * **`super()`**: Calls parent constructor. **Must be first instruction** in child constructor.
* **Modifiers:**
    * `protected`: Accessible in same package + subclasses (even if subclass is in another package).
* **`final` Classes:** Cannot be inherited (ex: `String`, `Math`).

## 3. Polymorphism
Ability of an object to be treated as an instance of the parent class.

### A. Upcasting (Implicit & Safe)
* Conversion from Child to Parent.
* `Animal a = new Dog();`
* Access only to methods in `Animal`, but execution will be from `Dog` (if overridden).

### B. Downcasting (Explicit & Risky)
* Conversion from Parent to Child.
* Requires check with `instanceof` to avoid `ClassCastException`.
* `if (a instanceof Dog) { ((Dog)a).bark(); }`

### C. Types of Polymorphism
1.  **Static (Overloading):** Same name, different parameters (resolved at compile time).
2.  **Dynamic (Overriding):** Same signature, different implementation in child (resolved at runtime).
    * **Restrictions:** Cannot override `static` methods (only hide them - Method Hiding) or `final`.
    * **Access:** Method in child cannot have more restrictive access than parent.

## 4. Methods from `Object` class
All classes automatically inherit from `Object`.
* **`toString()`**: Returns text representation. Default is memory address (`Class@Hash`). Should be overridden for useful data.
* **`equals(Object o)`**: Compares logical equality.
    * `==` compares references (addresses).
    * `equals` should be overridden to compare content (ex: ID, name).

## 5. 🧠 Memory & VTables (Advanced)
* **Metaspace:** Memory zone where JVM keeps class structure.
* **VTable (Virtual Method Table):**
    * Table used by JVM at **runtime** to decide which overridden method to call (Dynamic Dispatch).
    * *Note:* **Static** methods are NOT in VTable (so they have no dynamic polymorphism).
