# Two way Binding



* Type in the box to bind its value to the variable as soon as it goes out of focus 

```text
@page "/"



<div>
    <h1>@Name</h1>
    <input @bind-value="Name" />
    <button @onclick="@(e => updateName("Yadav"))">Update Name</button>
</div>



@code {

    public string Name { get; set; }
    public void updateName(string newName)
    {
        Name = newName;
    }



}
```



