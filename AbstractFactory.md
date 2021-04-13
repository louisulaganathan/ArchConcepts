**Participants:**<br/>
**AbstractFactory [ContinentFactory]** <br/>
**ConcreteFactory [AmericaContinent, AfricaContinent]** <br/>
**AbstractProduct [Herbivore, Carnivore]** <br/>
**ConcreteProduct [Wildbeest, Lion,  Bison,Wold]** <br/>
**ClientApp [AnimalWorld]** <br/>
**

**Abstract Factory**
``` 
public abstract class ContinentFactory
{
  public abstract Herbivore CreateHerbivore();
  public abstract Carnivore CreateCarnivore();
}
```

**Concrete Factory**
```
public class AmericaFactory: ContinentFactory
{
    public override  Herbivore CreateHerbivore()
    {
        return new Wildbeest();
    }
    public override Carnivore CreateCarnivore()
    {
        return new Lion();
    }
}
public class AfricaFactory: ContinentFactory
{
    public override  Herbivore CreateHerbivore()
    {
        return new Bison();
    }
    public override Carnivore CreateCarnivore()
    {
        return new Wold();
    }
}
```

**Abstract Product**
```
public abstract class Herbivore
{
}
public abstract class Carnivore
{
    public abstract void Eat(Herbivore h);
}
```

**Concrete Product**

```
public class Wilebeest : Herbivore
{
}
public class Lion: Carnivore
{
    public override void Eat(Herbivore h)
    {
        Console.WriteLine($"{this.GetType().Name} eats {h.getType().Name}");
    }
}
public class Bison : Herbivore
{
}
public class Wolf: Carnivore
{
    public override void Eat(Herbivore h)
    {
        Console.WriteLine($"{this.GetType().Name} eats {h.getType().Name}");
    }
}
```

**Client Application**
```
public class AnimalWorld
{
  private Herbivore _herivore;
  private Carnivore _carnivore;
  
  public AnimalWorld(ContinentFactory factory)
  {
      _herbivore = factory.CreateHerbivore();
      _carnivore = factory.CreateCarnivore();
  }
  
  public void RunFoodChain()
  {
      _carnivore.Eat(_herbivore);
  }
}
```

```
public class MainApp
{
  public static void Main()
  {
      ContinentFactory africa = new AfricaFactory();
      ContinentFactory america = new AmericaFactory();
      AnimalWorld world = new Animalworld(africa);
      world.RunFoodChain();
      world = new Animalworld(america);
      world.RunFoodChain();
  }
  
}
```



