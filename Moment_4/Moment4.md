# Moment 4 – Generiska klasser & felhantering

I detta moment kommer du att lära dig två kraftfulla verktyg inom programmering:

- **Generiska klasser och metoder** – så att du kan skriva kod som fungerar med olika datatyper.
- **Felhantering (exception handling)** – så att ditt program inte kraschar när något går fel.

---

## 🧰 Vad är generiska klasser och metoder?

Ibland vill vi skapa kod som kan användas med **flera olika datatyper**. Istället för att skriva om samma klass/metod flera gånger, kan vi använda **generics**.

### Exempel: generisk klass

```csharp
public class Box<T>
{
    public T Innehåll { get; set; }

    public void Visa()
    {
        Console.WriteLine($"Boxen innehåller: {Innehåll}");
    }
}
```

Här är `T` en platshållare för en datatyp. När du skapar objekt av klassen kan du specificera vilken typ den ska hantera:

```csharp
Box<string> box1 = new Box<string>();
box1.Innehåll = "Hej";

Box<int> box2 = new Box<int>();
box2.Innehåll = 42;
```

Detta är användbart om man t.ex. vill ha en lista, lagring eller wrapper som kan fungera för olika saker.

---

## 💥 Vad är undantag och felhantering?

När något oväntat händer i programmet – som att användaren skriver text istället för ett tal – kan det orsaka ett **undantag (exception)** och krascha programmet.

För att hantera detta använder vi `try` / `catch`:

```csharp
try
{
    Console.Write("Ange ett tal: ");
    int tal = Convert.ToInt32(Console.ReadLine());
    Console.WriteLine("Du skrev: " + tal);
}
catch (FormatException)
{
    Console.WriteLine("Fel: Du måste skriva ett heltal!");
}
```

### Fler exempel på vanliga undantag:
- `FormatException` – när konvertering misslyckas
- `IndexOutOfRangeException` – om du försöker nå ett element utanför listans gräns
- `NullReferenceException` – när du försöker använda ett objekt som är null

---

## 🛠️ Praktisk övning

Vi ska nu lägga till **felhantering** till vårt katalogsystem, och skapa en **generisk klass** som kan hantera produkter.

### 1. Lägg till felhantering i `Program.cs`

Skydda inmatningen från användaren med `try` / `catch`:

```csharp
bool kör = true;

while (kör)
{
    try
    {
        Console.Write("Ange produktnamn (eller 'stopp'): ");
        string namn = Console.ReadLine();
        if (namn.ToLower() == "stopp")
        {
            kör = false;
            continue;
        }

        Console.Write("Ange pris: ");
        double pris = Convert.ToDouble(Console.ReadLine());

        produkter.Add(new Produkt(namn, pris));
    }
    catch (FormatException)
    {
        Console.WriteLine("Fel: Du måste skriva ett giltigt pris (t.ex. 199,50).");
    }
}
```

---

### 2. Skapa en enkel generisk klass

**ProduktLåda.cs**
```csharp
public class ProduktLåda<T>
{
    public T Innehåll { get; set; }

    public void VisaInfo()
    {
        Console.WriteLine("Lådan innehåller:");
        Console.WriteLine(Innehåll.ToString());
    }
}
```

Använd den i `Main()`:

```csharp
ProduktLåda<Produkt> låda = new ProduktLåda<Produkt>();
låda.Innehåll = new Produkt("USB-laddare", 99);
låda.VisaInfo();
```

---

## ✅ Sammanfattning

Du har nu lärt dig:
- Vad generics är och hur de används för återanvändbar kod
- Hur man skapar en generisk klass
- Hur man hanterar fel med try/catch
- Hur man gör sitt program säkrare mot användarfel