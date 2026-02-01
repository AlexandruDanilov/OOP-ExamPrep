# 💥 Laborator 7: I/O și Gestionarea Excepțiilor

## 1. Excepții
Mecanism de tratare a erorilor care separă logica programului de gestionarea cazurilor excepționale.

### A. Mecanismul de bază
* **Aruncarea (`throw`):** Semnalarea unei erori.
* **Prinderea (`catch`):** Tratarea erorii.
* **Structura:**
    ```java
    try {
        // Cod care poate genera erori
    } catch (TipExceptie e) {
        // Tratare
    } finally {
        // Se execută MEREU (pentru cleanup)
    }
    ```
* **Multi-catch (Java 7+):** `catch (IOException | SQLException e) { ... }`

### B. Ierarhia Throwable
1.  **Checked Exceptions (`Exception`):**
    * Erori anticipabile (fișier lipsă, rețea).
    * **Obligatoriu** de tratat (`try-catch` sau `throws`).
2.  **Unchecked Exceptions (`RuntimeException`):**
    * Bug-uri de programare (null pointer, index out of bounds).
    * **Opțional** de tratat.
3.  **Errors (`Error`):**
    * Probleme grave de sistem (Out of Memory). Nu se prind.

### C. Reguli Speciale
* **Propagare:** Dacă o metodă nu prinde excepția, ea urcă pe stivă la metoda apelantă.
* **Moștenire:** O metodă suprascrisă NU poate arunca excepții checked noi sau mai generale decât părintele.
* **Try-with-resources:** Închide automat resursele (`AutoCloseable`).
    ```java
    try (BufferedReader br = new BufferedReader(new FileReader("fisier.txt"))) { ... }
    ```

---

## 2. File I/O (Input/Output)
Java folosește stream-uri pentru a manipula date.

### A. Modalități de Citire
1.  **`Scanner`:**
    * Bun pentru citire de tokeni (cuvinte, numere).
    * Metode: `nextInt()`, `nextDouble()`.
    * *Dezavantaj:* Mai lent pentru fișiere mari (face parsing).
2.  **`FileReader`:**
    * Citește fișiere text caracter cu caracter.
    * Simplu, dar ineficient fără buffer.
3.  **`InputStreamReader`:**
    * Adaptor: Transformă `InputStream` (bytes) în `Reader` (caractere).
    * Permite specificarea encoding-ului (UTF-8).
4.  **`BufferedReader`:**
    * Cel mai eficient pentru text.
    * Citește blocuri mari în memorie.
    * Metoda `readLine()` citește linie cu linie.

### B. Modalități de Scriere
1.  **`PrintWriter`:**
    * Scriere formatată (`printf`, `println`).
    * Ușor de folosit ("user-friendly").
2.  **`FileWriter`:**
    * Scrie caractere direct în fișier.
    * Suprascrie fișierul dacă nu folosim `append = true`.
3.  **`OutputStreamWriter`:**
    * Adaptor: Caractere -> Bytes.
    * Permite controlul encoding-ului la scriere.
4.  **`BufferedWriter`:**
    * Scriere eficientă (folosește buffer).
    * Metoda `newLine()` adaugă separatorul de linie specific OS-ului.

### C. Concepte Avansate
* **Byte Streams (`FileInputStream`/`FileOutputStream`):** Pentru date binare (imagini, audio).
* **Clasa `File`:** Reprezintă calea și meta-datele (nume, drepturi, existență), NU conținutul.
* **`RandomAccessFile`:** Permite citirea/scrierea la o poziție arbitrară (`seek(pos)`).