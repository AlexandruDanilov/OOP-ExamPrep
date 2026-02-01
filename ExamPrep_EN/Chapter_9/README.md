# 🏗️ Lab 9: Design Patterns II

## 1. Builder (Creational) 👷
Used to build complex objects step by step. Separates construction from representation.


### The Problem (Telescoping Constructor)
Without Builder, for an object with many optional parameters (ex: `Pizza`), we'd have huge, hard-to-read constructors:
`new Pizza("Large", "Thin", 1, 0, 1, 0, ...)` -> What do `1, 0` mean?

### The Builder Solution
A static inner class `Builder` with methods for each parameter (returning `this` for chaining).
```java
Pizza p = new Pizza.Builder("Large", "Thin") // Required parameters
            .cheeseCount(1)                  // Optional
            .pepperoniCount(2)               // Optional
            .build();                        // Construct the final object
```
* **Advantages:** Readable code, immutability (final object has no setters), avoids inconsistent states.

---

## 2. Observer (Behavioral) 👀
Defines a **1-to-N** dependency relationship between objects. When one object (Subject) changes state, all dependents (Observers) are notified automatically.


### Structure
1.  **Subject (Publisher):** Keeps list of observers (`add`, `remove`, `notify`).
2.  **Observer (Subscriber):** Interface with `update()` method.
3.  **ConcreteObserver:** Implements reaction to notification.

* **Example:** YouTube Channel (Subject) -> Subscribers (Observers). When new video is posted, all subscribers get notified.
* **Advantage:** Complete decoupling. Subject doesn't know who observers are or what they do, just notifies them.

---

## 3. Strategy (Behavioral) 🎲
Allows defining a family of algorithms, encapsulating each, and making them interchangeable at runtime.


### Structure
1.  **Context:** Class using the strategy (`ShoppingCart`).
2.  **Strategy Interface:** Common interface (`PaymentStrategy`).
3.  **Concrete Strategies:** Specific implementations (`CardPayment`, `PayPalPayment`).

* **Example:** `ShoppingCart` can pay by Card or PayPal. Can change payment method at runtime without modifying cart code.
* **Difference vs Factory:** Factory creates objects, Strategy changes the behavior (algorithm) of an existing object.

---

## 4. Command (Behavioral) 🎮
Encapsulates a request (action) as an object. Allows parameterizing clients with requests, queuing them, and supporting **Undo/Redo** operations.


### Structure
1.  **Command Interface:** `void execute()`, `void undo()`.
2.  **ConcreteCommand:** Ties an action to a Receiver (`LightOnCommand`).
3.  **Invoker:** Whoever triggers the command (Remote / Button).
4.  **Receiver:** Who does the actual work (Light / TV).

* **Use:** Text editor (Copy/Paste/Undo), Universal remote, Job Queues.
* **Advantage:** Decouples who requests action (button) from who executes it (light).

---

## 5. Comparisons (Tips & Tricks)
* **Factory vs Builder:**
    * Factory: Creates object "all at once" (everything ready immediately).
    * Builder: Builds object step by step (good for complex configurations).
* **Strategy vs State vs Command:**
    * **Strategy:** "How do I do this?" (Interchangeable algorithm).
    * **Command:** "When do I do this?" (Action stored for later/undo).
