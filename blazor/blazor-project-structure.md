# Blazor Project Structure

Files and folders in ASP.NET Core Blazor project

### Program.cs 

* This file contains the Main\(\) method which is the entry point for both the project types \(i.e Blazor WebAssembly and Blazor Server\). 
* In a **Blazor server project, the Main\(\) method calls CreateHostBuilder\(\)** method which sets up the ASP.NET Core host. 
* In a **Blazor WebAssembly project, the App component**, which is the root component of the application, is specified in the Main method. This root component is present in the root project folder in **App.razor** file.

Components are the building blocks of a Blazor application. 

![](../.gitbook/assets/image%20%282%29.png)

### wwwroot

* For both the project types, this folder contains the static files like images, stylesheets etc. 

### App.razor

```text
<Router AppAssembly="@typeof(Program).Assembly">
    <Found Context="routeData">
        <RouteView RouteData="@routeData"
        DefaultLayout="@typeof(MainLayout)" />
    </Found>
    <NotFound>
        <LayoutView Layout="@typeof(MainLayout)">
            <p>Sorry, there's nothing at this address.</p>
        </LayoutView>
    </NotFound>
</Router>
```

* This file is the application’s root component that manages client-side routing using the _Router_ component.
* The contents are the same for the _Blazor Server_ and _Blazor WebAssembly_ projects.
*  * The _Router_ component renders pages that match the requested address.
  * The router uses the _Found_ property to display content when a match is found.
  * If a match is not found, the _NotFound_ property is used to display the message, **`Sorry, there's nothing at this address`**.

### Pages folder

This folder contains the \_Host razor page and the routable components that make up the Blazor app. The components have the .razor extension.

* Index component \(Index.razor\) – Rendered when we navigate to the root application URL.
* Counter component \(Counter.razor\) – Rendered when we navigate to the path /counter.
* FetchData component \(FetchData.razor\) – Rendered when we navigate to the path /fetchdata.
* Error component \(Error.razor\) – Rendered when an unhandled exception occurs in the blazor app.

### Shared folder

* As the name implies, contains the shared components

### MainLayout component \(MainLayout.razor\)

* The application's main layout component

### NavMenu component \(NavMenu.razor\)

* Implements the navigation menu on the sidebar. NavLink component, renders navigation links to other Razor components like the index, counter and fetchdata components. This NavLink component is intelligent enough to highlight the navigation menu item, if it's component is currently displayed.

## File \_Imports.razor <a id="64a9"></a>

* The file contains a list of common namespaces using directives **`@using`**so that it doesn't have to include it in every razor component.
* Following are the contents of the file**`_Imports.razor`** in the _Blazor Server_ project.

```text
@using System.Net.Http
@using Microsoft.AspNetCore.Authorization
@using Microsoft.AspNetCore.Components.Authorization
@using Microsoft.AspNetCore.Components.Forms
@using Microsoft.AspNetCore.Components.Routing
@using Microsoft.AspNetCore.Components.Web
@using Microsoft.JSInterop
@using BlazorServerApp
@using BlazorServerApp.Shared
```

* Whereas in the _Blazor WebAssembly_ project, the contents of the file**`_Imports.razor`** are as follows.

```text
@using System.Net.Http
@using System.Net.Http.Json
@using Microsoft.AspNetCore.Components.Forms
@using Microsoft.AspNetCore.Components.Routing
@using Microsoft.AspNetCore.Components.Web
@using Microsoft.AspNetCore.Components.WebAssembly.Http
@using Microsoft.JSInterop
@using BlazorWebAssemblyApp
@using BlazorWebAssemblyApp.Shared
```

### 

## File wwwroot/index.html <a id="7b4b"></a>

* It is the root page in the ****_**Blazor WebAssembly**_ project, which is implemented as an HTML page.
* When the first request was made, this page was displayed in response.
* The page has standard HTML, HEAD, and BODY tags and specifies where the application’s root component, **`App.razor`** , must be provided.
* The page loads the **`_framework/blazor.webassembly.js`** file. This file is responsible for: - downloading compiled applications, dependencies, and .NET runtimes, - initializing the runtime to run Blazor applications in the browser.

### Startup.cs

* This file is present only in the Blazor Server project. As the name implies it contains the applications's startup logic. The Startup class contains the following two methods.
* **ConfigureServices** - Configures the applications DI i.e dependency injection services. For example AddServerSideBlazor\(\) method adds Blazor server side services. On the IServiceCollection interface there are several methods that start with the word Add. These methods add different services for the Blazor application. We can even add our own services to the DI container. We will see this in action in our upcoming videos.
* **Configure** - Configures the app's request processing pipeline. Depending on what we want the Blazor application to be capable of doing we add or remove the respective middleware components from request processing pipeline. For example, UseStaticFiles\(\) method adds the middleware component that can server static files like images, css etc.

## File Pages/`_Host.cshtml` <a id="55a1"></a>

* It is the root page in the _Blazor Server_ project, which is implemented as a razor page.
* When the first request is made, this page is displayed in response.
* The host page as HTML, HEAD, and BODY tags specifies where the application’s root component, **`App.razor`**, must be provided.
* The page loads the **`_framework/blazor.server.js`** file. This file is responsible for managing the real-time SignalR connection between the browser and the server. This connection is used to exchange information between clients and servers.

### Data folder \(Blazor Server\)

* Contains code files related to the sample WeatherForecast service

### appsettings.json \(Blazor Server\)

* Just like an asp.net core mvc project, a blazor project also uses this file to store the Configuration settings.

### 

