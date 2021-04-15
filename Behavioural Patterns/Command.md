**Participants** <br/>
**Command[]** <br/>
**ConcreteCommand[]** <br/>
**Client[]** <br/>
**Invoker[]** <br/>
**Receiver[]** <br/>

**MainApp startup class for Structural**

```
using System;
 
namespace DoFactory.GangOfFour.Command.Structural
{
  /// <summary>

  /// MainApp startup class for Structural 

  /// Command Design Pattern.

  /// </summary>

  class MainApp

  {
    /// <summary>

    /// Entry point into console application.

    /// </summary>

    static void Main()
    {
      // Create receiver, command, and invoker

      Receiver receiver = new Receiver();
      Command command = new ConcreteCommand(receiver);
      Invoker invoker = new Invoker();
 
      // Set and execute command

      invoker.SetCommand(command);
      invoker.ExecuteCommand();
 
      // Wait for user

      Console.ReadKey();
    }
  }
  
```
  
**Command**

```
 
  /// <summary>

  /// The 'Command' abstract class

  /// </summary>

  abstract class Command

  {
    protected Receiver receiver;
 
    // Constructor

    public Command(Receiver receiver)
    {
      this.receiver = receiver;
    }
 
    public abstract void Execute();
  }
  
```
  
**ConcreteCommand**

```
 
  /// <summary>

  /// The 'ConcreteCommand' class

  /// </summary>

  class ConcreteCommand : Command

  {
    // Constructor

    public ConcreteCommand(Receiver receiver) :
      base(receiver)
    {
    }
 
    public override void Execute()
    {
      receiver.Action();
    }
  }
```
  
**Receiver - Handler**

```
 
  /// <summary>

  /// The 'Receiver' class

  /// </summary>

  class Receiver

  {
    public void Action()
    {
      Console.WriteLine("Called Receiver.Action()");
    }
  }
  
```
  
**Invoker**

```
  
  /// <summary>

  /// The 'Invoker' class

  /// </summary>

  class Invoker

  {
    private Command _command;
 
    public void SetCommand(Command command)
    {
      this._command = command;
    }
 
    public void ExecuteCommand()
    {
      _command.Execute();
    }
  }
}
```
```



