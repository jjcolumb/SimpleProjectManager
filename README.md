# Basic ASP.NET Core Blazor Tutorial (Simple Project Manager Demo)
This tutorial explains how to create an XAF application that is used within a company department and can be opened in desktop and mobile browsers. It uses **DevExpress ASP.NET Core Blazor** UI controls for data presentation, and **DevExpress XPO** for data access.

![251030327-9542a20f-7113-4eda-ae8c-c91dcf0549de](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/d2870225-14f0-4ef6-a501-3e347a11419c)

This ASP.NET Core Blazor application can be used in the following scenarios:

* a user can view, search, create, update, and delete employees, projects and task data;
* a user can view, search, create, update, and delete customers and comments about a product to organize and provide data for a promotional website.

In this tutorial, you write the platform-agnostic code that affects application aspects that are not specific to the ASP.NET Core Blazor platform. XAF automatically generates UI screens and specifies database access.

## Create an XAF Application
This topic describes how to use the Solution Wizard to create an XAF application and specify its connection string.

### Create the ASP.NET Core Blazor Applications
1. From Visual Studio’s main menu, select File | New | Project… to invoke the Create a new project dialog.
2. Select DevExpress v22.1 XAF Template Gallery and click Next.

![251030835-e18fb92f-af50-438d-a7c8-f05fe46c8331](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/2b71a320-d17b-4d75-b735-9ff59aff76cc)


3. Specify the project name (“SimpleProjectManager”) and click Create.

![251030988-64de43fc-0f5b-4b7c-bf15-146ee2f01a17](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/9602440d-7006-4096-a241-8d05d80e70b1)


4. In the invoked Template Gallery, select XAF Solution Wizard (.NET Core) in the .NET Core section and click Run Wizard.

![251031048-6ff3c04c-7767-4e7d-a8fc-9dab25f77341](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/2c40b70c-a429-44d2-934a-68859cef91ae)


5. Choose Web (ASP.NET Core Blazor) and click Next.

![251031103-7a1df1a7-aed8-4b0d-86f8-435c06731de4](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/adbd517a-1fe6-4242-91f3-f26fe5baeaba)


6. Choose eXpress Persistent Objects and click Next.

![251031152-3d0c61dd-e13c-48a1-95c0-ef107472fd77](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/3a46c7a3-9515-47a0-92a9-679393ab7cc3)


> **Note:** You can use the Entity Framework Core﻿ or eXpress Persistent Objects (XPO)﻿ as your project’s object-relational mapping (ORM)﻿ tool. This tutorial demonstrates the XPO-based approach.

7. You can now choose security options for your application. Choose None as the Authentication type. This tutorial does not show how to use the XAF Security System. Click Finish.

![251031462-cd52a99f-9abb-4b93-8c7b-c1fd54afc984](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/400b353c-247b-487d-b9de-b8fc919983c5)



The Solution Wizard creates a solution with the following projects:

![251031692-3256a2ab-420a-4c5f-9b32-38af2fe2f80b](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/1ca4ef5d-e9af-40e9-992e-e8db601dc27a)


### Specify the Database Connection

The wizard connects the application to the **Microsoft SQL Server** database with the following connection string:

**"Integrated Security=SSPI;Pooling=false;Data Source=(localdb)\\mssqllocaldb;Initial Catalog=SimpleProjectManager"**

You can modify this connection string in the *SimpleProjectManager.Blazor.Server\appsettings.json* file (refer to the connectionStrings element). See the Connect an XAF Application to a Database Provider topic for more information.

At this stage, you can run the *ASP.NET Core Blazor* applications with automatically created navigation, menu, and other UI elements for line-of-business (LOB) applications. However, the data model and logic are not defined yet - this is implemented in the following topics.


## Define the Data Model and Set the Initial Data

This topic describes how to define the data model and business logic for your ASP.NET Core Blazor application. The application’s data model contains two logical parts:

