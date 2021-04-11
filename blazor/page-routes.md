# Page Routes / Navlinks

*  Pages have @page directive  @page"/" 

```text
#Simpler Anchor Tag

    <nav class="my-2 my-md-0 mr-md-3">
        <a class="p-2 text-light" href="/backlog">backlog</a>
        
        #navlink
        <NavLink class="p-2 text-light" href="/backlog">Backlog</NavLink>
 
    </nav>
```

* Navlink helps style differently since active tag\(in .css\) of link are automatically identified
* Multiple page routes landing to the same page  

```text
@page "/backlog"
@page "/backlog/me"
```

#### Navigation manger

* Using Depedency Injection \(Markup\)

Example below to redirect to another page upon reload

#### Dependency Injection

```text
@page "/"
@inject NavigationManager NavManager

<!--Inject driective/ NavigationManager instance with property NavManager  -->



<div>
    <h1>@Name</h1>
    <input @bind-value="Name" />
    <button @onclick="@(e => updateName("Yadav"))">Update Name</button>
</div>



@code {

    protected override async Task OnInitializedAsync()
    {
        NavManager.NavigateTo("/backlog");
    }



}
```

* Using Property for NavManager

```text
@page "/"


<!--Inject driective/ NavigationManager instance with property NavManager  -->



<div>
    <h1>@Name</h1>
    <input @bind-value="Name" />
    <button @onclick="@(e => updateName("Yadav"))">Update Name</button>
</div>



@code {


 -   [Inject]
 -   public NavigationManager NavManager { get; set; }

    protected override async Task OnInitializedAsync()
    {
        NavManager.NavigateTo("/backlog");
    }



}
```



#### Injecting Services

Registering services in Blazor project

Example  :

```text
#startup.cs
#Singleton helps create instance without new keyword


services.AddSingleton<IPtUserRepository, PtUserRepository>(c => new PtUserRepository(tempDataContext));
services.AddSingleton<IPtItemsRepository, PtItemsRepository>(c => new PtItemsRepository(tempDataContext));
services.AddSingleton<IPtDashboardRepository, PtDashboardRepository>(c => new PtDashboardRepository(tempDataContext));
services.AddSingleton<IPtTasksRepository, PtTasksRepository>(c => new PtTasksRepository(tempDataContext));
 
```

It creates instance of that class that will be shared by entire application , and lives for the duration of the webserver live

Registering a  service 

```text
services.AddSingleton<PtItemsRepository>();
or 
services.AddTransient<PtItemsRepository>();
//created for 1 request instance and stays for life of that request

or
services.AddScoped<PtItemsRepository>();
// new instance created everytime

```

