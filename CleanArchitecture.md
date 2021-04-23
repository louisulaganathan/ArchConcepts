## CLEAN ARCHITECHTURE ##

Principles to be considered for Clean architecture
**Seperation of Concerns**
    Avoid mixing different code responsibilities in same Method/class/project
      Data Access
      Business Rules & Domain Models
      User Interface
**SOLID - SRP **
**DRY **
**SOLID -DIP**

**Domain Model is not just business logic but also**
  A Model of the problem space composed of Entities , Interface, services & more.
  Interface defines contracts for working with domain objects
  Everythins in the appln depends on these interfaces & domain objects.
  
 ### What goes in Core ###
 
 Interfaces,
 Entities, Value objects,  Aggregates. => Domain Types
 Domain Services. - >service contains logics/actions to be performed on multiple entities
 Exceptions -> custom or appln exception
 
 Specification = >Querying logics for repository
 
 Domain Events
 Event Handlewrs
 
  ### What goes in Infrastructure ###
  Something which is not running on your 
  talks to something it not in your code, not in your memory space
  Repositories, EF(Core) DB Context, Cached Repositories
  Web API Clients
  File System Accesssors, Logging Adaptors
  Email/SMS Sending
  
  System Clock
  Other services [s3,blocb storage]
  
   ### What goes in Web ###
   Controllers, Views, Razor pages
   ViewModels, Api Models, Binding Models.  -> DTOs
   Filters, Binders, Tag/Html Helpers
   
   Other services & interfaces
   
   ### What goes in Shared Kernal ###
   Sharing logics between solutions.
   Common types between solutions will be distribute as **Nuget Packages**.
   
   Base Entity, Base Domain Event, Base Specification
   Common Exceptions, Common Interfaces
   Common Auth, Common DI, Common Logging, Common Guard Clauses
   
 <img width="785" alt="CleanArch-Layered " src="https://user-images.githubusercontent.com/74425320/115925782-532ca480-a447-11eb-899b-6f91c8b774e0.png">

<img width="781" alt="CleanArch-FolderStructure" src="https://user-images.githubusercontent.com/74425320/115925843-6b9cbf00-a447-11eb-842d-bc99f6ee66d7.png">

          

Applications that follow the Dependency Inversion Principle as well as the Domain-Driven Design (DDD) principles tend to arrive at a similar architecture
Clean Architecture is just the latest in a series of names for the same loosely-coupled, dependency-inverted architecture. 
You will also find it named hexagonal, ports-and-adapters, or onion architecture.

![Clean-1](https://user-images.githubusercontent.com/74425320/115637623-37ee5780-a2d6-11eb-9265-91fd2e83c82e.png)

![Clean-2](https://user-images.githubusercontent.com/74425320/115637846-c236bb80-a2d6-11eb-92b8-61bcf764de87.png)

![Clean-3](https://user-images.githubusercontent.com/74425320/115637686-5f452480-a2d6-11eb-8dfe-5fba0bd6879f.png)

![Clean-4](https://user-images.githubusercontent.com/74425320/115637707-6bc97d00-a2d6-11eb-9325-835dee1c19bd.png)

![Clean-5](https://user-images.githubusercontent.com/74425320/115637718-71bf5e00-a2d6-11eb-9cb4-b06ac7eba16d.png)


Domain Driven Design DDD
  
  
  ### The Core Project ###
  The Core project is the center of the Clean Architecture design, and all other project dependencies should point toward it. As such, it has very few external dependencies. The one exception in this case is the System.Reflection.TypeExtensions package, which is used by ValueObject to help implement its IEquatable<> interface. The Core project should include things like:

    Entities
    Aggregates
    Domain Events
    DTOs
    Interfaces
    Event Handlers
    Domain Services
    Specifications

 ### The Infrastructure Project ###
 
 Most of your application's dependencies on external resources should be implemented in classes defined in the Infrastructure project. 
 These classes should implement interfaces defined in Core. If you have a very large project with many dependencies, 
 it may make sense to have multiple Infrastructure projects (e.g. Infrastructure.Data), but for most projects one Infrastructure project with folders works fine. 
 
 The sample includes data access and domain event implementations, but you would also add things like email providers, file access, web api clients, etc. 
 to this project so they're not adding coupling to your Core or UI projects.

The Infrastructure project depends on Microsoft.EntityFrameworkCore.SqlServer and Autofac. 
The former is used because it's built into the default ASP.NET Core templates and is the least common denominator of data access. 
If desired, it can easily be replaced with a lighter-weight ORM like Dapper. 
Autofac (formerly StructureMap) is used to allow wireup of dependencies to take place closest to where the implementations reside.

### The Web Project ###

The entry point of the application is the ASP.NET Core web project. This is actually a console application, with a public static void Main method in Program.cs. 
It currently uses the default MVC organization (Controllers and Views folders) as well as most of the default ASP.NET Core project template code. 
This includes its configuration system, which uses the default appsettings.json file plus environment variables, and is configured in Startup.cs. 
The project delegates to the Infrastructure project to wire up its services using Autofac.

### The Test Projects ####

Test projects could be organized based on the kind of test (unit, functional, integration, performance, etc.) or 
by the project they are testing (Core, Infrastructure, Web), or both. For this simple starter kit, 
the test projects are organized based on the kind of test, with unit, functional and integration test projects existing in this solution. 
In terms of dependencies, there are three worth noting:

    ** xunit ** I'm using xunit because that's what ASP.NET Core uses internally to test the product. It works great and as new versions of ASP.NET Core ship, I'm confident it will continue to work well with it.

    ** Moq ** I'm using Moq as a mocking framework for white box behavior-based tests. If I have a method that, under certain circumstances, should perform an action that isn't evident from the object's observable state, mocks provide a way to test that. I could also use my own Fake implementation, but that requires a lot more typing and files. Moq is great once you get the hang of it, and assuming you don't have to mock the world (which we don't in this case because of good, modular design).
