# 🚀 Lab 12: Advanced Java Programming

## 1. Serialization
Process of transforming a Java object into a stream of bytes (for saving to file or sending over network).
* **Deserialization:** The reverse process (Bytes -> Object).

### A. Native Serialization
* Class must implement `java.io.Serializable` (marker interface).
* `ObjectOutputStream.writeObject(obj)`: Serialization.
* `ObjectInputStream.readObject()`: Deserialization.
* **`transient`:** Keyword for fields that should **NOT** be serialized (ex: passwords).
* **`serialVersionUID`:** Unique ID for versioning the class. If class changes, ID prevents wrong deserialization.

### B. JSON Serialization (with Jackson)
Modern standard. Uses text (JSON) instead of binary format.
* **Library:** `com.fasterxml.jackson.core`.
* **Annotations:**
    * `@JsonProperty("json_name")`: Maps a Java field to different JSON name.
    * `@JsonIgnore`: Excludes field from JSON.
* **Usage:** `ObjectMapper mapper = new ObjectMapper(); mapper.writeValueAsString(obj);`.

## 2. Annotations
Metadata added to code (`@Name`). Don't directly change logic, but are read by compiler or at runtime.
* **Definition:** `public @interface MyAnnotation { ... }`.
* **Meta-annotations:**
    * `@Target`: Where it applies (FIELD, METHOD, TYPE).
    * `@Retention`: How long it lives (SOURCE, CLASS, RUNTIME). For Reflection, needs `RUNTIME`.

## 3. Reflection 🪞
Mechanism allowing code to inspect its own structure at runtime.
* **Entry point:** `Class<?>` class.
    * `obj.getClass()` or `ClassName.class`.
* **Capabilities:**
    * Get methods, fields, constructors (`getDeclaredMethods()`).
    * Access **private** fields (`field.setAccessible(true)`).
    * Dynamic instantiation (`clazz.newInstance()`).
* **Use:** Frameworks (Spring, Hibernate, JUnit) to inject dependencies or run tests without knowing class names at compile time.
* **Disadvantages:** Slow, breaks encapsulation, errors only at runtime.

## 4. Automated Testing (Unit Testing) 🧪
Isolated testing of code units (methods/classes).

### A. JUnit (Testing Framework)
* **`@Test`:** Marks a method as a test.
* **Assertions:** `assertEquals(expected, actual)`, `assertTrue(cond)`, `assertThrows(Exception.class, () -> ... )`.
* **Lifecycle:** `@BeforeEach` (setup before each test), `@AfterEach` (cleanup).

### B. Mocking (with Mockito)
Simulating external dependencies (databases, APIs) to test in isolation.
* **`mock(Class.class)`:** Creates a fake object.
* **`when(mock.method()).thenReturn(value)`:** Defines simulated behavior.
* **`verify(mock).method()`:** Checks if method was called.

### C. Assertions (Keyword `assert`)
* `assert condition : "Message";`
* Used for internal verifications (invariants).
* Activated with `-ea` (Enable Assertions) at runtime. Doesn't replace Unit Testing.
