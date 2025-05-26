# Moment 2 – Listor och samlingar

I detta moment lär du dig att hantera **flera objekt** med hjälp av listor i C#. Vi bygger vidare på vår produktklass och lär oss att lägga till, spara och visa flera produkter samtidigt.

---

## 🧠 Vad är en lista?

En lista (`List<T>`) är en samling som kan lagra flera objekt av samma typ. Du kan lägga till, ta bort och gå igenom objekt med loopar.

### Skapa en lista av produkter

```csharp
List<Produkt> produkter = new List<Produkt>();

produkter.Add(new Produkt("C# för nybörjare", 199));
produkter.Add(new Produkt("Programmering 2", 249));
```

---

## 🔁 Loopar: foreach och while

### foreach

Med `foreach` kan du gå igenom varje objekt i listan:

```csharp
foreach (Produkt p in produkter)
{
    p.VisaInfo();
}
```

### while

En `while`-loop upprepar kod så länge ett villkor är sant:

```csharp
int i = 0;
while (i < 5)
{
    Console.WriteLine(i);
    i++;
}
```

Vi använder `while` för att låta användaren mata in flera produkter.

---

## 🎯 Hjälpmetoder: ToLower och Convert.ToDouble

### ToLower()

För att jämföra strängar oavsett stora/små bokstäver:

```csharp
string svar = Console.ReadLine();
if (svar.ToLower() == "ja")
{
    Console.WriteLine("Du skrev ja!");
}
```

### Convert.ToDouble()

För att omvandla en textinmatning till ett tal:

```csharp
Console.Write("Ange pris: ");
double pris = Convert.ToDouble(Console.ReadLine());
```

---

## 🛠️ Praktisk övning

Följ dessa steg:

### 1. Återanvänd din `Produkt.cs`

**Produkt.cs**
```csharp
public class Produkt
{
    public string Namn { get; set; }
    public double Pris { get; set; }

    public Produkt(string namn, double pris)
    {
        Namn = namn;
        Pris = pris;
    }

    public void VisaInfo()
    {
        Console.WriteLine($"{Namn} - {Pris} kr");
    }
}
```

### 2. Uppdatera `Program.cs` för att hantera en lista

**Program.cs**
```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<Produkt> produkter = new List<Produkt>();
        bool kör = true;

        while (kör)
        {
            Console.Write("Ange produktnamn (eller skriv 'stopp' för att avsluta): ");
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

        Console.WriteLine("\n--- Produktlista ---");
        foreach (Produkt p in produkter)
        {
            p.VisaInfo();
        }
    }
}
```

---

## ✅ Sammanfattning

Du har nu lärt dig:
- Skapa och använda listor
- Använda `foreach` och `while`-loopar
- Läsa in data med `Console.ReadLine()`
- Omvandla text till tal med `Convert.ToDouble()`
- Jämföra strängar med `ToLower()`
- Bygga vidare på din produktklass i ett riktigt program