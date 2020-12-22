# Blazor Hosting models

#### Blazor WebAssembly

This is also called the client-side hosting model and in this model, the application runs directly in the browser on WebAssembly. So, everything the application needs i.e the compiled application code itself, it's dependencies and the .NET runtime are downloaded to the browser. We use the Blazor WebAssembly App template, to create a Blazor application with the client-side hosting model. We will see this in action in our upcoming videos.

#### Blazor server

This is also called the server hosting model and in this model, the application is executed on the server from within an ASP.NET Core application. Between the client and the server, a SignalR connection is established. When an event occurs on the client such as a button click, for example, the information about the event is sent to the server over the SignalR connection. The server handles the event and for the generated HTML a diff \(difference\) is calculated. The entire HTML is not sent back again to the client, it's only the diff that is sent to the client over the established SignalR connection. The browser then updates the UI. Blazor embraces the single page application architecture which rewrites the same page dynamically in response to the user action. Since only the diff is applied to update the UI, the application feels faster and more responsive to the user.

### Blazor Server vs Blazor WebAssembly

The project structure and layout is not that different between the 2 project types.

![blazor server vs blazor webassembly](https://www.pragimtech.com/blog/contribute/article_images/blazor%20server%20vs%20blazor%20webassembly.png)



