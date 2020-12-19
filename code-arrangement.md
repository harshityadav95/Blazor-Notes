# Code Arrangement

* **Separating the c\# code from the HTML and Class code , using code behind file**
*  To create a code behind file 

```text
-  right click on the main page folder on the Pages
-  Click on Add 
-  Click on Class
-  Create class with convention 
Index.razor.cs
nameOfComponent+cs(to indicate the C# file)
```

*  The c\# will automatically structure and and place the new class inside the page name automatically

```text
- Now in the created new class make that class as partial class
- Make the Class inherit from ComponentBase
- now all the code that was inside the c# block can  be inside it



```

* to navigate from a function to its code behind file press F12 in visual studio and it will take you to code behind file
* the Class file will look something lik

```text
# filename Index.razor.cs

using Microsoft.AspNetCore.Components;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;

namespace RPS.Web.Server.Pages
{
    public partial class Index: ComponentBase
    {
        public string Name { get; set; }
        public void updateName(string newName)
        {
            Name = newName;
        }
    }
}

```





