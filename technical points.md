## Respawn

[Link](https://github.com/jbogard/Respawn)

Small utility to reset test databases to clean state. C# based and mainly focus on SQL database.


## MediatR

## AutoMapper

## FluentValidation

## FluentAssertions

## gRPC
[Course](https://app.pluralsight.com/library/courses/aspdotnet-core-6-using-grpc/table-of-contents) bookmark: Protocol Buffers
    - REST api : CRUD and purely web apps
    - SOAP
    - GraphQL : Open querying of large datasets
    - gRPC : streaming, low resource clients and inter-data center
    - SignalR: Multi-casting and web messaging


## React V.18
[What's New](https://blog.appsignal.com/2022/04/13/whats-new-in-react-18.html)

## Webpack vs Vite

## react-app-rewired

## ngrok (ngrok is a free service that helps you share a site or server running on your local machine.)

## controller-based APIs VS minimal APIs
### controller-based 
Structure and Organization: Controllers offer a clear structure, separating concerns and enhancing maintainability.
Flexibility: They enable custom routes, complex request handling, and support various HTTP verbs.
Testing: Controllers facilitate unit testing of individual actions, promoting a test-driven approach.

### minimal (Concise and Swift)
Simplicity: Minimal APIs drastically reduce code complexity, ideal for smaller projects or rapid prototyping.
Ease of Use: They enable quick API creation with fewer dependencies, accelerating development cycles.
Potential Performance Boost: The reduced overhead might lead to improved performance, especially in smaller applications.

[Microsoft Docs](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/apis?view=aspnetcore-9.0) : 

> Minimal APIs have many of the same capabilities as controller-based APIs. They support the configuration and customization needed to scale to multiple APIs, handle complex routes, apply authorization rules, and control the content of API responses. There are a few capabilities available with controller-based APIs that are not yet supported or implemented by minimal APIs. These include:

- No built-in support for model binding (IModelBinderProvider, IModelBinder). 
- Support can be added with a custom binding shim.
- No built-in support for validation (IModelValidator).
- No support for application parts or the application model. There's no way to apply or build your own conventions.
- No built-in view rendering support. We recommend using Razor Pages for rendering views.
- No support for JsonPatch
- No support for OData

## EF Conventions VS Data Annotations VS Fluent API in OnModelCreating

> You can also apply certain attributes (known as Data Annotations) to your classes and properties. Data annotations will override conventions, but will be overridden by Fluent API configuration.

- Grouping configuration
- Applying all configurations in an assembly
- Using EntityTypeConfigurationAttribute on entity types

[More Details](https://learn.microsoft.com/en-us/ef/core/modeling/)