* Marketing: the Customer and Testimonial classes
* Planning: the Project and Task classes

### Add the Customer and Testimonial Persistent Classes

1. In the **Solution Explorer**, right-click the *SimpleProjectManager.Module\BusinessObjects* folder and select **Add | Class…** from the context menu. Set the name to **“Marketing”** and click **Add**.

2. Replace the auto-generated file’s content with the following code:

```csharp
using DevExpress.Persistent.Base;
using DevExpress.Persistent.BaseImpl;
using DevExpress.Xpo;
using System;

namespace SimpleProjectManager.Module.BusinessObjects.Marketing {
    [NavigationItem("Marketing")]
    public class Customer : BaseObject {
        public Customer(Session session) : base(session) { }
        string firstName;
        public string FirstName {
            get { return firstName; }
            set { SetPropertyValue(nameof(FirstName), ref firstName, value); }
        }
        string lastName;
        public string LastName {
            get { return lastName; }
            set { SetPropertyValue(nameof(LastName), ref lastName, value); }
        }
        string email;
        public string Email {
            get { return email; }
            set { SetPropertyValue(nameof(Email), ref email, value); }
        }
        string company;
        public string Company {
            get { return company; }
            set { SetPropertyValue(nameof(Company), ref company, value); }
        }
        string occupation;
        public string Occupation {
            get { return occupation; }
            set { SetPropertyValue(nameof(Occupation), ref occupation, value); }
        }
        [Association("Customer-Testimonials")]
        public XPCollection<Testimonial> Testimonials {
            get { return GetCollection<Testimonial>(nameof(Testimonials)); }
        }
        public string FullName {
            get {
                string namePart = string.Format("{0} {1}", FirstName, LastName);
                return Company != null ? string.Format("{0} ({1})", namePart, Company) : namePart;
            }
        }
        byte[] photo;
        [ImageEditor(ListViewImageEditorCustomHeight = 75, DetailViewImageEditorFixedHeight = 150)]
        public byte[] Photo {
            get { return photo; }
            set { SetPropertyValue(nameof(Photo), ref photo, value); }
        }
    }
    [NavigationItem("Marketing")]
    public class Testimonial : BaseObject {
        public Testimonial(Session session) : base(session) {
            createdOn = DateTime.Now;
        }
        string quote;
        public string Quote {
            get { return quote; }
            set { SetPropertyValue(nameof(Quote), ref quote, value); }
        }
        string highlight;
        [Size(512)]
        public string Highlight {
            get { return highlight; }
            set { SetPropertyValue(nameof(Highlight), ref highlight, value); }
        }
        DateTime createdOn;
        [VisibleInListView(false)]
        public DateTime CreatedOn {
            get { return createdOn; }
            internal set { SetPropertyValue(nameof(CreatedOn), ref createdOn, value); }
        }
        string tags;
        public string Tags {
            get { return tags; }
            set { SetPropertyValue(nameof(Tags), ref tags, value); }
        }
        Customer customer;
        [Association("Customer-Testimonials")]
        public Customer Customer {
            get { return customer; }
            set { SetPropertyValue(nameof(Customer), ref customer, value); }
        }
    }
}
```

### Add the Project and ProjectTask Persistent Classes

1. In the **Solution Explorer**, right-click the *SimpleProjectManager.Module\BusinessObjects* folder and select **Add | Class…** from the context menu. Set the name to “Planning” and click **Add**.

2. Replace the auto-generated file’s content with the following code:

