# ☕ Laborator 1: Limbajul Java - Sinteză

## 1. Arhitectură și Compilare
* **Java** este un limbaj compilat și interpretat.
* **Flux:**
    1.  Cod sursă (`.java`) -> Compilator (`javac`) -> Bytecode (`.class`).
    2.  Bytecode -> JVM (`java`) -> Cod mașină (specific OS).
* **Portabilitate:** "Write Once, Run Anywhere" (datorită JVM).
* **Entry Point:**
    ```java
    public static void main(String[] args) { ... }
    ```
    * `public`: accesibil JVM-ului.
    * `static`: apelabil fără instanță.
    * `void`: nu returnează nimic.
    * `String[] args`: argumente din linia de comandă.

## 2. Tipuri de Date Primitive (8 tipuri)
În Java, primitivele **NU** sunt obiecte (pentru performanță).

| Categorie | Tip | Biți | Interval / Notă |
| :--- | :--- | :--- | :--- |
| **Întregi** | `byte` | 8 | -128 ... 127 (Atenție la overflow!) |
| | `short` | 16 | -32,768 ... 32,767 |
| | `int` | 32 | Default pentru numere întregi. |
| | `long` | 64 | Necesită sufix `L` (ex: `123L`). |
| **Reale** | `float` | 32 | Necesită sufix `f` (ex: `3.14f`). |
| | `double` | 64 | Default pentru zecimale. |
| **Caractere** | `char` | 16 | Unicode (ex: `'A'`, `'\u0041'`). |
| **Logic** | `boolean`| 1* | `true` sau `false`. |

* **Overflow:** Comportament ciclic (127 + 1 la byte devine -128).
* **Separatori:** `int bani = 1_000_000;` (pentru lizibilitate).

## 3. Conversii (Casting)
* **Implicit (Widening):** De la mic la mare (sigur).
    * `byte` → `int` → `double`.
* **Explicit (Narrowing):** De la mare la mic (risc de pierdere date).
    * `double d = 9.99; int i = (int) d;` // i devine 9.

## 4. Structuri de Control
* **Conditionale:**
    * `if`, `else if`, `else`.
    * `switch`: Merge pe primitive, String și Enum. Necesită `break`.
    * **Ternar:** `condiție ? val_true : val_false`.
* **Bucle:**
    * `for` (clasic), `while`, `do-while`.
    * **Enhanced for:** `for (int x : array) { ... }`.
    * `break`: Oprește bucla.
    * `continue`: Sare la iterația următoare.

## 5. Array-uri (Tablouri)
* Sunt obiecte, au dimensiune fixă după creare.
* Proprietatea `.length` (fără paranteze!) returnează dimensiunea.
* **Declarare:**
    ```java
    int[] arr = new int[5]; // plin cu 0
    int[] arr2 = {1, 2, 3}; // inițializare directă
    ```

## 6. Afișare
* `System.out.print("Text");` (fără linie nouă).
* `System.out.println("Text");` (cu linie nouă).
* `System.out.printf("Numar: %d", 10);` (formatat, ca în C).