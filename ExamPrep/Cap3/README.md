# 🏛️ Laborator 3: Design Avansat de Clase

## 1. Relații între Obiecte (Has-A)
Diferența fundamentală dintre Agregare și Compunere este dată de **ciclul de viață** al obiectelor.

### A. Agregare (Weak Has-A)
* **Definiție:** Obiectul "copil" poate exista independent de "părinte".
* **Instanțiere:** Obiectul este creat în exterior și pasat prin constructor.
* **Exemplu:** `Department` are `Employee[]`. Dacă ștergi departamentul, angajații nu dispar (doar devin șomeri).
* **Indiciu vizual:** Obiectul vine prin parametru în constructor.

### B. Compunere (Strong Has-A)
* **Definiție:** Obiectul "copil" este creat și gestionat exclusiv de "părinte".
* **Dependență:** Dacă părintele este distrus, și copilul este distrus.
* **Exemplu:** `House` are `Room[]`. Dacă demolezi casa, dispar camerele.
* **Indiciu vizual:** Operatorul `new` apare în interiorul clasei container.

## 2. Moștenire (Is-A)
Mecanismul prin care o clasă preia funcționalitatea altei clase (`extends`).
* **Regulă:** Java permite doar **moștenire simplă** (o singură clasă părinte).
* **Constructorii:** NU se moștenesc!
    * Ordinea inițializării: `Părinte` -> `Copil`.
    * **`super()`**: Apelează constructorul părintelui. **Trebuie să fie prima instrucțiune** în constructorul copilului.
* **Modificatori:**
    * `protected`: Accesibil în același pachet + subclase (chiar dacă subclasa e în alt pachet).
* **Clase `final`:** Nu pot fi moștenite (ex: `String`, `Math`).

## 3. Polimorfism
Abilitatea unui obiect de a fi tratat ca o instanță a clasei părinte.

### A. Upcasting (Implicit & Sigur)
* Conversia de la Copil la Părinte.
* `Animal a = new Dog();`
* Acces doar la metodele din `Animal`, dar execuția va fi cea din `Dog` (dacă e suprascrisă).

### B. Downcasting (Explicit & Riscant)
* Conversia de la Părinte la Copil.
* Necesită verificare cu `instanceof` pentru a evita `ClassCastException`.
* `if (a instanceof Dog) { ((Dog)a).bark(); }`

### C. Tipuri de Polimorfism
1.  **Static (Overloading):** Același nume, parametri diferiți (rezolvat la compilare).
2.  **Dinamic (Overriding):** Aceeași semnătură, implementare diferită în copil (rezolvat la rulare).
    * **Restrictii:** Nu poți suprascrie metode `static` (doar le ascunzi - Method Hiding) sau `final`.
    * **Acces:** Metoda din copil nu poate avea acces mai restrictiv decât cea din părinte.

## 4. Metode din clasa `Object`
Toate clasele moștenesc automat `Object`.
* **`toString()`**: Returnează reprezentarea text. Default este adresa de memorie (`Clasa@Hash`). Trebuie suprascrisă pentru date utile.
* **`equals(Object o)`**: Compară egalitatea logică.
    * `==` compară referințele (adresele).
    * `equals` trebuie suprascrisă pentru a compara conținutul (ex: ID, nume).

## 5. 🧠 Memorie & VTables (Advanced)
* **Metaspace:** Zonă de memorie unde JVM ține structura claselor.
* **VTable (Virtual Method Table):**
    * Tabel folosit de JVM la **runtime** pentru a decide ce metodă suprascrisă să apeleze (Dynamic Dispatch).
    * [Image of Java VTable structure]
    * *Notă:* Metodele **statice** NU sunt în VTable (deci nu au polimorfism dinamic).