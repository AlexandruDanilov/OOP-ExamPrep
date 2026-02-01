# ☕ Lab 1: Java Language - Summary

## 1. Architecture and Compilation
* **Java** is a compiled and interpreted language.
* **Flow:**
    1.  Source code (`.java`) -> Compiler (`javac`) -> Bytecode (`.class`).
    2.  Bytecode -> JVM (`java`) -> Machine code (OS-specific).
* **Portability:** "Write Once, Run Anywhere" (thanks to JVM).
* **Entry Point:**
    ```java
    public static void main(String[] args) { ... }
    ```
    * `public`: accessible to the JVM.
    * `static`: callable without an instance.
    * `void`: returns nothing.
    * `String[] args`: command-line arguments.

## 2. Primitive Data Types (8 types)
In Java, primitives are **NOT** objects (for performance).

| Category | Type | Bits | Range / Note |
| :--- | :--- | :--- | :--- |
| **Integers** | `byte` | 8 | -128 ... 127 (Watch out for overflow!) |
| | `short` | 16 | -32,768 ... 32,767 |
| | `int` | 32 | Default for integers. |
| | `long` | 64 | Requires `L` suffix (ex: `123L`). |
| **Floats** | `float` | 32 | Requires `f` suffix (ex: `3.14f`). |
| | `double` | 64 | Default for decimals. |
| **Characters** | `char` | 16 | Unicode (ex: `'A'`, `'\u0041'`). |
| **Boolean** | `boolean`| 1* | `true` or `false`. |

* **Overflow:** Cyclic behavior (127 + 1 on byte becomes -128).
* **Separators:** `int money = 1_000_000;` (for readability).

## 3. Type Conversions (Casting)
* **Implicit (Widening):** From small to large (safe).
    * `byte` → `int` → `double`.
* **Explicit (Narrowing):** From large to small (risk of data loss).
    * `double d = 9.99; int i = (int) d;` // i becomes 9.

## 4. Control Structures
* **Conditionals:**
    * `if`, `else if`, `else`.
    * `switch`: Works on primitives, String, and Enum. Requires `break`.
    * **Ternary:** `condition ? val_true : val_false`.
* **Loops:**
    * `for` (classic), `while`, `do-while`.
    * **Enhanced for:** `for (int x : array) { ... }`.
    * `break`: Stops the loop.
    * `continue`: Jumps to next iteration.

## 5. Arrays (Tables)
* Are objects, have fixed size after creation.
* Property `.length` (no parentheses!) returns the size.
* **Declaration:**
    ```java
    int[] arr = new int[5]; // filled with 0
    int[] arr2 = {1, 2, 3}; // direct initialization
    ```

## 6. Output
* `System.out.print("Text");` (no newline).
* `System.out.println("Text");` (with newline).
* `System.out.printf("Number: %d", 10);` (formatted, like in C).
