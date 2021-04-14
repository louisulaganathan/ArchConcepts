**Design Patterns => Gang of Four [GOF]**

  Design patterns are the proven solutions for the frequently occurring design problems during software development.
  
  |Creational|Structural|Behavioural|
  |--------|--------|--------|
  |Abstract Factory|Adapter|Interpreter|
  |Builder|Bridge|Iterator|
  |Factory Method|Decorator|Observer|
  |Prototype|Facade|State|
  |Singleton|Proxy|Template Method|
  |||Visitor|
  
  |Type|Description|
  |-----|------|
  |Creational[5]|Creational design patterns concerns with the object creation mechanism.|
  |Structural[7]|Structural design patterns concerns with the class and object compositions. how objects and classes can be combined and form a large structure and that ease the design by identifying a simple way to realize relationshipe between entities.|
  |Behavioural[11]|Behavioral design pattern concerns with communication between objects.|
  
  **Creational Design Patterns**
  
 | **Design Pattern**| **Explanation**|
 |-----------------|------------------------------------------|
 |Abstract Factory[5]|Creates an instance of several families of classes. Define an interface for creating families of related or dependent objects without specifying their concrete classes.|
 |Factory Method[5]|Creates an instance of serveral derived classes. Define an interface for creating an object but let the subclasses decide which class to instantiate. |
 |Builder[3]|Seperates the objects creation from its representations.|
 |Prototype[3]|A fully initialized instance to be copied or cloned.|
 |Singleton[4]| Ensure a class has only one instance and provide a global point of access to it.|
 
  **Structural Design Patterns**
  
 | **Design Pattern**| **Explanation**|
 |-----------------|------------------------------------------|
 |Adapter[4]|Match interfaces of different classes. Adapter pattern acts as a bridge between two incompatible interfaces. This pattern involves a class called adapter which is responsible for communication between two incompatible & independent interfaces.|
 |Bridge[3]| Seperates an object's interface from its implementation. The bridge pattern is used to separate abstraction from its implementation so that both can be modified independently.|
 |Decorator[3]| Add responsibilities to objects dynamically. The decorator pattern is used to add new functionality to an existing object without changing its structure.|
 |Facade[5]| A single class that represents the entire subsystem. Provide a unified interface to a set of interfaces in a subsystem|
 |Proxy[4]|An object representing another object.Provide surrogate or placeholder for another object to control access to it.|
 
 
   **Behavioral Design Patterns**
  
 | **Design Pattern**| **Explanation**|
 |-----------------|------------------------------------------|
 |Command|Encapsulates a command request as an object.|
 |Interpreter|A way to include language elements in a program.|
 |Mediator|Defines simplified communication between classes.|
 |Memento|Capture and restore an object's internal state.|
 |Observer[5]|A way of notifying change to a number of classes. Used when there is one-to-many relationship between objects so that when one object changes state, all its dependents are notified and updated automatically.|
 |State|Alter an object's behavior when its state changes.|
 |Strategy|Encapsulates an algorithm inside a class.|
 |Template Method|Defer the exact steps of an algorithm to the subclass|
 |Visitor|Defines the new operation to a class without change|
 
 
