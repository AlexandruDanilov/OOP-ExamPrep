# 🔧 Lab 11: Functional Programming, Lambdas and Streams

## 1. Functional Programming in Java
Declarative programming style (you say *what* you want, not *how* to do it step-by-step), based on pure functions and immutability.

### A. Functional Interfaces
An interface with **exactly one abstract method** (can have any number of `default` or `static` methods).
* Annotation: `@FunctionalInterface` (optional, but recommended).
* *Example:* `Runnable`, `Comparator`, `ActionListener`.

### B. Lambda Expressions
Inline implementation of a functional interface (an anonymous function).
* **Syntax:** `(parameters) -> { body }`
* *Example:* `(a, b) -> a + b` is an implementation for `int apply(int x, int y)`.
* **Restrictions:** Local variables used in lambda must be **final** or **effectively final** (value doesn't change).

## 2. Standard Functional Interfaces (`java.util.function`)
Java already provides interfaces for the most common scenarios:

| Interface | Method | Receives | Returns | Purpose | Example Lambda |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`Predicate<T>`** | `test(T t)` | `T` | `boolean` | Filtering, conditions | `x -> x > 0` |
| **`Function<T,R>`** | `apply(T t)` | `T` | `R` | Transformation (mapping) | `s -> s.length()` |
| **`Consumer<T>`** | `accept(T t)` | `T` | `void` | Action (print, log) | `s -> sout(s)` |
| **`Supplier<T>`** | `get()` | - | `T` | Providing values | `() -> Math.random()` |

* **Method References (`::`):** Shortcut for lambda.
    * `s -> System.out.println(s)` becomes `System.out::println`.

## 3. Stream API (`java.util.stream`) 🌊
A sequence of elements supporting sequential or parallel aggregate operations.
**A Stream is NOT a collection!** Doesn't store data, just processes it.

### The Stream Pipeline
1.  **Source:** `list.stream()`, `Arrays.stream()`.
2.  **Intermediate Operations (Lazy):** Don't execute immediately, just configure the pipeline. Return a `Stream`.
    * `filter(Predicate)`: Keep elements that pass the test.
    * `map(Function)`: Transform each element.
    * `distinct()`, `sorted()`, `limit()`.
3.  **Terminal Operation (Eager):** Triggers processing and produces result. Stream closes.
    * `forEach(Consumer)`: Iterate.
    * `collect(Collectors.toList())`: Gather results.
    * `count()`, `reduce()`, `findFirst()`.

### Golden Rules
1.  A Stream **cannot be reused** after it's closed (after terminal operation).
2.  Intermediate operations are **Lazy** (if you don't have terminal, nothing executes).
3.  **No side-effects:** Don't modify external variables from lambda (unless atomic/thread-safe).

## 4. Optional (`java.util.Optional`)
A container for a value that may be `null`. Avoids `NullPointerException`.
* **Creation:** `Optional.of(val)` (not null), `Optional.ofNullable(val)` (may be null), `Optional.empty()`.
* **Usage:**
    * `.isPresent()`: Check (old style).
    * `.ifPresent(Consumer)`: Execute only if value exists.
    * `.orElse(defaultVal)`: Return value or default.
    * `.orElseThrow()`: Throw exception if empty.
