# Moment 3 – Inkapsling och arv

I detta moment fortsätter vi att utveckla vårt katalogsystem och lär oss två viktiga principer i objektorienterad programmering: **inkapsling** och **arv**.

Eftersom detta är en distanskurs kommer vi gå igenom alla begrepp noggrant med exempel, så du kan läsa i lugn och ro och förstå hur allt hänger ihop.

---

## 🔒 Vad är inkapsling?

**Inkapsling** betyder att vi "kapslar in" data i våra klasser så att ingen annan del av programmet kan ändra den direkt. På så sätt skyddar vi vår data och gör koden mer robust och lättare att underhålla.

### 🔧 Varför använda inkapsling?
- Vi undviker att andra delar av programmet gör oväntade ändringar i datan.
- Vi kan lägga till logik när värden sätts, t.ex. kontrollera att priset inte är negativt.
- Vi gör det lättare att felsöka och förbättra koden senare.

---

## 🧱 get och set – hur fungerar det?

I C# använder vi **egenskaper** (properties) för att styra tillgång till data. En egenskap består av en **get-metod** och en **set-metod**.

### Exempel – egenskap för `Pris`:

```csharp
private double pris; // det verkliga värdet sparas här

public double Pris    // detta är egenskapen
{
    get { return pris; }              // används för att läsa värdet
    set { pris = value; }             // används för att sätta ett nytt värde
}
```

- `get` returnerar det interna värdet
- `set` sätter det interna värdet. `value` är det som skickas in.

### Kortare variant: Auto-egenskap

Om vi inte behöver extra logik kan vi använda en **auto-egenskap**:

```csharp
public string Namn { get; set; }
```

Detta skapar automatiskt ett dolt fält och en enkel get/set.


---

## 🛡️ Vad menas med inkapsling i praktiken?

För att inkapsla data i en klass använder man två saker tillsammans:

1. **Privata fält** (`private`) som inte kan nås direkt utifrån.
2. **Publika egenskaper** (`get`/`set`) som ger kontrollerad åtkomst till fälten.

### Exempel:

```csharp
public class Produkt
{
    private string namn;

    public string Namn
    {
        get { return namn; }        // kontroll över hur data hämtas
        set { namn = value; }       // kontroll över hur data sätts
    }
}
```

På detta sätt skyddas det privata fältet `namn` från direkt åtkomst.

---

## ⚖️ Auto-egenskaper vs vanliga egenskaper

I C# kan du också skriva så här:

```csharp
public string Namn { get; set; }
```

Detta kallas en **auto-egenskap**. Den skapar automatiskt ett dolt privat fält åt dig.

### Jämförelse:

| Typ | Beskrivning | Kontrollnivå | Kan innehålla logik? | Bra för |
|-----|-------------|---------------|------------------------|----------|
| **Auto-egenskap** | Kort syntax, inbyggt privat fält | Enkel | ❌ Nej | Enkla fall |
| **Vanlig egenskap** | Skriver `get`/`set` själv | Full kontroll | ✅ Ja | Validering, logik |

---

### Före och efter: Exempel på inkapsling

**Inget skydd (inte inkapslat):**

```csharp
public class Produkt
{
    public string Namn; // kan ändras direkt från utsidan, t.ex. produkt.Namn = null;
}
```

**Med inkapsling:**

```csharp
public class Produkt
{
    private string namn;

    public string Namn
    {
        get { return namn; }
        set
        {
            if (!string.IsNullOrWhiteSpace(value))
                namn = value;
        }
    }
}
```

🔹 Här skyddas värdet från att bli tomt eller null.

---



## 🧬 Vad är arv?

**Arv** innebär att en klass (subklass) ärver egenskaper och metoder från en annan klass (basklass). Det låter oss bygga vidare på existerande kod.

### Exempel:
```csharp
public class Produkt
{
    public string Namn { get; set; }
    public double Pris { get; set; }
}

public class Bok : Produkt
{
    public string Författare { get; set; }
}
```

Här är `Bok` en specialversion av `Produkt`, med en extra egenskap: `Författare`.

---

## 🛠️ Praktisk övning

Vi ska nu utöka vårt program med arv och förbättrad **inkapsling**.