```csharp
using System;
using DevExpress.Persistent.Base;
using DevExpress.Persistent.BaseImpl;
using DevExpress.Xpo;

namespace SimpleProjectManager.Module.BusinessObjects.Planning {
    [NavigationItem("Planning")]
    public class ProjectTask : BaseObject {
        public ProjectTask(Session session) : base(session) { }
        string subject;
        [Size(255)]
        public string Subject {
            get { return subject; }
            set { SetPropertyValue(nameof(Subject), ref subject, value); }
        }
        ProjectTaskStatus status;
        public ProjectTaskStatus Status {
            get { return status; }
            set { SetPropertyValue(nameof(Status), ref status, value); }
        }
        Person assignedTo;
        public Person AssignedTo {
            get { return assignedTo; }
            set { SetPropertyValue(nameof(AssignedTo), ref assignedTo, value); }
        }
        DateTime startDate;
        public DateTime StartDate {
            get { return startDate; }
            set { SetPropertyValue(nameof(startDate), ref startDate, value); }
        }
        DateTime endDate;
        public DateTime EndDate {
            get { return endDate; }
            set { SetPropertyValue(nameof(endDate), ref endDate, value); }
        }
        string notes;
        [Size(SizeAttribute.Unlimited)]
        public string Notes {
            get { return notes; }
            set { SetPropertyValue(nameof(Notes), ref notes, value); }
        }
        Project project;
        [Association]
        public Project Project {
            get { return project; }
            set { SetPropertyValue(nameof(Project), ref project, value); }
        }
    }
    [NavigationItem("Planning")]
    public class Project : BaseObject {
        public Project(Session session) : base(session) { }
        string name;
        public string Name {
            get { return name; }
            set { SetPropertyValue(nameof(Name), ref name, value); }
        }
        Person manager;
        public Person Manager {
            get { return manager; }
            set { SetPropertyValue(nameof(Manager), ref manager, value); }
        }
        string description;
        [Size(SizeAttribute.Unlimited)]
        public string Description {
            get { return description; }
            set { SetPropertyValue(nameof(Description), ref description, value); }
        }
        [Association, Aggregated]
        public XPCollection<ProjectTask> Tasks {
            get { return GetCollection<ProjectTask>(nameof(Tasks)); }
        }
    }

    public enum ProjectTaskStatus {
        NotStarted = 0,
        InProgress = 1,
        Completed = 2,
        Deferred = 3
    }
}
```

### Populate the Database with Initial Data

Open the *Updater.cs* file from the *SimpleProjectManager.Module* project’s Database Update folder and override the `ModuleUpdater.UpdateDatabaseAfterUpdateSchema` method as shown below:

```csharp
using DevExpress.Persistent.BaseImpl;
using SimpleProjectManager.Module.BusinessObjects.Marketing;
using SimpleProjectManager.Module.BusinessObjects.Planning;
// ...
public class Updater : ModuleUpdater {
    //...
    public override void UpdateDatabaseAfterUpdateSchema() {
        base.UpdateDatabaseAfterUpdateSchema();
        if (ObjectSpace.CanInstantiate(typeof(Person))) {
            Person person = ObjectSpace.FirstOrDefault<Person>(p => p.FirstName == "John" && p.LastName == "Nilsen");
            if (person == null) {
                person = ObjectSpace.CreateObject<Person>();
                person.FirstName = "John";
                person.LastName = "Nilsen";
            }
        }
        if (ObjectSpace.CanInstantiate(typeof(ProjectTask))) {
            ProjectTask task = ObjectSpace.FirstOrDefault<ProjectTask>(t => t.Subject == "TODO: Conditional UI Customization");
            if (task == null) {
                task = ObjectSpace.CreateObject<ProjectTask>();
                task.Subject = "TODO: Conditional UI Customization";
                task.Status = ProjectTaskStatus.InProgress;
                task.AssignedTo = ObjectSpace.FirstOrDefault<Person>(p => p.FirstName == "John" && p.LastName == "Nilsen");
                task.StartDate = new DateTime(2019, 1, 30);
                task.Notes = "OVERVIEW: http://www.devexpress.com/Products/NET/Application_Framework/features_appearance.xml";
            }
        }
        if (ObjectSpace.CanInstantiate(typeof(Project))) {
            Project project = ObjectSpace.FirstOrDefault<Project>(p => p.Name == "DevExpress XAF Features Overview");
            if (project == null) {
                project = ObjectSpace.CreateObject<Project>();
                project.Name = "DevExpress XAF Features Overview";
                project.Manager = ObjectSpace.FirstOrDefault<Person>(p => p.FirstName == "John" && p.LastName == "Nilsen");
                project.Tasks.Add(ObjectSpace.FirstOrDefault<ProjectTask>(t => t.Subject == "TODO: Conditional UI Customization"));
            }
        }
        if (ObjectSpace.CanInstantiate(typeof(Customer))) {
            Customer customer = ObjectSpace.FirstOrDefault<Customer>(c => c.FirstName == "Ann" && c.LastName == "Devon");
            if (customer == null) {
                customer = ObjectSpace.CreateObject<Customer>();
                customer.FirstName = "Ann";
                customer.LastName = "Devon";
                customer.Company = "Eastern Connection";
            }
        }
        ObjectSpace.CommitChanges();
    }
    //...
}
```
In the code above, the Object Space is used to create initial data. This is one of the main framework abstractions that allows you to perform CRUD (create-read-update-delete) operations.

