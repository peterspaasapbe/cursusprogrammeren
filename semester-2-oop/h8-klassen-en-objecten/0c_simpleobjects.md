# Methoden en access modifiers

## Een eenvoudige klasse

We zullen nu enkele basisconcepten van klassen en objecten toelichten aan de hand van praktische voorbeelden.

### Object methoden

Stel dat we een klasse willen maken die ons toelaat om objecten te maken die verschillende mensen voorstellen. We willen aan iedere mens kunnen vragen waar deze woont en die zal dat dan op het scherm tonen.

We maken een nieuwe klasse `Human` en maken een methode `Speak` die iets op het scherm zet:

```csharp
public class Human
{
    public void Speak()
    {
        Console.WriteLine("Ik ben een mens!");
    }
}
```

We zien twee nieuwe aspecten:

* Het keyword **`static`** komt bij een klasse niet aan te pas \(of toch minder zoals we [later zullen zien]()\)
* Voor de methode plaatsen we `public` : dit leggen we zo meteen uit

Je kan nu elders objecten aanmaken en ieder object z'n methode `Speak` aanroepen:

```csharp
Human joske = new Human();
Human alfons = new Human();

joske.Speak();
alfons.Speak();
```

Er zal 2x `Ik ben een mens!` op het scherm verschijnen. Waarbij telkens ieder object \(`joske` en `alfons`\) zelf verantwoordelijk ervoor waren dat dit gebeurde.

### Public en private access modifiers

De **access modifier** geeft aan hoe zichtbaar een bepaalde deel van de klasse is. Wanneer je niet wilt dat "van buitenuit" \(bv objecten van je klasse in de `Main`\) een bepaalde methode kan aangeroepen worden, dan dien je deze als `private` in te stellen. Wil je dit net wel dat moet je er expliciet `public` voor zetten.

Test in de voorgaande klasse eens wat gebeurt wanneer je `public` vervangt door `private` voor de methode. Inderdaad, je zal de methode `Speak` niet meer op de objecten kunnen aanroepen.

Test volgende klasse eens, kan je de methode `TellSecret` vanuit de Main op `joske` aanroepen?

```csharp
public class Human
{
    public void Speak()
    {
        Console.WriteLine("Ik ben een mens!");
    }

    private void TellSecret()
    {
        Console.WriteLine("Mijn geheim is dat ik leef!");
    }
}
```

Je kan klassen, methodes,... ook noteren zonder `public` of `private` maar er is een betekenisverschil. Wij verwachten dat je **altijd expliciet** noteert wat je verwacht.

#### Reden van private

Waarom zou je bepaalde zaken `private` maken?

Stel dat we in de klasse extra \(hulp\)methoden willen gebruiken die enkel intern nodig zijn, dan doen we dit. Volgende voorbeeld toont hoe we in de methode `Speak` de private methode `TellSecret` gebruiken:

```csharp
public class Human
{
    public void Speak()
    {
        Console.WriteLine("Ik ben een mens!");
        TellSecret();
    }

    private void TellSecret()
    {
        Console.WriteLine("Mijn geheim is dat ik leef!");
    }
}
```

Als we nu elders een object laten praten als volgt:

```csharp
Human rachid = new Human();
rachid.Speak();
```

Dan zal de uitvoer worden:

```text
Ik ben een mens!
Mijn geheim is dat ik leef!
```

## Instantie variabelen

We maken onze klasse wat groter, we willen dat een object een leeftijd heeft die we kunnen verhogen via een methode `CelebrateBirthday` \(we hebben de methode `TellSecret` even weggelaten\):

```csharp
public class Human
{
    private int age = 1;

    public void CelebrateBirthday()
    {
        Console.WriteLine("Hiphip hoera voor mezelf!");
        age++;
        Speak();
    }

    public void Speak()
    {
        Console.WriteLine("Ik ben een mens! ");
        Console.WriteLine($"Ik ben {age} jaar oud");
    }
}
```

Hier zien we een pak details de onze aandacht vereisen:

* Ook variabelen zoals `int age` mogen een access modifier krijgen in een klasse. Variabelen als deze zetten we altijd op `private` \(tenzij we in de les iets aan het demonstreren zijn\).
* Ook al is `age` `private` , alle methoden in de klasse kunnen hier aan. Het is enkel langs buiten dat bijvoorbeeld volgende code niet zal werken `rachid.age = 34;`
* We kunnen iedere variabele een beginwaarde geven.
* **Ieder object zal z'n eigen leeftijd hebben**

Die laatste opmerking is een kernconcept van OOP: ieder object heeft z'n eigen interne staat die kan aangepast worden individueel van de andere objecten van hetzelfde type.

We zullen dit testen in volgende voorbeeld waarin we 2 objecten maken en enkel 1 ervan laten verjaren. Kijk wat er gebeurt:

```csharp
Human elvis = new Human();
Human bono = new Human();

elvis.CelebrateBirthday();
elvis.CelebrateBirthday();
elvis.CelebrateBirthday();
bono.CelebrateBirthday();
```

Als je deze code zou uitvoeren zal je zien dat de leeftijd van Elvis verhoogt en niet die van Bono wanneer we `CelebrateBirthday` aanroepen. Zoals het hoort!

