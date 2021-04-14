**Participants** <br/>
**Abstraction ** <br/>
**RefinedAbstraction ** <br/>
**Implementor ** <br/>
**ConcreteImplementor ** <br/>

```
    public abstract class Abstraction
    {
       public Bridge Implementer { get; set; }

       public virtual void Operation()
       {
           Console.WriteLine("ImplementationBase:Operation()");
           Implementer.OperationImplementation();
       }
    }

    public class RefinedAbstraction : Abstraction
    {
         public override void Operation()
         {
             Console.WriteLine("RefinedAbstraction:Operation()");
             Implementer.OperationImplementation();
         }
    }
//Implementor
    public interface Bridge
    {
        void OperationImplementation();
    }
//Concrete implementor
    public class ImplementationA : Bridge
    {
         public void OperationImplementation()
         {
            Console.WriteLine("ImplementationA:OperationImplementation()");
         }
    }

    public class ImplementationB : Bridge
    {
       public void OperationImplementation()
       {
          Console.WriteLine("ImplementationB:OperationImplementation()");
       }
    }
```
