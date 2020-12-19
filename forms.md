# Forms

To add the form to the page use the Blazor  Edit form component

```text
<!--Telling form about model to bind to-->
<EditForm Model="Model" OnValidSubmit="HandleValidSubmit">
    <!--Binding model property to form-->
    <InputText  @bind-Value="Model.Title" id="title" class="form-control"></InputText>
    <button type="submit" class="btn btn-primary">Save</button>
</EditForm>
```

Adding bootstrap for better appearance

```text
    <EditForm Model="Model" OnValidSubmit="HandleValidSubmit">

        <div class="form-group row">
            <label for="title" class="col-sm-2 col-form-label">Title</label>
            <div class="col-sm-10">
                <InputText id="title" @bind-Value="Model.Title" class="form-control" />
            </div>
        </div>
    </EditForm>
    
```



