
# 📝 Uppgift: Filhantering och Kodstandard

## 🔹 Del 1 – Skapa och hantera filer
1️⃣ Skapa en textfil som heter `minData.txt` och skriv in följande rader:
```
Första raden text
Andra raden text
```

2️⃣ Skriv ett C#-program som gör följande:
- Läser in och visar hela innehållet från `minData.txt`.
- Lägger till en ny rad i filen, t.ex. `Tredje raden tillagd av programmet`.
- Visar filens innehåll igen så att det syns att den nya raden lagts till.

👉 **Tips:** Använd `File.Exists()`, `File.ReadAllText()` och `File.AppendAllText()`.

---

## 🔹 Del 2 – Förbättra kodstandard
Här är en kodsnutt med dålig standard:

```csharp
class bil{
public string marke;
public bil(string m){
marke=m;}
}
```

💡 **Din uppgift:** Skriv om koden så att den följer god kodstandard enligt det ni lärt er.

---

## 🔹 Extra reflektionsfråga (frivillig)
- Vad händer om du försöker läsa en fil som inte finns? Hur kan du hantera det?