> **Note:** You can refer to Supply Initial Data for more information on how to initially populate the database.

### Run the Application

Press **Start Debugging** or the **F5** key to run the application.

The following image shows the application’s auto-generated UI:


![251035891-1027caf5-0269-42d6-b06b-dabc9c93ddb7](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/f2dd61bb-5415-4251-a06f-eddf289d9806)
![251035891-1027caf5-0269-42d6-b06b-dabc9c93ddb7](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/06b04418-60c0-4ff8-9b0f-eb72f629f577)


XAF generates this UI for List and Detail Views with CRUD operations and other functionality (view, search, etc.). The Detail View contains editors (text box, memo, drop-down box, image and date picker, etc.) that display different business class properties.

Lookup and collection editors display properties that are part of an association. For example, the **Project** and **ProjectTask** classes participate in a **One-To-Many** relationship. The editor for the “Many” part (the Project‘s Tasks property) allows users to add, edit, remove, and export tasks.

To display reference properties (the **ProjectTask**‘s **AssignedTo** property), XAF generates a drop-down list of persons in the UI and creates a foreign key that references the **Person** table in the database. This drop-down list displays a person’s full names because the **FullName** property is the default property of the **Person** class.

### Auto-Created Database

The database is automatically created based on your data model. The database columns are generated based on the persistence settings specified in the data model (such as field size set via an attribute). The image below shows the **Object Explorer** window from the **SQL Server Management Studio**.

![251036471-2e004707-80a7-4aad-a706-8a9a27f203a5](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/e7e6e729-92b7-43c3-8461-7829b71fe853)


The applications’ navigation control contains items for each database table. These navigation items allow a user to navigate to a List View with records and open their Detail Views.


## Customize the Application UI and Behavior

In XAF, the data model defines the database structure and UI. Changes to your persistent classes affect the UI. For example, if you add a new property to a business class, a new editor is added to the list and detail forms.

You can use the auto-generated UI or customize it according to your business requirements and scenarios. This topic describes how to customize your application’s appearance and behavior.

### Customize the Application UI Metadata

### *Use Attributes in Code*

Built-in attributes allow you to edit the Application Model, create controls, and customize the application’s appearance and behavior (validation, fields’ visibility and formatting, etc.) in the Business Model‘s code. With this declarative approach, you can add only one line of code without using the model editor or creating Controllers.

Apply the `SizeAttribute` to the **Testimonial**‘s **Quote** property and pass **Unlimited** as the attribute’s parameter to replace a single-line editor with a multi-line editor.

```csharp
public class Testimonial {
    // ...
    string quote;
    [Size(SizeAttribute.Unlimited)]
    public string Quote {
        get { return quote; }
        set { SetPropertyValue(nameof(Quote), ref quote, value); }
    }
    // ...
}
```

