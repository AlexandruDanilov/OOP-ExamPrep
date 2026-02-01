# 🌀 Laborator 4: Abstractizare, Clase Speciale și Restricții

## 1. Abstractizare
Principiu POO care ascunde detaliile de implementare și expune doar funcționalitatea esențială.

### A. Metode Abstracte
* Se declară cu `abstract`.
* **NU** au corp (implementare), ci doar semnătură (terminată cu `;`).
* Pot exista **doar** în clase abstracte sau interfețe.
* *Scop:* Forțează subclasele să ofere propria implementare.

### B. Clase Abstracte
* Se declară cu `abstract class`.
* **NU** pot fi instanțiate (`new Vehicul()` ❌).
* Pot conține:
    * Metode abstracte.
    * Metode concrete (cu cod).
    * Câmpuri (variabile de instanță).
    * Constructori (apelați de copii prin `super()` pentru inițializare).
* *Utilizare:* Când clasele au mult cod comun (IS-A relationship), dar unele comportamente diferă.

## 2. Interfețe
Definesc un **contract** ("Ce știe să facă", nu "Ce este").
* Se declară cu `interface`.
* **NU** pot avea constructori sau stare (variabile de instanță).
* **Membri impliciți:**
    * Metodele sunt `public abstract` (până la Java 8).
    * Variabilele sunt `public static final` (constante).
* **Moștenire:**
    * O clasă poate implementa **multiple** interfețe (`implements A, B`).
    * O interfață poate extinde alte interfețe (`extends X, Y`).

### Noutăți Java 8+ în Interfețe
1.  **Metode `default`:** Au implementare (corp) în interfață.
    * *Scop:* Compatibilitate (adăugarea unei metode noi fără a "strica" clasele existente).
2.  **Metode `static`:** Metode utilitare legate de interfață.

### ⚔️ Clasă Abstractă vs Interfață
| Caracteristică | Clasă Abstractă | Interfață |
| :--- | :--- | :--- |
| **Relație** | **IS-A** (Tip de...) | **CAN-DO** (Abilitate/Contract) |
| **Moștenire** | Simplă (`extends`) | Multiplă (`implements`) |
| **Constructor** | Da | Nu |
| **Variabile** | Orice tip | Doar constante (`static final`) |

## 3. Clase Speciale & Imutabilitate

### A. Obiecte Imutabile (Immutable)
* Starea lor **NU** se poate modifica după creare.
* *Exemple:* `String`, `LocalDate`, clasele Wrapper (`Integer`).
* **Rețeta:** Clasă `final`, câmpuri `private final`, fără setteri, constructor care setează tot.
* *Avantaj:* Thread-safe, bune pentru chei în HashMap.

### B. Enums (Enumerări)
* Set fix de constante numite (`enum Direction { NORTH, SOUTH }`).
* Sunt clase reale: pot avea constructori (privați!), metode și câmpuri.
* Metode utile: `values()` (array cu toate), `valueOf("NAME")`, `ordinal()`.

### C. Records (Java 16+)
* `public record User(String name, int age) {}`
* Creează automat o clasă **imutabilă** și **finală**.
* Generează automat:
    * Constructor (canonical).
    * `equals()`, `hashCode()`, `toString()`.
    * Getteri (fără prefixul `get`, ex: `user.name()`).
* *Utilizare:* Ideale pentru **DTO** (Data Transfer Objects) - cărăuși de date fără logică.

## 4. Capcane (Exam Tips) ⚠️
1.  **Problema Diamantului:** Dacă implementezi două interfețe cu aceeași metodă `default`, ești **obligat** să suprascrii metoda în clasă pentru a rezolva conflictul (`A.super.metoda()`).
2.  **Variabile în Interfețe:** Dacă scrii `int x = 5;` într-o interfață, este automat `public static final`. Nu o poți modifica.
3.  **Records:** Nu pot extinde alte clase (deja extind `Record`), dar pot implementa interfețe.