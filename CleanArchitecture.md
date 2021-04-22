## CLEAN ARCHITECHTURE ##

Clean Architecture is just the latest in a series of names for the same loosely-coupled, dependency-inverted architecture. 
You will also find it named hexagonal, ports-and-adapters, or onion architecture.

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
