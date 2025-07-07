
# Filer och Kodstandard

## 📌 Vad är en fil?
En **fil** är en enhet där vi kan lagra data på en dator eller annan enhet.  
En fil kan innehålla text, siffror, bilder, ljud eller annan information.  
Filer ligger sparade på hårddiskar, USB-minnen, eller i molnet och kan öppnas av program.  

### Exempel på filtyper:
- **Textfiler** (t.ex. `.txt`, `.csv`, `.json`) → innehåller bara text, kan läsas i texteditor.
- **Binära filer** (t.ex. `.jpg`, `.exe`, `.mp3`) → innehåller data som datorn förstår, men inte alltid människa direkt.

## 📌 Varför jobbar vi med filer i programmering?
Vi använder filer när vi vill:
- **Spara data**: Exempelvis spara poäng i ett spel så att de finns kvar nästa gång vi startar spelet.
- **Läsa in data**: Exempelvis läsa en lista med elever från en fil när ett program startar.
- **Dela data**: Program kan läsa och skriva filer för att utbyta information med andra program.

## ✍️ Exempel: Läsa från en textfil i C#
Detta exempel visar hur man kontrollerar att filen finns och läser in innehållet.

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string path = "minfil.txt";

        if (File.Exists(path))
        {
            string innehall = File.ReadAllText(path);
            Console.WriteLine("Filens innehåll:");
            Console.WriteLine(innehall);
        }
        else
        {
            Console.WriteLine("Filen finns inte.");
        }
    }
}
```

📝 **Förklaring:**  
- Vi skapar en variabel `path` som har filnamnet.
- Vi kollar om filen finns med `File.Exists(path)`.
- Om filen finns läser vi allt innehåll med `File.ReadAllText(path)` och skriver ut det.
- Om filen inte finns visar vi ett meddelande.

## ✍️ Exempel: Skriva till en textfil i C#
Så här kan vi spara text i en fil.

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string path = "utdata.txt";
        string text = "Hej från programmet!";

        File.WriteAllText(path, text);

        Console.WriteLine("Texten skrevs till filen.");
    }
}
```

📝 **Förklaring:**  
- `File.WriteAllText(path, text)` skriver texten till filen. Om filen inte finns skapas den.  
- Om filen redan finns skrivs den över.

## ⚠️ Vanliga fel
När vi arbetar med filer kan vi stöta på problem:
- **Filen finns inte:** Programmet försöker läsa något som inte finns.
- **Fel sökväg:** T.ex. filen ligger i en annan mapp än vi trodde.
- **Filen används av ett annat program:** T.ex. filen är öppen i ett annat program (som Notepad).

👉 **Tips:** Använd alltid `File.Exists()` för att kolla om filen finns innan du försöker läsa den.

## ✅ Vad är kodstandard?
Kodstandard är **regler för hur vi skriver vår kod**.  
Det gör att koden blir:
- Lättare att läsa och förstå.
- Enklare att felsöka.
- Lättare att arbeta med när flera personer jobbar med samma kod.

## 🎨 Exempel på kodstandarder

### 📌 Namngivning
- **Variabler:** små bokstäver + camelCase (första ordet litet, sedan stor bokstav på nya ord)  
  Exempel: `antalElever`, `förnamn`
- **Metoder:** PascalCase (alla ord börjar med stor bokstav)  
  Exempel: `BeräknaMedelvärde()`, `LäsFil()`
- **Klasser:** PascalCase  
  Exempel: `Elev`, `Filhanterare`

### 📌 Indentering
Indentering betyder att vi gör kodens struktur tydlig genom att flytta in kod som hör ihop.

❌ Dålig kod:
```csharp
if (x > 0){
Console.WriteLine("Positivt");
}
```

✅ Bra kod:
```csharp
if (x > 0)
{
    Console.WriteLine("Positivt");
}
```

### 📌 Kommentarer
Kommentarer används för att förklara varför koden gör något – inte vad den gör om det redan är tydligt.

```csharp
// Läser in filens innehåll så att vi kan visa det för användaren
string innehall = File.ReadAllText("minfil.txt");
```

## 🏁 Övningar

### Del 1 – Filhantering
1️⃣ Skapa en textfil som heter `testfil.txt`. Skriv några rader text i den.  
2️⃣ Skriv ett program som:
- Läser filen och visar innehållet i konsolen.
- Lägger till en ny rad i filen utan att ta bort det gamla.

👉 Tips: Använd `File.AppendAllText()` för att lägga till text.

### Del 2 – Förbättra kodstandard
Här är en kodsnutt med dålig standard:

```csharp
class elev{
public string namn;
public elev(string n){
namn=n;}
}
```

🔹 Uppgift: Skriv om koden så den följer kodstandard.

<details>
<summary>Lösning</summary>

```csharp
class Elev
{
    public string Namn;

    public Elev(string namn)
    {
        Namn = namn;
    }
}
```
</details>

## 💬 Tips
- Skriv alltid kod som om någon annan ska läsa den.
- Följ kodstandard även på små uppgifter – det blir en bra vana.
- Kontrollera alltid om filer finns innan du försöker läsa dem.

## ❓ Reflektionsfrågor
- Vad händer om filen inte finns när programmet körs?
- Hur kan en bra kodstandard hjälpa dig när du jobbar med större projekt?
- Hur skulle din egen kod se ut om du läste den om ett år?
