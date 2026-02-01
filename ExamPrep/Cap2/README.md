# 🧱 Laborator 2: Clase, Obiecte și Memorie

## 1. Concepte Fundamentale
* **Clasa:** Este "schița" (blueprint-ul). Definește structura (câmpuri) și comportamentul (metode).
* **Obiectul:** Este **instanța** clasei (casa construită după schiță). Există fizic în memorie.
* **Referința:** Variabila care ține adresa obiectului.
    * `Student s;` -> Declarare referință (valoare `null`, nu există obiect).
    * `s = new Student();` -> Instanțiere (Alocare memorie + Inițializare).

## 2. Membrii Clasei
### A. Câmpuri (Starea)
* Variabile declarate în interiorul clasei.
* **Valori implicite:** Dacă nu le inițializezi, JVM le dă valori default:
    * Numeric: `0`
    * Boolean: `false`
    * Obiecte: `null`
* **Shadowing:** Când un parametru are același nume cu un câmp (`x`). Se rezolvă cu `this.x`.

### B. Metode (Comportamentul)
* **Supraîncărcare (Overloading):** Mai multe metode cu **același nume** dar **parametri diferiți** (tip sau număr).
    * *Nota:* Tipul returnat NU contează pentru overloading.
* **Pass-by-value:** Java trimite parametrii prin copiere.
    * La obiecte, se copiază **valoarea referinței** (adresa).
    * Dacă modifici câmpurile obiectului în metodă -> se vede și afară.
    * Dacă reasignezi referința (`s = new Student()`) în metodă -> NU se vede afară.

### C. Constructori
* Metode speciale apelate la `new`.
* **Reguli:** Au același nume cu clasa și **NU** au tip returnat (nici `void`).
* **Constructor Default:** Dacă nu scrii niciun constructor, Java îți dă unul gol (`Student() {}`).
    * **Atenție:** Dacă scrii tu un constructor cu parametri, cel default dispare!
* **Copy Constructor:** Primește un obiect de același tip pentru a copia valorile.
* **Constructor Chaining:** `this(...)` apelează alt constructor din aceeași clasă. Trebuie să fie **prima instrucțiune**.

## 3. 💾 Gestionarea Memoriei
### Stack (Stiva)
* Memorie rapidă, temporară.
* Aici stau: variabilele locale (primitive) și **referințele** către obiecte.

### Heap (Grămada)
* Memorie dinamică, gestionată de **Garbage Collector (GC)**.
* Aici stau **Obiectele** propriu-zise (tot ce e creat cu `new`).
* **GC:** Șterge automat obiectele la care nu mai există nicio referință activă.

## 4. 🪨 Keyword-ul `static`
Membrii statici aparțin **Clasei**, nu instanțelor.
* **Câmpuri statice:** O singură copie în memorie, partajată de toate obiectele (ex: `Apple.gravAcc`).
* **Metode statice:**
    * Se apelează prin `NumeClasa.metoda()`.
    * **NU** pot accesa `this` sau membri non-statici.
* **Blocuri statice:** `static { ... }`. Se execută o singură dată, la încărcarea clasei în memorie (înainte de orice constructor).

## 5. Încapsulare
Ascunderea detaliilor interne.
* **Access Modifiers:**
    * `private`: Vizibil doar în clasă.
    * `default` (lipsă): Vizibil doar în pachet.
    * `protected`: Pachet + Subclase.
    * `public`: Vizibil oriunde.
* **Getter/Setter:** Metode publice pentru a controla accesul la câmpuri private.

## 6. Tips & Tricks (Capcane)
1.  **String:** E obiect imuabil. Inițializare preferată: `String s = "Text";`.
2.  **`this`:**
    * `this.x`: acces câmp.
    * `metoda(this)`: pasare referință curentă.
    * `this()`: apel constructor (doar prima linie).