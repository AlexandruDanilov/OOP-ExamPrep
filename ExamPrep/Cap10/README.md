# 🏷️ Laborator 10: Genericitate (Generics)

## 1. De ce Generics?
Înainte de Java 5, colecțiile foloseau `Object`, ceea ce ducea la erori de tip la runtime și cast-uri manuale periculoase.
Generics mută verificarea tipurilor la **compilare**.

* **Fără Generics (Raw Types):**
    ```java
    List list = new ArrayList();
    list.add("Hello");
    Integer i = (Integer) list.get(0); // Runtime Error: ClassCastException
    ```
* **Cu Generics:**
    ```java
    List<String> list = new ArrayList<>();
    // list.add(10); // Compile Error! (Siguranță)
    String s = list.get(0); // Cast-ul nu mai este necesar
    ```

## 2. Tipuri Parametrizate
Clasele și interfețele pot primi tipuri ca parametri (`<T>`, `<E>`, `<K, V>`).

### A. Clase Generice
```java
public class Box<T> {
    private T value;
    public void set(T val) { this.value = val; }
    public T get() { return value; }
}
// Utilizare: Box<Integer> intBox = new Box<>();
```

### B. Metode Generice
Pot avea propriii parametri de tip, independenți de clasa în care se află.
```java
// <T> înainte de tipul returnat marchează metoda ca fiind generică
public static <T> T identity(T val) { return val; }
```

### C. Bounded Generics (Limitări)
Putem restricționa tipurile acceptate folosind `extends`.
* `<T extends Number>`: T trebuie să fie `Number` sau o subclasă (Integer, Double).
* `<T extends Comparable<T>>`: T trebuie să fie un obiect comparabil.

---

## 3. Wildcards (?)
Folosite când nu cunoaștem (sau nu ne pasă de) tipul exact al colecției.

### A. Unbounded (`?`)
`List<?>`: Listă de orice.
* Poți citi doar `Object`.
* **NU** poți adăuga nimic (decât `null`), pentru că nu știi ce tip acceptă lista.

### B. Upper Bounded (`? extends T`) - Producer
`List<? extends Number>`: Lista conține `Number` sau subclase.
* **Citire:** Sigură (citim ca `Number`).
* **Scriere:** Interzisă (nu știm dacă lista e de `Integer` sau `Double`).

### C. Lower Bounded (`? super T`) - Consumer
`List<? super Integer>`: Lista conține `Integer` sau părinți (`Number`, `Object`).
* **Citire:** Doar ca `Object` (nu e utilă).
* **Scriere:** Sigură (putem adăuga `Integer` sau subclase).

> **Regula PECS:** **P**roducer **E**xtends, **C**onsumer **S**uper.

---

## 4. Type Erasure (Ștergerea Tipurilor) ⚠️
Generics există **doar la compilare**. La runtime, JVM șterge tipurile generice (`List<String>` devine `List`, iar `T` devine `Object` sau bound-ul său).

**Consecințe și Restricții:**
1.  **Nu** poți instanția tipul generic: `new T()` ❌.
2.  **Nu** poți crea array-uri generice: `new T[10]` ❌.
3.  **Nu** poți folosi primitive: `List<int>` ❌ (folosește `List<Integer>`).
4.  **Nu** poți folosi `instanceof List<String>` (doar `instanceof List<?>`).
5.  **Invarianță:** `List<Object>` **NU** este părintele lui `List<String>`.
    * Array-urile sunt covariante (`Object[]` = `String[]`), dar generics sunt invarianți.

---

## 5. Glosar Generics
* **T** (Type), **E** (Element), **K** (Key), **V** (Value).
* **Raw Type:** `List l = new ArrayList();` (De evitat!).
* **Reified:** Tipuri care există la runtime (Arrays). Generics sunt **Non-reified**.