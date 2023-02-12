# .NET Generic Host

[Referenz](https://docs.microsoft.com/en-us/dotnet/core/extensions/generic-host)

> A _host_ is an object that encapsulates an app's resources, such as:
>-   Dependency injection (DI)
>-   Logging
>-   Configuration
>-   `IHostedService` implementations

Beim Host kann Klassen, die IHostedService implementieren, registrieren. Wenn der host startet wird von jeder dieser Klassen `StartAsync` aufgerufen. Wenn man einen long running hosted Service haben möchte kann man von `BackgroundService` (siehe [link](https://docs.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.backgroundservice?view=dotnet-plat-ext-6.0)) ableiten.

Der Host wird über einen `Builder` konfiguriert und danach via `RunAsync` gestartet:

```CSharp

await Host.CreateDefaultBuilder(args)
    .ConfigureServices(services =>
    {
        services.AddHostedService<SampleHostedService>();
    })
    .Build()
    .RunAsync();
```

Standardmäßig werden vom Framework drei Interfaces im Host-spezifischen DI-Contianer registriert:

-   [IHostApplicationLifetime](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-6.0#ihostapplicationlifetime)
-   [IHostLifetime](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-6.0#ihostlifetime)
-   [IHostEnvironment / IWebHostEnvironment](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-6.0#ihostenvironment)


**IHostApplicationLifetime**: Hier kann man Start- und Stop-Hooks registrieren und während des App-Startups oder -Shutdown eigene Tasks durchzuführen.

**IHostLifetime**: Implementiert wie die App gestartet und gestopt wird. Es gibt z.B. eine `ConsoleLifetime`, bei der durch `Ctrl+C` die App gestopt wird.

**IHostEnvironment**: Darüber kann man sich Infos über den App-Name, den Environment-Name oder den ContentRootPath holen.


Für die Host- und App-Konfiguration sind diese Links interessant: [Host-Config](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-6.0#host-configuration), [App-Config](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-6.0#app-configuration).

#NetCore