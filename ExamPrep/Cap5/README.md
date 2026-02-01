# 🪆 Laborator 5: Clase Interne și Strings

## 1. Clase Interne (Nested Classes)
Clase definite în interiorul altei clase pentru a grupa logic entități strâns legate.

### A. Tipuri de Clase Interne
1.  **Clase Interne Normale (Non-static Inner Classes):**
    * Au acces la membrii instanței clasei exterioare (chiar și `private`).
    * **Instanțiere:** Necesită o instanță a clasei exterioare.
        ```java
        Outer outer = new Outer();
        Outer.Inner inner = outer.new Inner();
        ```
    * Acces la `this` exterior: `OuterClassName.this`.

2.  **Clase Interne Statice (Static Nested Classes):**
    * Se comportă ca o clasă normală, doar că sunt "cuibărite" în alta.
    * **NU** au acces la membrii non-statici ai clasei exterioare.
    * **Instanțiere:** Nu necesită instanță exterioară.
        ```java
        Outer.StaticInner inner = new Outer.StaticInner();
        ```

3.  **Clase Anonime (Anonymous Inner Classes):**
    * Clase fără nume, definite și instanțiate pe loc.
    * Folosite pentru implementări rapide de interfețe/clase abstracte (ex: Event Listeners).
    * **Limitări:** Nu au constructori. Pot accesa variabile locale doar dacă sunt `final` sau *effectively final*.
    * **Lambda:** `() -> {}` (înlocuiește clasele anonime pentru interfețe funcționale).

4.  **Clase Locale (Local Inner Classes):**
    * Definite în interiorul unei metode. Vizibile doar acolo.

## 2. Strings (Șiruri de Caractere) 🧶
`String` este un obiect imutabil în Java.

### A. Creare și Memorie
* **Literal:** `String s = "Java";` -> Stocat în **String Pool** (Heap). Refolosește obiectele identice (memorie eficientă).
* **Constructor:** `String s = new String("Java");` -> Creează forțat un obiect **NOU** în Heap (ineficient).

### B. Imutabilitate
* Odată creat, conținutul unui `String` **NU** se poate schimba.
* Metodele care par să modifice (`concat`, `toUpperCase`) returnează de fapt un **nou** obiect.
    ```java
    String s = "a";
    s.concat("b"); // s rămâne "a"
    s = s.concat("b"); // s devine "ab" (referință nouă)
    ```

### C. Comparare
* `==` : Compară **referințele** (adresele de memorie).
    * `"A" == "A"` -> `true` (același obiect din Pool).
    * `new String("A") == "A"` -> `false`.
* `.equals()` : Compară **conținutul** (textul). **Folosiți întotdeauna `.equals()`!**

### D. Performanță: StringBuilder
* Pentru concatenări repetate (ex: în bucle), `String` e lent (creează mii de obiecte temporare).
* **Soluție:** Folosiți `StringBuilder` (mutabil).
    * `sb.append("x")` modifică buffer-ul intern, fără a crea obiecte noi.

### E. Utilitare
* `String.valueOf(x)`: Convertește orice în String (safe pentru null).
* `Integer.parseInt("123")`: String -> int.
* `split(regex)`: Sparge textul în tokeni.
* `regex`: Expresii regulate (`\\d+` cifre, `\\s` spații).