

Link: [Scrutor](https://github.com/khellang/Scrutor)


From ChatGPT:

> Scrutor is a .NET library that provides a simple and fluent API for scanning assemblies and registering types in the .NET Core dependency injection container. It allows you to use attributes or conventions to automatically register your types, which can save you a lot of time and reduce the amount of code you need to write.

>With Scrutor, you can quickly and easily register all types that implement a specific interface or derive from a specific base class, as well as apply custom filters to fine-tune which types get registered.

>Overall, Scrutor makes it easier to manage and organize your dependency injection container registrations, while also providing more flexibility and control over the registration process.

Mithilfe von Scrutor kann man Service basierend auf einem Attribute als `Transien`, `Singleton` oder `Scoped` in der [[ServiceCollection]] registrieren:


```CSharp

services.Scan(scan => scan
    .FromAssemblyOf<MyService>()
    .AddClasses(classes => classes.WithAttribute<ServiceLifetimeAttribute>())
    .UsingAttributes()
    .AsImplementedInterfaces()
    .Configure(registration =>
        registration.Lifetime = (registration.Type.GetCustomAttribute<ServiceLifetimeAttribute>()?.Lifetime) switch
        {
            ServiceLifetime.Singleton => ServiceLifetime.Singleton,
            ServiceLifetime.Scoped => ServiceLifetime.Scoped,
            _ => ServiceLifetime.Transient
        }));

services.AddHostedService<MyHostedService>();
services.Scan(scan => scan
    .FromAssemblyOf<MyOtherHostedService>()
    .AddClasses(classes => classes.AssignableTo<IHostedService>())
    .AsImplementedInterfaces()
    .WithSingletonLifetime());


[AttributeUsage(AttributeTargets.Class, AllowMultiple = false)]
public class ServiceLifetimeAttribute : Attribute
{
    public ServiceLifetime Lifetime { get; }

    public ServiceLifetimeAttribute(ServiceLifetime lifetime)
    {
        Lifetime = lifetime;
    }
}

```


#CSharp 
#DotNet 
#DependencyInjection
