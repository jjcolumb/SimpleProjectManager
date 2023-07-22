[![en]([https://img.shields.io/badge/lang-en-red.svg)](https://github.com/jjcolumb/SimpleProjectManager#readme)
# Tutorial básico de ASP.NET  Core Blazor (demostración de Simple Project Manager)

Este tutorial explica cómo crear una aplicación XAF que se utiliza dentro de un departamento de la empresa y se puede abrir en navegadores de escritorio y móviles. Utiliza los controles de interfaz de usuario  **DevExpress ASP.NET Core Blazor**  para la presentación de datos y  **DevExpress XPO**  para el acceso a los datos.

![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/39f7251d-00ed-469c-98f7-a57629b66383)

Esta aplicación ASP.NET Core Blazor se puede utilizar en los siguientes escenarios:

-   un usuario puede  _ver_,  _buscar_,  _crear_,  _actualizar_  y  _eliminar_  empleados, proyectos y datos de tareas;
-   Un usuario puede  _ver_,  _buscar_,  _crear_,  _actualizar_  y  _eliminar_  clientes y comentarios sobre un producto para organizar y proporcionar datos para un sitio web promocional.

En este tutorial, escribirá el código independiente de la plataforma que afecta a los aspectos de la aplicación que no son específicos de la plataforma ASP.NET Core Blazor. XAF genera automáticamente pantallas de interfaz de usuario y especifica el acceso a la base de datos.

## Dependencias y requisitos previos

Antes de comenzar el tutorial, lea esta sección y asegúrese de que se cumplen las siguientes condiciones:

1.  [Visual Studio 2022 v17.0+](https://visualstudio.microsoft.com/) (con la carga de trabajo de desarrollo ASP.NET y web) está instalado en el equipo. Tiene experiencia básica en el desarrollo de .NET Framework en este IDE.
2.  [.NET 6 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/6.0) está instalado en el equipo.
3.  Una versión de  [prueba  gratuita de 30 días](https://www.devexpress.com/products/try/)  o una versión con licencia de  [DevExpress Universal Subscription](https://www.devexpress.com/Subscriptions/Universal.xml) está instalada en su equipo.
4.  Tiene conocimientos básicos de los conceptos de  [asignación relacional de objetos (ORM)](https://en.wikipedia.org/wiki/Object-relational_mapping) y  [DevExpress XPO](https://www.devexpress.com/products/net/orm/).
5.  Cualquier  [RDBMS](https://en.wikipedia.org/wiki/Relational_database_management_system) compatible con la herramienta XPO ORM (consulte Sistemas de bases de datos  [compatibles con XPO)](https://docs.devexpress.com/XPO/2114/product-information/database-systems-supported-by-xpo?v=22.1)  se instala y se puede acceder a él desde el equipo para almacenar los datos de la aplicación (se recomienda una instancia de LocalDB o SQL Server Express).
6.  Está familiarizado con la  [arquitectura de aplicaciones XAF](https://docs.devexpress.com/eXpressAppFramework/112559/overview/architecture?v=22.1).

## Lecciones del tutorial

1.  Crear una aplicación XAF: cree una aplicación ASP.NET Core Blazor  [XAF](https://docs.devexpress.com/eXpressAppFramework/401944/getting-started/basic-tutorial-blazor/create-an-xaf-application-blazor?v=22.1)  y especifique sus cadenas de conexión.
2.  Definir el modelo de datos  [y las relaciones: defina el modelo de datos](https://docs.devexpress.com/eXpressAppFramework/401953/getting-started/basic-tutorial-blazor/define-the-data-model-and-set-the-initial-data-blazor?v=22.1)  que sirve como base para la interfaz de usuario CRUD de la aplicación.
3.  Personalizar la interfaz de usuario y el comportamiento de la aplicación: personalice la estructura y los metadatos de la  [interfaz de](https://docs.devexpress.com/eXpressAppFramework/401954/getting-started/basic-tutorial-blazor/customize-the-application-ui-and-behavior-blazor?v=22.1)  usuario generada automáticamente e implemente la interacción personalizada del usuario.
4.  [Reutilizar la funcionalidad implementada](https://docs.devexpress.com/eXpressAppFramework/401955/getting-started/basic-tutorial-blazor/reuse-implemented-functionality-blazor?v=22.1): agregue módulos a sus aplicaciones para habilitar funcionalidad adicional.

## Aprende más

-   Lea  [las preguntas frecuentes - Blazor UI (FAQ)](https://docs.devexpress.com/eXpressAppFramework/403277/support-qa-troubleshooting/frequently-asked-questions-blazor-faq?v=22.1)
-   Pruebe  [las demostraciones  de XAF](https://www.devexpress.com/support/demos/).
-   Visite la  [página  de inicio de XAF](https://www.devexpress.com/Products/NET/Application_Framework/)  .
-   Siga el  [tutorial en profundidad (Aplicación Blazor)](https://docs.devexpress.com/eXpressAppFramework/402125/getting-started/in-depth-tutorial-blazor?v=22.1)


# Crear una aplicación XAF

En este tema se describe cómo utilizar el  [Asistente para soluciones](https://docs.devexpress.com/eXpressAppFramework/113624/installation-upgrade-version-history/visual-studio-integration/solution-wizard?v=22.1)  para crear una aplicación XAF y especificar su cadena de conexión.

## Crear las aplicaciones ASP.NET  Core Blazor

1.  En el menú principal de Visual Studio, seleccione  **Archivo**  |  **Nuevo**  |  **Proyecto...**  para invocar el cuadro de diálogo  **Crear un nuevo proyecto**.
    
2.  Seleccione  **DevExpress v22.1  XAF Template Gallery**  y haga clic en  **Siguiente**.
    
    ![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/03143aa0-70cb-4404-806c-3ba34441c418)

    
3.  Especifique el nombre del proyecto ("SimpleProjectManager") y haga clic en  **Crear**.
    
    ![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/e91bc71c-7a36-4f2f-a21d-0b3d6a8cd01a)

    
4.  En la Galería de plantillas invocada, seleccione  **Asistente para soluciones XAF (**.NET Core) en la sección .**NET Core**  y haga clic en  **Ejecutar asistente**.
    
    ![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/846d4743-c15e-42bf-ba67-666f082dbbce)

    
5.  Elija  **Web (ASP.NET Core Blazor)**  y haga clic en  **Siguiente**.
    
    ![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/1d5ffc34-2766-4617-bd14-cbd5e40e2d50)

    
6.  Elija  **eXpress Objetos persistentes**  y haga clic en  **Siguiente**.
    
    ![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/88303c5c-2a4b-4d18-a7ad-58f811e5db9f)

    
    >NOTA
    Puede utilizar [Entity Framework Core](https://docs.microsoft.com/en-us/ef/core/) o [eXpress Persistent Objects (XPO) como herramienta de asignación relacional de objetos (ORM)  ](https://www.devexpress.com/Products/NET/ORM/)[  ](https://en.wikipedia.org/wiki/Object-relational_mapping)del proyecto . En este tutorial se muestra el enfoque basado en  **XPO**.
    
7.  Ahora puede elegir opciones de seguridad para su aplicación.  **Elija Ninguno**  como tipo de  **autenticación**. Este tutorial no muestra cómo utilizar el  [sistema de seguridad](https://docs.devexpress.com/eXpressAppFramework/113366/data-security-and-safety/security-system?v=22.1)  XAF. Haga clic en  **Finalizar**.
    
    ![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/579684e9-c99f-4770-acea-43e5f61814ad)

    

El Asistente para soluciones crea una solución con los siguientes proyectos:

![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/44d00e2b-eda0-427c-ae7e-139dfe546924)


Consulte el tema  [Estructura de soluciones de aplicaciones](https://docs.devexpress.com/eXpressAppFramework/118045/application-shell-and-base-infrastructure/application-solution-components/application-solution-structure?v=22.1)  para obtener más información sobre los proyectos de una solución XAF.

## Especificar la conexión de base de datos

El asistente conecta la aplicación a la base de datos de  **Microsoft SQL Server**  con la siguiente cadena de conexión:

`"Integrated Security=SSPI;Pooling=false;Data Source=(localdb)\\mssqllocaldb;Initial Catalog=SimpleProjectManager"`

Puede modificar esta cadena de conexión en el archivo  _SimpleProjectManager.Blazor.Server\appsettings.json_  (consulte el elemento  **connectionStrings**). Consulte el tema  [Conectar una aplicación XAF a un proveedor de base de datos](https://docs.devexpress.com/eXpressAppFramework/113155/business-model-design-orm/connect-an-xaf-application-to-a-database-provider?v=22.1)  para obtener más información.

En esta etapa, puede ejecutar las aplicaciones ASP.NET Core Blazor con navegación, menú y otros elementos de interfaz de usuario creados automáticamente para aplicaciones de línea de negocio (LOB). Sin embargo, el modelo de datos y la lógica aún no están definidos, lo que se implementa en los siguientes temas.


# Definir el modelo de datos y establecer los datos iniciales


En este tema se describe cómo definir el modelo de datos y la lógica empresarial para la aplicación ASP.NET Core Blazor. El modelo de datos de la aplicación contiene dos partes lógicas:

-   Marketing: las clases  **de Cliente**  y  **Testimonio**
-   Planeación: las clases  **Project**  y  **Task**

## Agregar las clases persistentes de clientes y testimonios

1.  En el  **Explorador de soluciones**, haga clic con el botón secundario en la carpeta  _SimpleProjectManager.Module\BusinessObjects_  y seleccione  **Agregar**  |  **Clase...**  desde el menú contextual. Establezca el nombre en "Marketing" y haga clic en  **Agregar**.
    
2.  Reemplace el contenido del archivo generado automáticamente con el código siguiente:
    

    
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
    

    

## Agregar las clases persistentes Proyecto y Tarea de proyecto

1.  En el  **Explorador de soluciones**, haga clic con el botón secundario en la carpeta  _SimpleProjectManager.Module\BusinessObjects_  y seleccione  **Agregar**  |  **Clase...**  desde el menú contextual. Establezca el nombre en "Planificación" y haga clic en  **Agregar**.
    
2.  Reemplace el contenido del archivo generado automáticamente con el código siguiente:
    

    
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
    

    

## Rellenar la base de datos con datos iniciales

Abra el archivo Updater.cs de la carpeta  _Actualización de base de datos_  del proyecto SimpleProjectManager.Module y reemplace el método  [ModuleUpdater.UpdateDatabaseAfterUpdateSchema](https://docs.devexpress.com/eXpressAppFramework/DevExpress.ExpressApp.Updating.ModuleUpdater.UpdateDatabaseAfterUpdateSchema?v=22.1)  como se muestra a continuación:


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

En el código anterior, el  [espacio de objetos](https://docs.devexpress.com/eXpressAppFramework/113707/data-manipulation-and-business-logic/object-space?v=22.1)  se utiliza para crear datos iniciales. Esta es una de las principales abstracciones del marco que le permite realizar operaciones CRUD (crear-leer-actualizar-eliminar).

>NOTA
>Puede consultar [Proporcionar datos iniciales](https://docs.devexpress.com/eXpressAppFramework/402170/getting-started/in-depth-tutorial-blazor/business-model-design/business-model-design-with-xpo/supply-initial-data-xpo?v=22.1) para obtener más información sobre cómo rellenar inicialmente la base de datos.

## Ejecutar la aplicación

Presione  **Iniciar depuración**  o la tecla  **F5**  para ejecutar la aplicación.

La siguiente imagen muestra la interfaz de usuario generada automáticamente de la aplicación:
![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/8e026f0a-1d3e-424b-b53d-31069807ae1c)


XAF genera esta interfaz de usuario para vistas de lista y detalles con operaciones CRUD y otras funcionalidades (vista, búsqueda, etc.). La vista detallada contiene editores (cuadro de texto, nota, cuadro desplegable, selector de imagen y fecha, etc.) que muestran  [diferentes propiedades de clase empresarial](https://docs.devexpress.com/eXpressAppFramework/113014/business-model-design-orm/data-types-supported-by-built-in-editors?v=22.1).

Los editores de búsqueda y colección muestran propiedades que forman parte de una asociación. Por ejemplo, las clases Project y  **ProjectTask**  participan en una  [relación de uno a muchos](https://docs.devexpress.com/eXpressAppFramework/112654/business-model-design-orm/business-model-design-with-xpo/relationships-between-persistent-objects-in-code-and-ui?v=22.1#onetomanyaggregated).  El editor de la parte "Muchas" (propiedad  **Tareas**  del  **proyecto**) permite a los usuarios agregar, editar, quitar y exportar tareas.

Para mostrar  [las propiedades](https://docs.devexpress.com/eXpressAppFramework/113572/business-model-design-orm/data-types-supported-by-built-in-editors/reference-foreign-key-complex-type-properties?v=22.1)  de referencia (la propiedad  **AssignedTo**  de  **ProjectTask**), XAF genera una lista desplegable de personas en la interfaz de usuario y crea una  _clave externa_  que hace referencia a la tabla  **Person**  de la base de datos. Esta lista desplegable muestra los nombres completos de una persona porque la propiedad  **FullName**  es la propiedad predeterminada de la clase  **Person**  (vea  [Propiedad predeterminada de una clase Business](https://docs.devexpress.com/eXpressAppFramework/113525/business-model-design-orm/how-to-specify-a-display-member-for-a-lookup-editor-detail-form-caption?v=22.1#default-property-of-a-business-class)).

>NOTA
Puede encontrar más información sobre la generación de la interfaz de usuario en los temas  Generación de columnas de vista de lista  y [Generación de diseño de elementos de vista](https://docs.devexpress.com/eXpressAppFramework/113680/ui-construction/views/layout/view-items-layout-generation?v=22.1).[](https://docs.devexpress.com/eXpressAppFramework/113285/ui-construction/views/layout/list-view-column-generation?v=22.1)

## Base de datos creada automáticamente

La base de datos se crea automáticamente en función del modelo de datos. Las columnas de la base de datos se generan en función de la configuración de persistencia especificada en el modelo de datos (como el tamaño de campo establecido mediante un atributo). La imagen siguiente muestra la ventana  **Explorador de objetos**  de  **SQL Server Management Studio**.

![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/7c1b1738-5d35-4987-948c-1b345025c677)


El control de navegación de las aplicaciones contiene elementos para cada tabla de base de datos. Estos elementos de navegación permiten al usuario navegar a una vista de lista con registros y abrir sus vistas de detalle.


# Personalizar la interfaz de usuario y el comportamiento de la aplicación


En XAF, el modelo de datos define la estructura de la base de datos y la interfaz de usuario. Los cambios en las clases persistentes afectan a la interfaz de usuario. Por ejemplo, si agrega una nueva propiedad a una clase empresarial, se agrega un nuevo editor a los formularios de lista y detalle.

Puede usar la interfaz de usuario generada automáticamente o personalizarla según los requisitos y escenarios de su negocio. En este tema se describe cómo personalizar la apariencia y el comportamiento de la aplicación.

## Personalizar los metadatos de la interfaz de usuario de la aplicación

### Usar atributos en código

[Los atributos integrados](https://docs.devexpress.com/eXpressAppFramework/112701/business-model-design-orm/data-annotations-in-data-model?v=22.1)  permiten editar el modelo de aplicación, crear controles y personalizar la apariencia y el comportamiento de la  [aplicación](https://docs.devexpress.com/eXpressAppFramework/112579/ui-construction/application-model-ui-settings-storage?v=22.1)  (validación, visibilidad y formato de los campos, etc.) en el código del modelo de  [negocio](https://docs.devexpress.com/eXpressAppFramework/113664/business-model-design-orm?v=22.1). Con este enfoque declarativo, solo puede agregar una línea de código sin usar  [el editor de modelos](https://docs.devexpress.com/eXpressAppFramework/401954/getting-started/basic-tutorial-blazor/customize-the-application-ui-and-behavior-blazor?v=22.1#use-the-model-editor)  ni crear  [controladores](https://docs.devexpress.com/eXpressAppFramework/401954/getting-started/basic-tutorial-blazor/customize-the-application-ui-and-behavior-blazor?v=22.1#define-custom-logic-and-ui-elements).

Aplique  [SizeAttribute](https://docs.devexpress.com/XPO/DevExpress.Xpo.SizeAttribute?v=22.1)  a la propiedad  **Quote**  del  **testimonio**  y pase  **Unlimited**  como parámetro del atributo para reemplazar un editor de una sola línea por un editor de varias líneas.



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

Ejecute la aplicación ASP.NET Core Blazor y abra la Vista de detalles de  **testimonios**. La siguiente imagen ilustra la interfaz de usuario estándar y personalizada:

![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/d0e94df8-246a-441b-b310-2c0744574c65)


Tenga en cuenta que este enfoque agrega una dependencia de los ensamblados XAF a la  [capa de acceso a datos (DAL).](https://docs.devexpress.com/XPO/2123/connect-to-a-data-store?v=22.1#data-access-layer)

### Usar el Editor de modelos

La configuración del modelo de datos se exporta a los metadatos de la aplicación ([modelo de aplicación](https://docs.devexpress.com/eXpressAppFramework/112579/ui-construction/application-model-ui-settings-storage?v=22.1)). Si no desea definir la estructura y el comportamiento de la interfaz de usuario de la aplicación en el código del modelo de datos, edite los metadatos de la aplicación en el  [Editor de modelos](https://docs.devexpress.com/eXpressAppFramework/112582/ui-construction/application-model-ui-settings-storage/model-editor?v=22.1). Cada proyecto almacena la configuración de metadatos como marcado XML en archivos  _*.xafml._  Estos archivos forman la  [estructura en capas](https://docs.devexpress.com/eXpressAppFramework/403527/ui-construction/application-model-ui-settings-storage/change-application-model?v=22.1)  del modelo de aplicación.

Siga los pasos a continuación para cambiar la imagen del objeto de negocio  **Cliente**  y habilitar imágenes en el control de navegación a través del Editor de modelos:

1.  En el  **Explorador de soluciones**, haga clic con el botón secundario en el proyecto  **SimpleProjectManager.Module**  y seleccione  **Abrir editor de modelos**  en el menú contextual o haga doble clic en el archivo con la extensión XAFML.
2.  En el Editor de modelos, desplácese hasta  **BOModel**  |  **Cliente**  en el árbol y establezca la propiedad  [ObjectCaptionFormat](https://docs.devexpress.com/eXpressAppFramework/DevExpress.ExpressApp.Model.IModelClass.ObjectCaptionFormat?v=22.1)  en  **{0:FullName}**.
    
    ![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/cbdeabd8-26d3-4f8f-908e-d93bbe7c0165)

    

La siguiente imagen ilustra el resultado. La vista Detalles  **del cliente**  muestra el valor de la propiedad  **FullName**  en el título.



## Definir lógica personalizada y elementos de interfaz de usuario

El Editor de modelos y los atributos integrados permiten cambiar las opciones del elemento y el control de la interfaz de usuario. Otros cambios solo se pueden implementar en el código. Por ejemplo, puede usar el mecanismo Controladores y  [acciones](https://docs.devexpress.com/eXpressAppFramework/112622/ui-construction/controllers-and-actions/actions?v=22.1)  para reemplazar los elementos de interfaz de usuario  [predeterminados de](https://docs.devexpress.com/eXpressAppFramework/112621/ui-construction/controllers-and-actions/controllers?v=22.1)  la aplicación o implementar lógica empresarial personalizada.

Un controlador es un componente que puede usar para cambiar el flujo de la aplicación, personalizar los elementos de la interfaz de usuario e implementar la interacción personalizada del usuario. Los controladores también pueden incluir  [acciones](https://docs.devexpress.com/eXpressAppFramework/112622/ui-construction/controllers-and-actions/actions?v=22.1). Las acciones se muestran en la interfaz de usuario como elementos interactivos (botones, elementos de menú, etc.) y ejecutan lógica empresarial personalizada.

Siga los pasos siguientes para implementar una  [acción simple](https://docs.devexpress.com/eXpressAppFramework/DevExpress.ExpressApp.Actions.SimpleAction?v=22.1)  que permita a un usuario marcar las tareas de  **proyecto**  seleccionadas como completadas y establezca la propiedad  **EndDate**  en la fecha y hora actuales:

1.  En el  **Explorador de soluciones**, haga clic con el botón secundario en la carpeta  **SimpleProjectManager.Module\Controllers**  y seleccione  **Agregar**  |  **Clase...**  en el menú contextual. Establezca el nombre de clase en  **ProjectTaskController**.
2.  Reemplace el código de clase creado por el siguiente:
    

    
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
    


La siguiente imagen muestra la acción  **MarkCompleted**  en la aplicación ASP.NET Core Blazor.

![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/b469c00a-c009-4d45-8806-9e9e50e8467f)


La acción  **MarkCompleted**  itera los objetos seleccionados, modifica sus propiedades, confirma los cambios en la base de datos y actualiza la pantalla.

Alternativamente, puede ...

-   implementar el  [ObjectViewController<ViewType genérico, ObjectType>](https://docs.devexpress.com/eXpressAppFramework/DevExpress.ExpressApp.ObjectViewController-2?v=22.1)  en lugar del  [ViewController](https://docs.devexpress.com/eXpressAppFramework/DevExpress.ExpressApp.ViewController?v=22.1). Para  **ObjectViewController**, puede especificar el tipo de vista y objeto para el que se debe activar este controlador en los parámetros genéricos  **ViewType**  y  **ObjectType**:  [Definir el ámbito de los controladores y las acciones](https://docs.devexpress.com/eXpressAppFramework/113103/ui-construction/controllers-and-actions/define-the-scope-of-controllers-and-actions?v=22.1).
-   utilice  [ActionAttribute](https://docs.devexpress.com/eXpressAppFramework/DevExpress.Persistent.Base.ActionAttribute?v=22.1)  para crear una acción directamente desde un método de clase empresarial. Consulte el tema  [Agregar una acción simple mediante un atributo](https://docs.devexpress.com/eXpressAppFramework/112731/getting-started/in-depth-tutorial-winforms-webforms/extend-functionality/add-a-simple-action-using-an-attribute?v=22.1)  para obtener más información.


# Reutilizar la funcionalidad implementada

En este tema se describe cómo agregar  [módulos y](https://docs.devexpress.com/eXpressAppFramework/118046/application-shell-and-base-infrastructure/application-solution-components/modules?v=22.1#modules-shipped-with-xaf)  objetos de negocio adicionales desde una biblioteca externa para ampliar la funcionalidad de la aplicación.

## Módulos XAF Extra

Siga los pasos que se indican a continuación para agregar el  [módulo Validación](https://docs.devexpress.com/eXpressAppFramework/113684/validation-module?v=22.1)  y configurar reglas de validación para objetos de negocio.

1.  En el  **Explorador de soluciones**, haga clic con el botón secundario en el proyecto  **SimpleProjectManager.Blazor.Server**  y seleccione  **Administrar paquetes NuGet.**  En el Administrador de paquetes NuGet invocado, elija el origen del paquete local DevExpress  **22.1**  e instale los  **paquetes NuGet**  DevExpress.ExpressApp.Validation y  **DevExpress.ExpressApp.Validation.Blazor.**
    
    ![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/b7e6a571-c4db-4d02-9aa7-31391375cb14)

    
2.  Abra el archivo  _SimpleProjectManager.Blazor.Server_\Module.cs y agregue el código siguiente al constructor  _Module_:
    

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
    
3.  Abra el archivo  _SimpleProjectManager.Module\BusinessObjects\Planning.cs_  y aplique  [RuleCriteriaAttribute](https://docs.devexpress.com/eXpressAppFramework/DevExpress.Persistent.Validation.RuleCriteriaAttribute?v=22.1)  a la clase  **ProjectTask**:
    

    
    ```csharp
    using DevExpress.Persistent.Validation;
    // ...
    [RuleCriteria("EndDate >= StartDate", 
        CustomMessageTemplate = "Start Date must be less than End Date")]
    public class ProjectTask : BaseObject {
        // ...
    }
    
    ```
    
4.  Ejecute la aplicación ASP.NET Core Blazor y cree varias tareas de proyecto. El módulo agregado valida las tareas del proyecto de acuerdo con la configuración especificada.
    
    ![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/e1ed39ce-bf6f-4678-afa8-fd67e1d7c6fc)

    

## Modelos de datos de bibliotecas externas

Puede agregar una clase empresarial a la aplicación desde la  [biblioteca de clases empresariales](https://docs.devexpress.com/eXpressAppFramework/112571/business-model-design-orm/built-in-business-classes-and-interfaces?v=22.1). XAF genera elementos de interfaz de usuario de acuerdo con la estructura de esta clase. Los pasos siguientes muestran cómo agregar la clase Person desde la biblioteca de  **clases empresariales**  y crear el elemento de navegación  **Employee**  para mostrar objetos  **Person**  en una lista.

1.  Abra el archivo  _SimpleProjectManager.Module_\Module_.cs_  y agregue el código siguiente al constructor Module:

    
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
    
2.  Invoque el  **Editor de modelos**  para el proyecto  _SimpleProjectManager.Module_  y navegue hasta  **NavigationItems**  |  **Artículos**  |  **Planificación**  |  **Nodo Elementos**. Cree un nuevo elemento de navegación y establezca su propiedad  **Caption**  en "Employee" y  **View**  en "Person_ListView". Consulte el tema Agregar un elemento  [al control de](https://docs.devexpress.com/eXpressAppFramework/112749/getting-started/in-depth-tutorial-winforms-webforms/ui-customization/add-an-item-to-the-navigation-control?v=22.1)  navegación para obtener más información sobre cómo agregar un elemento de navegación.
    
    ![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/c2e1f504-9849-4479-b4fa-ebea64aff36d)

    
3.  Ejecute la aplicación. El control de navegación muestra el nuevo elemento en la sección  **Planeación**.
    
    ![image](https://github.com/jjcolumb/SimpleProjectManager/assets/126447472/45fadfa2-8841-4781-ac93-090a45b43af8)

    

>NOTA
>También puede utilizar módulos  [de terceros  o crear sus propios módulos](https://www.devexpress.com/products/net/application_framework/#community) reutilizables para utilizarlos en varias aplicaciones XAF.
