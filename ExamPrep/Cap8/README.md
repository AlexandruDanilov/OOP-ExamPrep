# 🏗️ Laborator 8: Design Patterns I

Design Pattern-urile sunt soluții reutilizabile pentru probleme comune de arhitectură software. Se împart în:
1.  **Creational:** Crearea obiectelor (Singleton, Factory).
2.  **Structural:** Structura claselor (Proxy).
3.  **Behavioral:** Comunicarea între obiecte (Visitor).

---

## 1. Singleton (Creational) 🔒
Asigură că o clasă are **o singură instanță** și oferă un punct global de acces la ea.

### Implementare
1.  **Constructor privat** (blochează `new` din exterior).
2.  **Instanță statică** (unică, stocată intern).
3.  **Metodă statică publică** (`getInstance`) care returnează instanța.

```java
// Varianta cea mai sigură (Thread-safe, Serialization-safe)
public enum Singleton {
    INSTANCE;
    public void doSomething() { System.out.println("Working..."); }
}

// Varianta Clasică (Lazy Initialization - nerecomandată fără sincronizare în multithreading)
public class Config {
    private static Config instance;
    private Config() {} // Constructor privat
    
    public static Config getInstance() {
        if (instance == null) {
            instance = new Config(); // Creat doar la prima utilizare
        }
        return instance;
    }
}
```

* **Utilizare:** Logger, Configurare, Conexiuni Baze de Date.
* **De ce e Anti-Pattern?** Introduce stare globală ascunsă, creează cuplaj strâns (tight coupling) și face **testarea unitară dificilă** (greu de înlocuit cu mock-uri).
* **Alternativa:** Dependency Injection (Agregare).

---

## 2. Factory Patterns (Creational) 🏭

### A. Factory Method
Definește o interfață pentru crearea unui obiect, dar lasă subclasele să decidă clasa exactă instanțiată.
* **Problemă:** Codul client nu trebuie să depindă de clasele concrete (`Truck`, `Ship`) și de keyword-ul `new`.
* **Soluție:** `Transport t = logistics.createTransport();`
* **Avantaj:** Respectă Open/Closed Principle (putem adăuga tipuri noi de transport fără a modifica logica clientului).

### B. Abstract Factory
Creează **familii** de obiecte relaționate (compatibile) fără a specifica clasele concrete.
* **Exemplu:** `GUIFactory` care produce `Button` și `Checkbox`.
    * `WindowsFactory` -> produce `WindowsButton` + `WindowsCheckbox`.
    * `MacFactory` -> produce `MacButton` + `MacCheckbox`.
* **Diferență:**
    * *Factory Method:* Creează un singur produs.
    * *Abstract Factory:* Creează o familie de produse care trebuie să funcționeze împreună.

---

## 3. Visitor (Behavioral) 🚶‍♂️
Permite adăugarea de operații noi pe o structură de obiecte existentă (ierarhie de clase) fără a modifica clasele respective.

### Problema: Double Dispatch
În Java, supraîncărcarea (Overloading) este statică (decisă la compilare).
```java
void export(Node n) { ... }
void export(City c) { ... }
...
Node n = new City();
exporter.export(n); // Apelează export(Node), NU export(City)!
```

### Soluția Visitor
Folosește **Double Dispatch** pentru a determina metoda corectă la runtime.
1.  **Visitable (Element):** Are metoda `accept(Visitor v)`.
    * Implementare: `v.visit(this);` -> Aici `this` este tipul concret (`City`), deci se leagă corect.
2.  **Visitor:** Are metode `visit(City)`, `visit(Industry)`.

* **Utilizare:** Export (XML/JSON), Raportare, Validare pe structuri complexe.

---

## 4. Proxy (Structural) 🛡️
Un intermediar care controlează accesul la un obiect original.
* **Virtual Proxy (Lazy Loading):** Încarcă obiectul real (costisitor) doar când e nevoie. Ex: încărcarea unei imagini mari doar când apare pe ecran.
* **Protection Proxy:** Verifică drepturile de acces înainte de a delega cererea.
* **Remote Proxy:** Reprezentare locală a unui obiect aflat pe alt server.