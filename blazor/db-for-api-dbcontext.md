# DB for API DbContext

### Connecting the SQL Nuget package Manager to be installed

* Microsoft.EntityFrameworkCore.SqlServer
* Microsoft.EntityFrameworkCore.Tools

### Add the following string in the App config of the Project

Include the following database connection string in appsettings.json file of the REST API project.

```text
"ConnectionStrings": {
  "DBConnection": "server=(localdb)\\MSSQLLocalDB;database=EmployeeDB;Trusted_Connection=true"
}
```

## ASP.NET Core REST API DbContext

In this video we will discuss adding database support for ASP.NET Core REST API service. For this we are going to use Entity Framework Core.

### What is Entity Framework Core

Entity Framework Core is an ORM \(i.e an Object-Relational Mapper\). It's a complete rewrite from the ground up. If you have any experience with previous versions of Entity Framework, you will find lot of familiar features. 

EF core is lightweight, extensible, and open source software. Like .NET Core, EF Core is also cross platform. It works on windows, Mac OS, and Linux. EF core is Microsoft’s official data access platform.

### Entity Framework Core DbContext class

One of the very important classes in Entity Framework Core is the DbContext class. This is the class that we use in our application code to interact with the underlying database. It is this class that manages the database connection and is used to retrieve and save data in the database.

To use the DbContext class in our application

1. We create a class that derives from the DbContext class.
2. DbContext class is in Microsoft.EntityFrameworkCore namespace.

```text
// code that interact with the database
public class AppDbContext : DbContext
{ 

}
```

### DbContextOptions in Entity Framework Core

For the DbContext class to be able to do any useful work, it needs an instance of the DbContextOptions class.

The DbContextOptions instance carries configuration information such as the connection string, database provider to use etc.

We pass the DbContextOptions to the base DbContext class constructor using the base keyword as shown below.

```text
public class AppDbContext : DbContext
{
    // for connection string from appconfig.json
    public AppDbContext(DbContextOptions<AppDbContext> options)
        : base(options)
    {
    }
}
```

### Entity Framework Core DbSet

* The DbContext class includes a DbSet&lt;TEntity&gt; property for each entity in the model.
* At the moment in our application we have, 2 entity classes - Employee and Department.
* So in our AppDbContext class we have 2 corresponding DbSet properties.

```text
DbSet<Employee>
DbSet<Department>
```

* We will use these DbSet properties to query and save instances of Employee and Department classes.
* The LINQ queries against the DbSet properties will be translated into queries against the underlying database.

```text
public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options)
        : base(options) 
    {
    }

    public DbSet<Employee> Employees { get; set; }
    public DbSet<Department> Employees { get; set; }
}
```

* TO add some seed data to the above class we add overload function that makes it like this 

### Add SQL Server to the project 

Goto Startup.cs of the EmployeeManagement.api and add the following method to read connection string 

```text
public void ConfigureServices(IServiceCollection services)
{
    //this code need to be added
    services.AddDbContext<AppDbContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DBConnection")));
    
    // this is already present
    services.AddControllers();
}
```

Now , executing the database migration  

### Database Migration 

1. Launch the Nuget  Package manager command line in the visual studio \(make sure in the package manager terminal the Default project is the Api \) since the migration will only be made for the API project

```text
Add-Migration InitialCreate
```

After the migration is complete there will be a Migrations folder created in the API project , the file \(intialCreate\) contains our migration code 

* To update the Database 

```text
Update-Database
```

After the above is suceessfull goto    
View &gt; SQL server object explorer &gt; Database &gt; Employee Databased &gt;&gt; \(right click \) &gt;&gt; view data to view the data stored in the SQL object  



