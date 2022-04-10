# Invoke Powershell from CSharp

[Referenz](https://docs.microsoft.com/en-us/powershell/scripting/developer/hosting/windows-powershell-host-quickstart?view=powershell-7.2)


Um Powershell aus C# heraus zu nutzen braucht man das [Microsoft.PowerShell.SDK](https://www.nuget.org/packages/Microsoft.PowerShell.SDK/)-Nuget-Paket. 

Die Powershell Instanz selber wird über die [System.Management.Automation.PowerShell](https://docs.microsoft.com/en-us/dotnet/api/System.Management.Automation.PowerShell?view=powershellsdk-7.0.0)-Klasse erzeugt. Die PowerShell-Instanz muss in einem **Runspace** laufen. Der Runspace enthält Referenzen auf CmdLets und Variablen damit die PowerShell Instanz funktioniert. Es gibt einen Default-Runspace, der so ziemlich alles enthält. Das Laden des Runspace kann Performance kosten, deswegen kann man Runspaces beschneiden, damit nur das Geladen wird was man braucht. Hierfür wird der **InitialSessionState** benötigt, in dem man definiert welche Cmdlets und Variablen zur Verfügung stehen.

Die einfachste Möglichkeit eine PowerShell zu erzeugen:

```
PowerShell ps = PowerShell.Create();
```

Man kann dann mit `AddCommand` eine Pipeline bauen:

```

```
