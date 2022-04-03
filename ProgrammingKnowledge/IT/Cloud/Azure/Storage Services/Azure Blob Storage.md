# Azure Blob Storage

[Referenz](https://docs.microsoft.com/en-us/learn/modules/azure-storage-fundamentals/azure-blob-container-storage)

## Allgemein 

Ermöglicht das Speichern von `Blob`s (=*Binary Large Object*). Blobs werden in `Containern` organisiert. Ein Container kann mehrere Blobs enthalten. Blobs sind **geo redundant**. 

Daten die in Blobs gespeichert werden können:

- Audio/Video
- Elends lange Logfiles
- Bilder
- Verschlüsselte Daten
- Backups
- ...

Ein Vorteil von Blobs: Man muss sich nicht um Disks kümmern. Azure übernimmt die Allokierung von Disks wenn der Blob größer wird (= IAAS).

Blobs können die verschiedenen Access Tiers, wie in [[Azure Storage Account]] beschrieben, haben.

## Azure Blob Accees Tiers (=Ebenen)

Um verschiedene Verrechnungsebenen zu realsieren bietet Blob Storage verschiedene Access Tiers:

- **Hot**: Daten die oft verwendet werden. Höchstes SLA. Kosten sind hier am höchsten.
- **Cool**: Daten die seltener verwendet werden und zumindest 30 Tage gespeichert werden (z.B. Rechnungen). Hier ist die Availability geringer, die Integrietät ist aber weiterhin gewährleistet. Die Speicherung der Daten ist günstiger als im Hot Tier, allerdings kann ein Zugriff teurer werden. Die Zugriffszeiten sind ähnlich zum Hot Tier.
- **Archive**: Für Daten die eher nie verwendet werden. Speicherkosten sehr gering. Allerdings sind die Zugriffskosten am höchsten, da die Archive **extra** für den Zugriff vorbereitet werden müssen. 

*Hot*- und *Cool*-Tier können auf **Storage Account** Ebene eingestellt werden. *Hot*-*Cool*- und *Archive*-Tier können auf **Blob**-Ebene während oder nach dem Upload eingestellt werden.

#Azure
#AzureStorageAccount 
#AzureStorageServices 
#IAAS
