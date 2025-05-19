# Moment 1 – Objektorientering från grunden

I detta moment kommer du att få lära dig grunderna i objektorienterad programmering (OOP) i C#. Vi kommer att fokusera på hur man skapar **klasser**, **objekt**, **metoder** och **egenskaper**.

## Vad är objektorienterad programmering?

Objektorienterad programmering är en programmeringsstil där man organiserar sin kod i **klasser** och **objekt**.

- En **klass** är en mall (ritning) för ett objekt.
- Ett **objekt** är en instans av en klass, alltså ett faktiskt exemplar du kan använda i ditt program.

T.ex.:
- Klass: `Produkt`
- Objekt: En faktisk produkt som t.ex. en bok med namnet "C# för nybörjare" och priset 199 kr.

## Grundläggande begrepp

### Klass
```csharp
public class Produkt
{
    public string Namn;
    public double Pris;
}
```

Detta är en klass som beskriver en produkt. Den har två **fält**: `Namn` och `Pris`.

### Objekt
```csharp
Produkt bok = new Produkt();
bok.Namn = "C# för nybörjare";
bok.Pris = 199.0;
```

Här skapar vi ett objekt (en bok) av klassen `Produkt`.

### Metod
Vi kan lägga till metoder i vår klass som utför uppgifter:
```csharp
public void VisaInfo()
{
    Console.WriteLine($"{Namn} - {Pris} kr");
}
```

### Konstruktor
En konstruktor låter dig skapa objekt med startvärden direkt:
```csharp
public Produkt(string namn, double pris)
{
    Namn = namn;
    Pris = pris;
}
```

### Egenskaper (Properties)
Det är bättre att använda egenskaper än publika fält:
```csharp
public string Namn { get; set; }
public double Pris { get; set; }
```

## Praktisk övning

1. Skapa ett nytt projekt i VS Code:
```bash
dotnet new console -n Minikatalogen
cd Minikatalogen
code .
```

2. Skapa en ny fil `Produkt.cs` och skriv följande kod:
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

3. I `Program.cs`, skriv följande kod i `Main()`:
```csharp
Produkt bok1 = new Produkt("C# för nybörjare", 199);
Produkt bok2 = new Produkt("Programmering 2", 249);

bok1.VisaInfo();
bok2.VisaInfo();
```

## Sammanfattning
Du har nu lärt dig att:
- Skapa en klass med egenskaper
- Skapa objekt från klassen
- Skriva metoder
- Använda konstruktörer

Dessa grunder kommer att användas i varje kommande moment.