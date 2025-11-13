

Hier die Befehle und das PS-REmoting zu aktivieren:

```powershell
Set-NetConnectionProfile -NetworkCategory Private
Enable-PSRemoting -Force 
```

Auf demselben Rechner kann man das wie folgt prüfen:

```powershell
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "10.0.0.222"
Enter-PSSession -ComputerName 10.0.0.222 -Credential (Get-Credential)
```

Dann sieht man 

```powershell
[10.0.0.222]: PS C:\Users\Administrator\Documents> exit
```


#PsRemoting