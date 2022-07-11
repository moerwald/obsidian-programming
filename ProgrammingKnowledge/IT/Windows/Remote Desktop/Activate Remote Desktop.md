# Activate via PSEXEC

RDP kann über PSExec remote aktiviert werden. PSExec legt dann einen enstprechenden Registry Eintrag an:

```
psexec \\10.144.41.224 reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
```

Kann unter diesem [Link](https://davidvielmetter.com/tricks/four-ways-to-remotely-reboot-a-windows-machine/) nachgelesen werden.



#RDP
#RemoteDesktop
