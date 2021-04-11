# Component Events

* Simple Button click event to display name when you click on it

```text
@page "/"

<div>
    <h1>@Name</h1>
    <button @onclick="updateName">Update Name</button>
</div>

@code {

    public string Name { get; set; }
    public void updateName()
    {
        Name = "Harshit";
    }


}
```

*  Passing an argument in the Event to the method

```text
@page "/"



<div>
    <h1>@Name</h1>
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



