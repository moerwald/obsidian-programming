# Azure File Storage
[Referenz](https://docs.microsoft.com/en-us/learn/modules/azure-storage-fundamentals/azure-file-storage) 

## Allgemein

Ermöglicht einen FileShare in der Cloud. Der Zugriff kann über SMB (= [Server Message Block](https://en.wikipedia.org/wiki/Server_Message_Block)) oder NFS (Network File System) erfolgen. Die Shares können über jedes Betriebssystem gemounted werden.

### Vorteil 
OnPrem FileShares können leicht in die Cloud gemovt werden, sofern aus App-Sicht der Name des Netzlaufwerks gleich bleibt. Generell kann es als Dropbox Ersatz genutzt werden.

FileShares können geo-redundant verwendet werden. Azure FileShare verschlüsselt die Daten im DataCenter, SMB kümmert sich um die Verschlüsselung beim Transport.

![Diagram that shows the file sharing capabilities of Azure Files between a Western US Azure file share and a European Azure file share, each with their own SMB users.](https://docs.microsoft.com/en-us/learn/azure-fundamentals/azure-storage-fundamentals/media/azure-files-5f942c3e.png) 



#Azure
#AzureStorageAccount 
#AzureStorageServices 