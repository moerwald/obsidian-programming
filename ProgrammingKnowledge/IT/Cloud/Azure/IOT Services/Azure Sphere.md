Azure Sphere ist ein Plattform die End-To-End Security zwischen Azure und IOT Devices bietet. Hierfür werden spezielle Azure Micro-Controller-Units verwendet auf denen ein Custom Microsoft Linux läuft. 

Azure Sphere besteht aus drei Teilen:

1. Die MCU, die das custom Linux hostet. ![Screenshot of an Azure Sphere development kit micro-controller unit.](https://docs.microsoft.com/en-us/learn/azure-fundamentals/iot-fundamentals/media/2-identify-product-options-02-d830e12a.png) 
2. Das custom Linux, auf dem später die Kunde-App läuft.
3. Azure Sphere Security Service (AS3). AS3 authetifiziert das MCU wenn es sich auf Azure verbindet. Die Authentifizierung erfolgt über Zertifikate. Steht die m**verschlüsselte** Verbindung, erfolgt ein Check ob das OS komprimietiert ist oder nicht. Falls nein, wird die zuvor hochgeladene APP auf das MCU kopiert und das Device geht online.

#Azure
#AzureIotServices