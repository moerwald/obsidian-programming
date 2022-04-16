# Wie findet man raus ob Windows auf VM läuft oder nicht


```Powershell
get-wmiobject win32_computersystem | fl model
```


#PowerShellSnippet