---

### 1. Uppdatera din `Produkt.cs` med inkapslade fält

Istället för att använda auto-egenskaper använder vi nu **privata fält och vanliga egenskaper**. Det gör att vi i framtiden kan kontrollera vilka värden som sätts.

**Produkt.cs**
```csharp
public class Produkt
{
    private string namn;
    private double pris;

    public string Namn
    {
        get { return namn; }
        set
        {
            if (!string.IsNullOrWhiteSpace(value))
                namn = value;
        }
    }

    public double Pris
    {
        get { return pris; }
        set
        {
            if (value >= 0)
                pris = value;
        }
    }

    public Produkt(string namn, double pris)
    {
        Namn = namn;
        Pris = pris;
    }

    public virtual void VisaInfo()
    {
        Console.WriteLine($"{Namn} - {Pris} kr");
    }
}
```

🔹 Här använder vi `private` fält och `get/set`-metoder för att **inkapsla** datan.  
🔹 Vi lägger även till enkel **validering** i `set` för att undvika tomma namn eller negativa priser.

---

### 2. Skapa en ny subklass `Bok`

**Bok.cs**
```csharp
public class Bok : Produkt
{
    public string Författare { get; set; }

    public Bok(string namn, double pris, string författare) : base(namn, pris)
    {
        Författare = författare;
    }

    public override void VisaInfo()
    {
        Console.WriteLine($"{Namn} (Bok av {Författare}) - {Pris} kr");
    }
}
```

---

### 3. Använd båda klasserna i `Program.cs`

**Program.cs**
```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<Produkt> produkter = new List<Produkt>();

        produkter.Add(new Produkt("USB-laddare", 99));
        produkter.Add(new Bok("C# på riktigt", 249, "Anna Svensson"));

        foreach (Produkt p in produkter)
        {
            p.VisaInfo();
        }
    }
}
```

🔹 Eftersom både `Produkt` och `Bok` är av typen `Produkt`, kan vi lagra dem i samma lista!

---

## ✅ Sammanfattning

Du har nu lärt dig:
- Hur inkapsling fungerar med `private` fält + `get`/`set`
- Skillnaden mellan auto-egenskaper och manuella egenskaper
- Hur arv används för att skapa varianter av en basklass
- Hur `virtual` och `override` används för att anpassa metoder

Vi ska nu utöka vårt program med arv och förbättrad inkapsling.

### 1. Uppdatera din `Produkt.cs`

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

    public virtual void VisaInfo()
    {
        Console.WriteLine($"{Namn} - {Pris} kr");
    }
}
```

🔹 Nytt: `virtual` gör det möjligt att skriva över metoden i en subklass.

---

### 2. Skapa en ny subklass `Bok`

**Bok.cs**
```csharp
public class Bok : Produkt
{
    public string Författare { get; set; }

    public Bok(string namn, double pris, string författare) : base(namn, pris)
    {
        Författare = författare;
    }

    public override void VisaInfo()
    {
        Console.WriteLine($"{Namn} (Bok av {Författare}) - {Pris} kr");
    }
}
```

🔹 Här använder vi `: base(...)` för att skicka namn och pris till basklassens konstruktor.  
🔹 Vi skriver över `VisaInfo()` med `override` för att visa mer information.

---

### 3. Använd båda klasserna i `Program.cs`

**Program.cs**
```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<Produkt> produkter = new List<Produkt>();

        produkter.Add(new Produkt("USB-laddare", 99));
        produkter.Add(new Bok("C# på riktigt", 249, "Anna Svensson"));

        foreach (Produkt p in produkter)
        {
            p.VisaInfo();
        }
    }
}
```

🔹 Eftersom både `Produkt` och `Bok` är av typen `Produkt`, kan vi lagra dem i samma lista!

---

## ✅ Sammanfattning

Du har nu lärt dig:
- Hur inkapsling fungerar med `get` och `set`
- Hur man använder egenskaper för att kontrollera tillgång till data
- Hur arv används för att skapa olika varianter av produkter
- Hur man använder `virtual` och `override` för att anpassa beteende
- Hur man jobbar vidare med katalogen och lägger till flera typer av produkter