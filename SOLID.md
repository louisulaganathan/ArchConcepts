** SOLID Design Principles**

SOLID principles are the design principles

**S** is single responsibility principle (SRP)<br/>       
**O**  stands for open closed principle (OCP)<br/>
**L**  Liskov substitution principle (LSP)<br/>
**I**  interface segregation principle (ISP)<br/>
**D**  Dependency injection principle (DIP)<br/>


**Advantages of SOLID Principles in C#** <br/>
  Maintainability<br/>
  Testability<br/>
  Flexibility and Extensibility<br/>
  Parallel Development<br/>

**Single Responsibility Principle**

A class should take one responsibility and there should be one reason to change that class.

Code that ignore SRP:
```
class Customer
    {
        public void Add()
        {
            try
            {
                // Database code goes here
            }
            catch (Exception ex)
            {
                System.IO.File.WriteAllText(@"c:\Error.txt", ex.ToString());
            }
        }
    }
 ```
 
 ```
 namespace SRP
{
    public class Employee
    {
        public int Employee_Id { get; set; }
        public string Employee_Name { get; set; }

        /// <summary>
        /// This method used to insert into employee table
        /// </summary>
        /// <param name="em">Employee object</param>
        /// <returns>Successfully inserted or not</returns>
        public bool InsertIntoEmployeeTable(Employee em)
        {
            // Insert into employee table.
            return true;
        }
        /// <summary>
        /// Method to generate report
        /// </summary>
        /// <param name="em"></param>
        public void GenerateReport(Employee em)
        {
            // Report generation with employee data using crystal report.
        }
    }
}
 ```
 
 **SRP implementation**
 ```
 class FileLogger
    {
        public void Handle(string error)
        {
            System.IO.File.WriteAllText(@"c:\Error.txt", error);
        }
    }
    
 class Customer
    {
        private FileLogger obj = new FileLogger();
        publicvirtual void Add()
        {
            try
            {
                // Database code goes here
            }
            catch (Exception ex)
            {
                obj.Handle(ex.ToString());
            }
        }
    }
 ```
 
 ```
 public class ReportGeneration
{
     /// <summary>
     /// Method to generate report
     /// </summary>
     /// <param name="em"></param>
     public void GenerateReport(Employee em)
     {
         // Report reneration with employee data.
     }
}
```

**Open Closed Principe**

A software module/class is open for extension and closed for modification

**Ignore OCP principle**
```
public class ReportGeneration
{
    /// <summary>
    /// Report type
    /// </summary>
    public string ReportType { get; set; }

    /// <summary>
    /// Method to generate report
    /// </summary>
    /// <param name="em"></param>
    public void GenerateReport(Employee em)
    {
        if (ReportType == "CRS")
        {
             // Report generation with employee data in Crystal Report.
        }
        if (ReportType == "PDF")
        {
            // Report generation with employee data in PDF.
        }
     }
 }
```
**Open Closed Principle**
```
public class IReportGeneration
    {
        /// <summary>
        /// Method to generate report
        /// </summary>
        /// <param name="em"></param>
        public virtual void GenerateReport(Employee em)
        {
            // From base
        }
    }
    /// <summary>
    /// Class to generate Crystal report
    /// </summary>
    public class CrystalReportGeneraion : IReportGeneration
    {
        public override void GenerateReport(Employee em)
        {
            // Generate crystal report.
        }
    }
    /// <summary>
    /// Class to generate PDF report
    /// </summary>
    public class PDFReportGeneraion : IReportGeneration
    {
        public override void GenerateReport(Employee em)
        {
            // Generate PDF report.
        }
    }
```

**Liskov Subtitution Principle**

you should be able to use any derived class instead of a parent class and have it behave in the same manner without modification.

**Ignoring LSP**

```
public abstract class Employee
{
    public virtual string GetProjectDetails(int employeeId)
    {
        return "Base Project";
    }
    public virtual string GetEmployeeDetails(int employeeId)
    {
        return "Base Employee";
    }
}
public class CasualEmployee : Employee
{
    public override string GetProjectDetails(int employeeId)
    {
        return "Child Project";
    }
    // May be for contractual employee we do not need to store the details into database.
    public override string GetEmployeeDetails(int employeeId)
    {
        return "Child Employee";
    }
}
public class ContractualEmployee : Employee
{
    public override string GetProjectDetails(int employeeId)
    {
        return "Child Project";
    }
    // May be for contractual employee we do not need to store the details into database.
    public override string GetEmployeeDetails(int employeeId)
    {
        throw new NotImplementedException();
    }
}
```

**LSP**
```
public interface IEmployee
{
    string GetEmployeeDetails(int employeeId);
}

public interface IProject
{
    string GetProjectDetails(int employeeId);
}
```

**Interface Segregation Principle**

that clients should not be forced to implement interfaces they don't use. Instead of one fat interface, many small interfaces are preferred based on groups of methods, each one serving one submodule.
```
public interface IEmployeeDatabase
{
    bool AddEmployeeDetails();
    bool ShowEmployeeDetails(int employeeId);
}
```

**ISP**

```
public interface IAddOperation
{
    bool AddEmployeeDetails();
}
public interface IGetOperation
{
    bool ShowEmployeeDetails(int employeeId);
}
```

**Depedency Inversion Principle**

The Dependency Inversion Principle (DIP) states that high-level modules/classes should not depend on low-level modules/classes. Both should depend upon abstractions. Secondly, abstractions should not depend upon details. Details should depend upon abstractions.

```
public class Email
{
    public void SendEmail()
    {
        // code to send mail
    }
}

public class Notification
{
    private Email _email;
    public Notification()
    {
        _email = new Email();
    }

    public void PromotionalNotification()
    {
        _email.SendEmail();
    }
}
```

**DIP**
```
public interface IMessenger
{
    void SendMessage();
}
public class Email : IMessenger
{
    public void SendMessage()
    {
        // code to send email
    }
}

public class SMS : IMessenger
{
    public void SendMessage()
    {
        // code to send SMS
    }
}
public class Notification
{
    private IMessenger _iMessenger;
    public Notification()
    {
        _ iMessenger = new Email();
    }
    public void DoNotify()
    {
        _ iMessenger.SendMessage();
    }
}


```

**DIP**

```
public class Notification
{
    private IMessenger _iMessenger;
    public Notification(Imessenger pMessenger)
    {
        _ iMessenger = pMessenger;
    }
    public void DoNotify()
    {
        _ iMessenger.SendMessage();
    }
}
public class Notification
{
    private IMessenger _iMessenger;

    public Notification()
    {
    }
    public IMessenger MessageService
    {
       private get;
       set
       {
           _ iMessenger = value;
       }
     }

    public void DoNotify()
    {
        _ iMessenger.SendMessage();
    }
}

public class Notification
{
    public void DoNotify(IMessenger pMessenger)
    {
        pMessenger.SendMessage();
    }
}
```

