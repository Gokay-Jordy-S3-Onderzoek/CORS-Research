# CORS-Research

## How to enable CORS in your Api?
Enabling CORS in you Api greatly depends on what framework you are using. In some frameworks enabling and seting up CORS is very easy, in others it is a bit more complicated. In this document I will show you how to enable CORS in the following frameworks:
 - [ASP.NET Core](#aspnet-core)
 - [Spring Boot](#spring-boot)
 - [Node.js](#nodejs)
 - [Laravel](#laravel)

### ASP.NET Core
In ASP.NET Core API enabling CORS is pretty straight forward. First you need to add CORS to the builder.Services in the Program.cs file. You do this by adding the following lines before the builder.Build() line:
```csharp
builder.services.AddCors();
```
After this we need to tell the app to use CORS. This is done by adding the following lines after the builder.Build() line:
```csharp
app.UseCors(x => x
                .WithOrigins("http://localhost:3000")
                .AllowAnyMethod()
                .AllowAnyHeader()
                .AllowCredentials());
```

http://localhost:3000 is in this case the Origin we allow to make requests to this API.

### Spring Boot

Springboot might've one of the easiest ways to enable CORS. All you need to do is add the following annotation to your controller:
```java
@CrossOrigin(origins = "http://localhost:3000")
```

You add this annotation to the controller that contains the methods that you want to allow CORS for. Or you can even add it before the method itself. In this case the Origin we allow to make requests to this API is http://localhost:3000.


