# 💥 Lab 7: I/O and Exception Handling

## 1. Exceptions
Mechanism for handling errors that separates program logic from exception handling.

### A. Basic Mechanism
* **Throwing (`throw`):** Signaling an error.
* **Catching (`catch`):** Handling the error.
* **Structure:**
    ```java
    try {
        // Code that may throw errors
    } catch (ExceptionType e) {
        // Handle
    } finally {
        // Executes ALWAYS (for cleanup)
    }
    ```
* **Multi-catch (Java 7+):** `catch (IOException | SQLException e) { ... }`

### B. Throwable Hierarchy
1.  **Checked Exceptions (`Exception`):**
    * Anticipated errors (missing file, network).
    * **Must** be handled (`try-catch` or `throws`).
2.  **Unchecked Exceptions (`RuntimeException`):**
    * Programming bugs (null pointer, index out of bounds).
    * **Optional** to handle.
3.  **Errors (`Error`):**
    * Serious system problems (Out of Memory). Not caught.

### C. Special Rules
* **Propagation:** If a method doesn't catch the exception, it goes up the stack to the caller.
* **Inheritance:** An overridden method **cannot** throw new checked exceptions or more general ones than the parent.
* **Try-with-resources:** Automatically closes resources (`AutoCloseable`).
    ```java
    try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) { ... }
    ```

---

## 2. File I/O (Input/Output)
Java uses streams to manipulate data.

### A. Reading Methods
1.  **`Scanner`:**
    * Good for reading tokens (words, numbers).
    * Methods: `nextInt()`, `nextDouble()`.
    * *Disadvantage:* Slower for large files (does parsing).
2.  **`FileReader`:**
    * Reads text files character by character.
    * Simple, but inefficient without buffer.
3.  **`InputStreamReader`:**
    * Adapter: Transforms `InputStream` (bytes) to `Reader` (characters).
    * Allows specifying encoding (UTF-8).
4.  **`BufferedReader`:**
    * Most efficient for text.
    * Reads large blocks into memory.
    * Method `readLine()` reads line by line.

### B. Writing Methods
1.  **`PrintWriter`:**
    * Formatted writing (`printf`, `println`).
    * Easy to use ("user-friendly").
2.  **`FileWriter`:**
    * Writes characters directly to file.
    * Overwrites file unless we use `append = true`.
3.  **`OutputStreamWriter`:**
    * Adapter: Characters -> Bytes.
    * Controls encoding on write.
4.  **`BufferedWriter`:**
    * Efficient writing (uses buffer).
    * Method `newLine()` adds OS-specific line separator.

### C. Advanced Concepts
* **Byte Streams (`FileInputStream`/`FileOutputStream`):** For binary data (images, audio).
* **`File` Class:** Represents the path and metadata (name, permissions, existence), NOT content.
* **`RandomAccessFile`:** Allows reading/writing at arbitrary position (`seek(pos)`).
