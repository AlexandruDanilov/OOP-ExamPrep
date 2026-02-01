# 📦 Laborator 6: Colecții, Tipuri Speciale și Utilitare

## 1. Clase Wrapper
Java separă tipurile **Primitive** (performante, dar simple) de **Obiecte** (funcționalități extra, dar costisitoare). Wrappers fac legătura.

* **Primitive:** `int`, `double`, `boolean`, `char`.
* **Wrappers:** `Integer`, `Double`, `Boolean`, `Character`.
* **Autoboxing:** Conversie automată Primitivă → Obiect (`Integer a = 10;`).
* **Unboxing:** Conversie automată Obiect → Primitivă (`int b = a;`).
* **Capcană:** Compararea cu `==` la Wrappers compară referințele, nu valorile!
    ```java
    Integer a = 1000, b = 1000;
    System.out.println(a == b); // false (obiecte diferite)
    System.out.println(a.equals(b)); // true (valori egale)
    ```
    *Notă:* Java cacheuiește Integerii mici (-128 la 127), deci acolo `==` poate returna `true`, dar nu te baza pe asta. 

## 2. Java Collections Framework (JCF)
Structuri de date dinamice. Ierarhia principală se împarte în `Collection` și `Map`. 

### A. List (Ordonat, Duplicate permise)
* **`ArrayList`:** Array dinamic.
    * Rapid la citire (`get` -> O(1)).
    * Lent la inserare/ștergere în mijloc (trebuie mutate elementele).
* **`LinkedList`:** Listă dublu înlănțuită.
    * Rapid la inserare/ștergere.
    * Lent la acces aleatoriu (`get` -> O(n)).

### B. Set (Unic, Fără duplicate)
* **`HashSet`:** Neordonat. Cel mai rapid (O(1)). Folosește `hashCode`.
* **`LinkedHashSet`:** Păstrează ordinea inserării.
* **`TreeSet`:** Sortează elementele (natural sau cu Comparator). O(log n).

### C. Queue (Cozi)
* **`PriorityQueue`:** Elementele ies în funcție de prioritate (sortate), nu FIFO.
* **`ArrayDeque`:** Coadă dublă, mai rapidă decât LinkedList pentru stive/cozi.

### D. Map (Cheie-Valoare) - NU extinde Collection
* **`HashMap`:** Rapid, neordonat. Permite o cheie `null`.
* **`LinkedHashMap`:** Păstrează ordinea inserării.
* **`TreeMap`:** Chei sortate. Nu permite chei `null`.

## 3. Comparare și Sortare
* **`Comparable<T>`:** "Ordinea naturală". Implementat **în clasa obiectului**.
    * Metoda: `compareTo(T o)`.
    * Ex: `Collections.sort(lista)` folosește asta.
* **`Comparator<T>`:** "Ordine custom". Implementat într-o **clasă separată** (sau lambda).
    * Metoda: `compare(T o1, T o2)`.
    * Ex: `lista.sort(new NameComparator())`.

## 4. Contractul Equals & HashCode ⚠️
Vital pentru `HashSet` și `HashMap`.
1.  Dacă `a.equals(b)` este true, atunci `a.hashCode() == b.hashCode()` **TREBUIE** să fie true.
2.  Dacă nu respecți asta, colecțiile hash vor "pierde" obiectele (le pun într-un bucket, dar le caută în altul).

## 5. Utilitare
### A. Math & Big Numbers
* `Math`: Metode statice (`sqrt`, `pow`, `random`).
* `BigInteger` / `BigDecimal`: Pentru numere uriașe sau precizie financiară absolută (evită erorile de virgulă mobilă ale `double`).

### B. Date și Timp (Java 8+)
Clase imutabile (thread-safe):
* `LocalDate`: Doar dată (2023-10-05).
* `LocalTime`: Doar oră (14:30).
* `LocalDateTime`: Dată + Oră.
* `ZonedDateTime`: Dată + Oră + Fus Orar.
* Formatare: `DateTimeFormatter`.