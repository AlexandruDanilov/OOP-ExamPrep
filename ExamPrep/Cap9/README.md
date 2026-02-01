# 🏗️ Laborator 9: Design Patterns II

## 1. Builder (Creational) 👷
Folosit pentru a construi obiecte complexe pas cu pas. Separă construcția de reprezentare.


### Problema (Telescoping Constructor)
Fără Builder, pentru un obiect cu mulți parametri opționali (ex: `Pizza`), am avea constructori gigantici și greu de citit:
`new Pizza("Large", "Thin", 1, 0, 1, 0, ...)` -> Ce înseamnă `1, 0`?

### Soluția Builder
O clasă statică internă `Builder` care are metode pentru fiecare parametru (returnând `this` pentru chaining).
```java
Pizza p = new Pizza.Builder("Large", "Thin") // Parametri obligatorii
            .cheeseCount(1)                  // Opțional
            .pepperoniCount(2)               // Opțional
            .build();                        // Construiește obiectul final
```
* **Avantaje:** Cod lizibil, imutabilitate (obiectul final nu are setteri), evită stările inconsistente.

---

## 2. Observer (Behavioral) 👀
Definește o relație de dependență **1-la-N** între obiecte. Când un obiect (Subject) își schimbă starea, toți dependenții (Observeri) sunt notificați automat.


### Structura
1.  **Subject (Publisher):** Ține lista de observatori (`add`, `remove`, `notify`).
2.  **Observer (Subscriber):** Interfață cu metoda `update()`.
3.  **ConcreteObserver:** Implementează reacția la notificare.

* **Exemplu:** Youtube Channel (Subject) -> Subscribers (Observers). Când apare un video nou, toți abonații primesc notificare.
* **Avantaj:** Decuplare totală. Subiectul nu știe cine sunt observatorii sau ce fac ei, doar îi anunță.

---

## 3. Strategy (Behavioral) 🎲
Permite definirea unei familii de algoritmi, încapsularea fiecăruia și interschimbarea lor la runtime.


### Structura
1.  **Context:** Clasa care folosește strategia (`ShoppingCart`).
2.  **Strategy Interface:** Interfața comună (`PaymentStrategy`).
3.  **Concrete Strategies:** Implementări specifice (`CardPayment`, `PayPalPayment`).

* **Exemplu:** `ShoppingCart` poate plăti cu Cardul sau PayPal. Putem schimba metoda de plată la runtime fără a modifica codul coșului.
* **Diferență vs Factory:** Factory creează obiecte, Strategy schimbă comportamentul (algoritmul) unui obiect existent.

---

## 4. Command (Behavioral) 🎮
Încapsulează o cerere (acțiune) ca un obiect. Permite parametrizarea clienților cu cereri, stocarea în coadă și operații de **Undo/Redo**.


### Structura
1.  **Command Interface:** `void execute()`, `void undo()`.
2.  **ConcreteCommand:** Leagă o acțiune de un Receiver (`LightOnCommand`).
3.  **Invoker:** Cel care declanșează comanda (Telecomanda / Butonul).
4.  **Receiver:** Cel care face munca efectivă (Becul / TV-ul).

* **Utilizare:** Editor text (Copy/Paste/Undo), Telecomandă universală, Job Queues.
* **Avantaj:** Decuplează cel care cere acțiunea (butonul) de cel care o execută (becul).

---

## 5. Comparații (Tips & Tricks)
* **Factory vs Builder:**
    * Factory: Creează obiectul "dintr-o bucată" (totul gata imediat).
    * Builder: Construiește obiectul pas cu pas (bun pentru configurații complexe).
* **Strategy vs State vs Command:**
    * **Strategy:** "Cum fac asta?" (Algoritm interschimbabil).
    * **Command:** "Când fac asta?" (Acțiune stocată pentru mai târziu/undo).