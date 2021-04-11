# Blazor Component Lifecycle Method

*  Blazor components have several life cycle methods. **OnInitializedAsync i**s the most common life cycle method. We are overriding this method to retrieve Employees data.

```text
protected override Task OnInitializedAsync()
{
        LoadEmployees();
        return base.OnInitializedAsync();
}
```