Run the ASP.NET Core Blazor application and open the **Testimonial** Detail View. The following image illustrates the standard and customized UI:

![251037209-77619135-0720-4e26-88ee-799517321f49](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/c3848fcd-d4d0-4917-a297-d661bb638b45)


Note that this approach adds a dependency from XAF assemblies to your data access layer (DAL).

### *Use the Model Editor*

Data model settings are exported to the application’s metadata (Application Model). If you do not want to define the application’s UI structure and behavior in your data model code, edit the application metadata in the Model Editor. Each project stores metadata settings as XML markup in **.xafml files.* These files form the Application Model’s layered structure.
Follow the steps below to change the Customer business object’s image and enable images in the navigation control via the Model Editor:

1. In the **Solution Explorer**, right-click the* SimpleProjectManager.Module* project and select Open **Model Editor** in the context menu or double-click the file with the *XAFML* extension.
2. In the **Model Editor**, navigate to the **BOModel | Customer** node in the tree and set the `ObjectCaptionFormat` property to **{0:FullName}**.

![251037797-2d2b5062-c3a9-4b16-abd6-cda4cb4a48c2](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/ff0fd9d2-07b6-4e81-8ffd-b313c58233b7)


The image below illustrates the result. The **Customer** Detail View displays the **FullName** property value in the caption.

![251037209-77619135-0720-4e26-88ee-799517321f49](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/158b5833-c788-4eb8-a0fa-37330985fdf7)


### Define Custom Logic and UI Elements

The Model Editor and built-in attributes allow you to change the options of the UI element and control. Other changes can be implemented only in code. For example, you can use the Controllers and Actions mechanism to replace the application’s default UI parts or implement custom business logic.

A Controller is a component that you can use to change the application flow, customize UI elements, and implement custom user interaction. Controllers can also include Actions. Actions are displayed in the UI as interactive elements (buttons, menu items, etc.) and execute custom business logic.

Follow the steps below to implement a `SimpleAction` that allows a user to mark the selected **Project Tasks** as completed and sets the **EndDate** property to the current date and time:
1. In the **Solution Explorer**, right-click the *SimpleProjectManager.Module\Controllers* folder and select **Add | Class…** in the context menu. Set the class name to **ProjectTaskController**.
2. Replace the created class code with the following:

```csharp
using System;
using DevExpress.Data.Filtering;
using DevExpress.ExpressApp;
using DevExpress.ExpressApp.Actions;
using SimpleProjectManager.Module.BusinessObjects.Planning;

namespace SimpleProjectManager.Module.Controllers {
    public class ProjectTaskController : ViewController {
        public ProjectTaskController() {
            TargetObjectType = typeof(ProjectTask);
            TargetViewType = ViewType.Any;
            SimpleAction markCompletedAction = new SimpleAction(
                this, "MarkCompleted",
                DevExpress.Persistent.Base.PredefinedCategory.RecordEdit){
                    TargetObjectsCriteria = 
                    (CriteriaOperator.Parse("Status != ?",ProjectTaskStatus.Completed)).ToString(),
                    ConfirmationMessage =
                            "Are you sure you want to mark the selected task(s) as 'Completed'?",
                    ImageName = "State_Task_Completed"
                };
            markCompletedAction.SelectionDependencyType = SelectionDependencyType.RequireMultipleObjects;
            markCompletedAction.Execute += (s, e) => {
                foreach(ProjectTask task in e.SelectedObjects) {
                    task.EndDate = DateTime.Now;
                    task.Status = ProjectTaskStatus.Completed;
                    View.ObjectSpace.SetModified(task); 
                }
                View.ObjectSpace.CommitChanges();
                View.ObjectSpace.Refresh();
            };
        }
    }
}
```

The image below shows the MarkCompleted Action in the ASP.NET Core Blazor application.

