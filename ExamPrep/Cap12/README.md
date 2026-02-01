# 🚀 Laborator 12: Programare Avansată Java

## 1. Serializare (Serialization)
Procesul de transformare a unui obiect Java într-un flux de bytes (pentru salvare în fișier sau trimitere prin rețea).
* **Deserializare:** Procesul invers (Bytes -> Obiect).

### A. Serializarea Nativă
* Clasa trebuie să implementeze `java.io.Serializable` (interfață marker).
* `ObjectOutputStream.writeObject(obj)`: Serializare.
* `ObjectInputStream.readObject()`: Deserializare.
* **`transient`:** Cuvânt cheie pentru câmpuri care **NU** trebuie serializate (ex: parole).
* **`serialVersionUID`:** ID unic pentru versionarea clasei. Dacă clasa se schimbă, ID-ul previne deserializarea eronată.

### B. Serializarea JSON (cu Jackson)
Standardul modern. Nu folosește format binar, ci text (JSON).
* **Bibliotecă:** `com.fasterxml.jackson.core`.
* **Adnotări:**
    * `@JsonProperty("nume_json")`: Mapează un câmp Java la un nume JSON diferit.
    * `@JsonIgnore`: Exclude câmpul din JSON.
* **Utilizare:** `ObjectMapper mapper = new ObjectMapper(); mapper.writeValueAsString(obj);`.

## 2. Adnotări (Annotations)
Metadate adăugate codului (`@Nume`). Nu schimbă logica direct, dar sunt citite de compilator sau la runtime.
* **Definire:** `public @interface MyAnnotation { ... }`.
* **Meta-adnotări:**
    * `@Target`: Unde se aplică (FIELD, METHOD, TYPE).
    * `@Retention`: Cât trăiește (SOURCE, CLASS, RUNTIME). Pentru Reflection, trebuie `RUNTIME`.

## 3. Reflection 🪞
Mecanism prin care codul își inspectează propria structură la runtime.
* **Punct de intrare:** Clasa `Class<?>`.
    * `obj.getClass()` sau `ClassName.class`.
* **Capabilități:**
    * Aflarea metodelor, câmpurilor, constructorilor (`getDeclaredMethods()`).
    * Accesarea câmpurilor **private** (`field.setAccessible(true)`).
    * Instanțierea dinamică (`clazz.newInstance()`).
* **Utilizare:** Framework-uri (Spring, Hibernate, JUnit) pentru a injecta dependențe sau a rula teste fără a ști numele claselor la compilare.
* **Dezavantaje:** Lent, rupe încapsularea, erori doar la runtime.

## 4. Testare Automată (Unit Testing) 🧪
Verificarea izolată a unităților de cod (metode/clase).

### A. JUnit (Framework de testare)
* **`@Test`:** Marchează o metodă ca test.
* **Assertions:** `assertEquals(expected, actual)`, `assertTrue(cond)`, `assertThrows(Exception.class, () -> ... )`.
* **Lifecycle:** `@BeforeEach` (setup înainte de fiecare test), `@AfterEach` (cleanup).

### B. Mocking (cu Mockito)
Simularea dependențelor externe (baze de date, API-uri) pentru a testa în izolare.
* **`mock(Clasa.class)`:** Creează un obiect fals.
* **`when(mock.metoda()).thenReturn(valoare)`:** Definește comportamentul simulat.
* **`verify(mock).metoda()`:** Verifică dacă metoda a fost apelată.

### C. Assertions (Keyword `assert`)
* `assert conditie : "Mesaj";`
* Folosit pentru verificări interne (invarianți).
* Se activează cu `-ea` (Enable Assertions) la rulare. Nu înlocuiește Unit Testing-ul.