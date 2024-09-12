# Debugging External Source Code in Visual Studio: A Guide

Debugging external source code in Visual Studio, such as code from the .NET runtime or NuGet packages, is a powerful feature that allows developers to dive deep into code they didn't write themselves. Chuck Ries, an engineer on the Visual Studio Debugger team, shares some valuable insights into this process and demonstrates how to navigate through external code effectively. This article summarizes key points from his talk.

### Default Debugging Scenario
Visual Studio’s default settings are optimized for debugging code within your own project. By default:
- **Just My Code** is enabled.
- No symbol servers are configured.
- External source code remains hidden in the call stack.

Here’s a common scenario: when a lambda function is passed to a method like `Array.Sort`, the developer can step into the lambda. The call stack will show external code collapsed. For example, the `.NET Sort` method would be part of the external code.

By clicking "Show external code" in the call stack, Visual Studio decompiles the external code. This provides a view into the code that is generated from Intermediate Language (IL) instructions, converting them back into readable C#. This version is functional but may differ in style and structure from the original source code.

### Navigating External Source Code
Developers can explore external source code through:
1. **Decompilation**: Visual Studio can decompile code, showing a human-readable version of the IL instructions running at runtime. However, heavily optimized code, especially by the CLR’s Just-in-Time (JIT) compiler, may result in some local variables being unavailable for inspection.
   
2. **Solution Explorer**: By expanding the "External Sources" node, developers can browse all modules with loaded symbols. This provides an organized view of available namespaces and types, allowing you to sync with the active document and browse through the decompiled external code.

### Improving Debugging with Symbols and Source Link
For more accurate and insightful debugging of external code, developers can tweak some Visual Studio settings:
1. **Disable "Just My Code"**: This allows stepping into external methods like `Array.Sort`.
   
2. **Enable Symbol Servers**: In the Debug options, enabling **Microsoft Symbol Servers** allows Visual Studio to download symbols for the .NET runtime, offering deeper insight into the execution flow.
   
3. **Configure Symbol Loading**: Changing the symbol loading setting to "Load only specified modules" ensures that Visual Studio only downloads symbols when required, improving efficiency.

When stepping into `Array.Sort` with these settings, Visual Studio fetches the source from GitHub, allowing developers to step directly through the external code, with the added benefit of retaining access to local variables since the code is re-jitted for debugging.

### Debugging NuGet Packages
One of the key advantages of Visual Studio's external source debugging is the ability to debug code from external dependencies, such as NuGet packages. To do this:
- Enable **nuget.org Symbol Servers** in the symbol settings.
- Add any custom **Azure DevOps Symbol Servers** to fetch symbols from packages hosted in your organization.

Once configured, Visual Studio can download symbols and source files from NuGet packages, allowing full debugging capabilities even for code that wasn’t built directly in your local environment.

### Source Link: The Key to External Debugging
Source Link provides seamless access to the source code of external dependencies. Visual Studio automatically uses Source Link if it's enabled in the project, downloading the appropriate source files for debugging. As of .NET 8, Source Link is enabled by default in any .NET project. For earlier versions, developers can include the Source Link GitHub package to enable this functionality.

### Building with Source Link
To enable Source Link in your projects:
1. **.NET 8 or Later**: Source Link is built-in, and you don't need additional steps.
2. **Earlier .NET Versions**: Include the GitHub Source Link package to configure Source Link.

Once Source Link is enabled, build pipelines like GitHub Actions or Azure DevOps need to be configured to ensure symbols are published correctly, allowing debugging in downstream projects. This involves adding tasks to the CI pipeline to pack the project with symbols and push them to a symbol server.

### Conclusion
Debugging external source code is a powerful feature in Visual Studio that helps developers understand and troubleshoot code they didn’t write. By decompiling, loading symbols, and using Source Link, developers can gain deep insights into external dependencies, making the debugging process more effective and comprehensive.

These features, especially when used in conjunction with .NET 8 or later, provide a much richer and more efficient debugging experience, ensuring that even optimized code can be inspected and stepped through with ease.


Checkout this [Youtube Video]([(1704) Debugging External Sources with Visual Studio - YouTube](https://www.youtube.com/watch?v=TxIL5JzEblk)).