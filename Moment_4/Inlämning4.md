
# Inlämningsuppgift – Moment 4
## Uppgift

Skapa ett litet program där du:

Skapar en **generisk klass** som kan lagra olika typer av data i en lista.  
Använder **try / catch / finally** för att hantera fel när användaren matar in data.

---

## Steg-för-steg

1️⃣ Skapa en generisk klass `Storage<T>`  
- Klassen ska kunna lagra en lista med objekt av typen `T`.  
- Klassen ska ha metoder för att lägga till ett objekt och skriva ut alla objekt.

---

2️⃣ I `Main()`  
- Skapa ett objekt av `Storage<int>` och ett av `Storage<string>`.  
- Lägg till några värden i båda och skriv ut dem.

---

3️⃣ Fråga användaren efter ett heltal  
- Använd `try / catch / finally` för att hantera fel om användaren skriver in något som inte är ett heltal.  
- Visa ett felmeddelande om det blir fel.  
- Skriv `"Input attempt complete."` i `finally`.

---

## Mål
Förstå grunderna i generiska klasser.  
Öva på felhantering med try / catch / finally.
