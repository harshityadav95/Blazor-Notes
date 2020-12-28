# Loading Indicator

*  For delay in data retrieval by the time the page component is rendered could lead to many  problems , so using a load indicator until the data retrieval process is completed and can be displayed on the page .

1. Async the OnInitalizedAsunc\(
2.  If Else 

```text
// EmployeeListBase.cs

public class EmployeeListBase : ComponentBase
{
    public IEnumerable<Employee> Employees { get; set; }

    protected override async Task OnInitializedAsync()
    {
        await Task.Run(LoadEmployees);
    }

    private void LoadEmployees()
    {
        System.Threading.Thread.Sleep(2000);
        // Retrieve data from the server and initialize
        // Employees property which the View will bind
    }
}
```

```text
// EmployeeList.razor

@if (Employees == null)
{
    <div class="spinner"></div>
}
else
{
    <div class="card-deck">
        @foreach (var employee in Employees)
        {
            <div class="card m-3">
                <div class="card-header">
                    <h3>@employee.FirstName @employee.LastName</h3>
                </div>
                <img class="card-img-top imageThumbnail" 
                     src="@employee.PhotoPath" />
            </div>
        }
    </div>
}
```

```text
.spinner {
    border: 16px solid silver;
    border-top: 16px solid #337AB7;
    border-radius: 50%;
    width: 80px;
    height: 80px;
    animation: spin 700ms linear infinite;
    top: 40%;
    left: 55%;
    position: absolute;
}

@keyframes spin {
    0% {
        transform: rotate(0deg)
    }

    100% {
        transform: rotate(360deg)
    }
}
```



Reference 

*  [https://www.pragimtech.com/blog/blazor/blazor-loading-indicator/](https://www.pragimtech.com/blog/blazor/blazor-loading-indicator/)

