**<u>Participants</u>** <br/>
**AbstractProduct[Page]** <br/>
**ConcreteProduct[SkillsPage, EducationPage, ExperiencePage]** <br/>
**AbstractCreator[Document]** <br/>
**ConcreteCreator[Report, Resume, Book]** <br/>


**Abstract Product**
```
public abstract class Page {
}
```
**Concrete Product**
```
public class SkillsPage:Page
{
}
public class ExperiencePage : Page
{
}
public class EducationPage : Page
{
}
:
:
//summary, conclusion, result page implns.
```
**Abstract Creator**

```
public abstract class Document
{
    private List<Page> _pages = new List<Page>();
    
    Public List<Page> Pages { 
      get {
          return _pages;
      }
    }
    
    public Document()
    { 
        this.CreatePages();
    }
    
    public abstract Void CreatePages();
}
```

**Concrete Creator**
```
public class Resume: Document
{
    public override void CreatePages()
    {
      Pages.Add(new SkillsPage());
      Pages.Add(new EducagtionPage());
      Pages.Add(new ExperiencePage());
    }
}

public class Report: Document
{
    public override void CreatePages()
    {
      Pages.Add(new IntroductionPage());
      Pages.Add(new ResultsPage());
      Pages.Add(new ConclusionPage());
      Pages.Add(new SummaryPage());
    }
}


