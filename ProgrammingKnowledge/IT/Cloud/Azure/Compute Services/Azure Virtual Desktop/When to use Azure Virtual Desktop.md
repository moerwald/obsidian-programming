# When to use Azure Virtual Desktop

Kann man einsetzen wenn man sich folgendes sparen möchte:

- Hardware
- Versand
- Verwaltung der Systeme (Security Patches, etc.)

[[Azure Virtual Desktop]] im Detail.


## Warum sollte man Virtual Desktop verwenden?

### Bessere User Experience

Der Benutzer kann sich über jedes Device auf den Desktop verbinden. Der Virtual Desktop wird in einem Datacenter gehostet, dass nahe an dem liegt, wo andere Services (des Kunden) laufen. 

User Profile liegen in einem Container. Wenn sich ein User verbindet wird der Container an die Virtual Desktop VM angeflanscht. Somit hat jeder User seinen eigenen individuellen Desktop.

### Bessere Security

Virtual Desktops können über [[Azure Active Directory]] verwaltet werden. Somit sind Dinge wie Multi-Factor-Authentication kein Problem. Weiters läuft jede User-Session isoliert von anderen. Zusätzlich können Rollen-basierte-Zugriffe gewährt werden.

Die Verbindung auf den Desktop erfolgt via `reverse connect` -> es  müssen in der Firewall nicht User-spezifische Inbound Rules definiert werden. 

## Key Features

### Einfacheres Management

Da es auch nur ein Azure Service ist kann man es mit Azure-AD und RBAC ([Role based access controls]) administrieren. Zusätzlich hat man eine hohe Verfügbarkeit (Stichwort: Disaster Recovery). Azure Virtual Desktop ist eine VM, somit greifen die Azure Optionen VMs zu patchen bzw. zu deployen.

### Perfomance Management

Die VMs für den Desktop liegen in `host pools` die Load Balanced werden. Mithilfe der Host-Pools können die User auf mehrere VMs (im Pool) verteilt werden. Somit bleibt die User Experience ok. 

### Multi-session Windows 10 deployment

Mehrere User können parallel auf einer VM arbeiten, ohne sich gegenseitig zu stören.




#AzureComputeServices