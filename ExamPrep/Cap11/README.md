# 🔧 Laborator 11: Programare Funcțională, Lambdas și Stream-uri

## 1. Programare Funcțională în Java
Stil de programare declarativ (spui *ce* vrei, nu *cum* se face pas cu pas), bazat pe funcții pure și imutabilitate.

### A. Interfețe Funcționale
O interfață cu **exact o metodă abstractă** (poate avea oricâte metode `default` sau `static`).
* Adnotare: `@FunctionalInterface` (opțională, dar recomandată).
* *Exemplu:* `Runnable`, `Comparator`, `ActionListener`.

### B. Lambda Expressions
Implementare inline a unei interfețe funcționale (o funcție anonimă).
* **Sintaxă:** `(parametri) -> { corp }`
* *Exemplu:* `(a, b) -> a + b` este o implementare pentru `int apply(int x, int y)`.
* **Restricții:** Variabilele locale folosite în lambda trebuie să fie **final** sau **effectively final** (să nu li se schimbe valoarea).

## 2. Interfețe Funcționale Standard (`java.util.function`)
Java oferă deja interfețe pentru cele mai comune scenarii:

| Interfață | Metodă | Primește | Returnează | Scop | Ex. Lambda |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`Predicate<T>`** | `test(T t)` | `T` | `boolean` | Filtrare, condiții | `x -> x > 0` |
| **`Function<T,R>`** | `apply(T t)` | `T` | `R` | Transformare (mapare) | `s -> s.length()` |
| **`Consumer<T>`** | `accept(T t)` | `T` | `void` | Acțiune (print, log) | `s -> sout(s)` |
| **`Supplier<T>`** | `get()` | - | `T` | Furnizare valori | `() -> Math.random()` |

* **Method References (`::`):** Scurtătură pentru lambda.
    * `s -> System.out.println(s)` devine `System.out::println`.

## 3. Stream API (`java.util.stream`) 🌊
O secvență de elemente care suportă operații de agregare secvențiale sau paralele.
**Stream-ul NU este o colecție!** Nu stochează date, doar le procesează.

### Pipeline-ul unui Stream
1.  **Sursă:** `list.stream()`, `Arrays.stream()`.
2.  **Operații Intermediare (Lazy):** Nu se execută imediat, doar configurează pipeline-ul. Returnează tot un `Stream`.
    * `filter(Predicate)`: Păstrează elementele care trec testul.
    * `map(Function)`: Transformă fiecare element.
    * `distinct()`, `sorted()`, `limit()`.
3.  **Operație Terminală (Eager):** Declanșează procesarea și produce rezultatul. Stream-ul se închide.
    * `forEach(Consumer)`: Iterează.
    * `collect(Collectors.toList())`: Adună rezultatele.
    * `count()`, `reduce()`, `findFirst()`.

### Reguli de Aur
1.  Un Stream **nu poate fi refolosit** după ce a fost închis (după operația terminală).
2.  Operațiile intermediare sunt **Lazy** (dacă nu ai terminală, nu se execută nimic).
3.  **Fără side-effects:** Nu modificați variabile externe din lambda (decât dacă sunt atomice/thread-safe).

## 4. Optional (`java.util.Optional`)
Un container pentru o valoare care poate fi `null`. Evită `NullPointerException`.
* **Creare:** `Optional.of(val)` (nu null), `Optional.ofNullable(val)` (poate fi null), `Optional.empty()`.
* **Utilizare:**
    * `.isPresent()`: Verificare (stil vechi).
    * `.ifPresent(Consumer)`: Execută doar dacă există valoare.
    * `.orElse(defaultVal)`: Returnează valoarea sau un default.
    * `.orElseThrow()`: Aruncă excepție dacă e gol.