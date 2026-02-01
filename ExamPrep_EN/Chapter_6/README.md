# 📦 Lab 6: Collections, Special Types and Utilities

## 1. Wrapper Classes
Java separates **Primitive** types (efficient, but simple) from **Objects** (extra functionality, but costly). Wrappers bridge the gap.

* **Primitives:** `int`, `double`, `boolean`, `char`.
* **Wrappers:** `Integer`, `Double`, `Boolean`, `Character`.
* **Autoboxing:** Automatic conversion Primitive → Object (`Integer a = 10;`).
* **Unboxing:** Automatic conversion Object → Primitive (`int b = a;`).
* **Pitfall:** Comparing Wrappers with `==` compares references, not values!
    ```java
    Integer a = 1000, b = 1000;
    System.out.println(a == b); // false (different objects)
    System.out.println(a.equals(b)); // true (equal values)
    ```
    *Note:* Java caches small Integers (-128 to 127), so there `==` might return `true`, but don't rely on it.

## 2. Java Collections Framework (JCF)
Dynamic data structures. Main hierarchy splits into `Collection` and `Map`.

### A. List (Ordered, Duplicates allowed)
* **`ArrayList`:** Dynamic array.
    * Fast for reading (`get` -> O(1)).
    * Slow for insertion/deletion in middle (must shift elements).
* **`LinkedList`:** Doubly linked list.
    * Fast for insertion/deletion.
    * Slow for random access (`get` -> O(n)).

### B. Set (Unique, No duplicates)
* **`HashSet`:** Unordered. Fastest (O(1)). Uses `hashCode`.
* **`LinkedHashSet`:** Preserves insertion order.
* **`TreeSet`:** Sorts elements (naturally or with Comparator). O(log n).

### C. Queue (Queues)
* **`PriorityQueue`:** Elements come out by priority (sorted), not FIFO.
* **`ArrayDeque`:** Double queue, faster than LinkedList for stacks/queues.

### D. Map (Key-Value) - Does NOT extend Collection
* **`HashMap`:** Fast, unordered. Allows one `null` key.
* **`LinkedHashMap`:** Preserves insertion order.
* **`TreeMap`:** Keys sorted. Doesn't allow `null` keys.

## 3. Comparison and Sorting
* **`Comparable<T>`:** "Natural order". Implemented **in the object's class**.
    * Method: `compareTo(T o)`.
    * Ex: `Collections.sort(list)` uses this.
* **`Comparator<T>`:** "Custom order". Implemented in a **separate class** (or lambda).
    * Method: `compare(T o1, T o2)`.
    * Ex: `list.sort(new NameComparator())`.

## 4. Equals & HashCode Contract ⚠️
Critical for `HashSet` and `HashMap`.
1.  If `a.equals(b)` is true, then `a.hashCode() == b.hashCode()` **MUST** be true.
2.  If you break this, hash collections will "lose" objects (put in one bucket, search in another).

## 5. Utilities
### A. Math & Big Numbers
* `Math`: Static methods (`sqrt`, `pow`, `random`).
* `BigInteger` / `BigDecimal`: For huge numbers or absolute financial precision (avoids floating-point errors of `double`).

### B. Date and Time (Java 8+)
Immutable classes (thread-safe):
* `LocalDate`: Date only (2023-10-05).
* `LocalTime`: Time only (14:30).
* `LocalDateTime`: Date + Time.
* `ZonedDateTime`: Date + Time + Timezone.
* Formatting: `DateTimeFormatter`.
