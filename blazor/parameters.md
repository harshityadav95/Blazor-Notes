# Parameters

*  Passing the parameter as argument in the URL and 

```text
@page "/backlog"
-@page "/backlog/{PresetParam}"



@using RPS.Web.Server.Components.Backlog;
@using RPS.Web.Server.Models;


<Items PresetParam="@PresetParam" />

@code {

-    [Parameter]
    public string PresetParam { get; set; } = "my";

}
```

*  Constraining the parameter type

```text
@page "/details/{Id:int}/{ScreenParam}"
```