![251038767-0b663f2a-2551-4629-bbce-ce3d44d562e9](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/dcd0b3da-ec2b-40fc-9357-499395f9906e)


The **MarkCompleted** Action iterates the selected objects, modifies their properties, commits changes to the database, and refreshes the screen.

Alternatively, you can …

* implement the generic `ObjectViewController<ViewType, ObjectType>` instead of the `ViewController`. For the **ObjectViewController**, you can specify the View’s and object’s type this Controller should be activated for in the generic **ViewType** and **ObjectType** parameters: Define the Scope of Controllers and Actions.
* use the `ActionAttribute` to create an action directly from a business class method.


## Reuse Implemented Functionality

This topic describes how to add additional modules and business objects from an external library to extend the application’s functionality.

1. In the **Solution Explorer**, right-click the **SimpleProjectManager.Blazor.Server** project and select **Manage NuGet Packages**. In the invoked **NuGet Package Manager**, choose the **DevExpress 2x.x** Local package source and install the **DevExpress.ExpressApp.Validation** and **DevExpress.ExpressApp.Validation.Blazor** NuGet packages.

![251039437-ef0be94f-82ef-4dba-b70b-95a638ea919a](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/9560900a-ae7b-4f71-8225-108a5c2dc4c1)


2. Open the *SimpleProjectManager.Blazor.Server\Module.cs* file and add the following code to the Module constructor:

```csharp
using DevExpress.ExpressApp.Validation;
// ...
namespace SimpleProjectManager.Blazor.Server {
    public sealed partial class SimpleProjectManagerBlazorModule : ModuleBase {
        public SimpleProjectManagerBlazorModule() {
            // ...
            RequiredModuleTypes.Add(typeof(ValidationModule));
        }
    }
}
```

3. Open the *SimpleProjectManager.Module\BusinessObjects\Planning.cs* file and apply the `RuleCriteriaAttribute` to the **ProjectTask** class:

```csharp
using DevExpress.Persistent.Validation;
// ...
[RuleCriteria("EndDate >= StartDate", 
    CustomMessageTemplate = "Start Date must be less than End Date")]
public class ProjectTask : BaseObject {
    // ...
}
```

4. Run the ASP.NET Core Blazor application and create several project tasks. The added module validates project tasks according to the specified settings.

![251039835-c8c91a62-5726-45f5-9764-1deb43500dd6](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/6c1449c0-6c1a-4e99-bcd4-4c6c10b2d743)



### Data Models from External Libraries

You can add a business class to your application from the **Business Class** Library. XAF generates UI elements according to this class’ structure. The following steps show how to add the **Person** class from the **Business Class** Library and create the **Employee** navigation item to display **Person** objects in a list.

1. Open the *SimpleProjectManager.Module\Module.cs* file and add the following code to the Module constructor:

```csharp
using DevExpress.Persistent.BaseImpl;
// ...
namespace SimpleProjectManager.Module {
    public sealed partial class SimpleProjectManagerModule : ModuleBase {
        public SimpleProjectManagerModule() {
            // ...
            AdditionalExportedTypes.Add(typeof(Person));
        }
    }
}
```

2. Invoke the **Model Editor** for the **SimpleProjectManager.Module** project and navigate to the **NavigationItems | Items | Planning | Items** node. Create a new navigation item and set its **Caption** property to “Employee” and **View** to “Person_ListView”.
 
![251040328-73970991-8242-42b9-bafb-944bf688c715](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/a0ef55f1-a521-4e18-9b18-fffb312eabf2)


3. Run the application. The navigation control shows the new item in the **Planning** section.

![251040694-389405ce-2ea8-42df-82a4-c0e8a63584e4](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/84e723c5-3578-478b-ad0f-bc652f3f0510)


> **Note:** You can also use third-party modules﻿ or create your own reusable modules for use in multiple XAF applications.
