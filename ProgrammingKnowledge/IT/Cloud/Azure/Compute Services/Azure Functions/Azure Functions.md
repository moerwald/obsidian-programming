# Azure Functions

[Referenz](https://docs.microsoft.com/en-us/learn/modules/azure-compute-fundamentals/azure-functions)


Macht Sinn wenn ich mich um Infrastruktur und Plattform **nicht** kümmern möchte. Functions laufen immer als Antwort eines Events, spricht Event-getriggert. Functions eignen sich am Besten wenn die Abarbeitung des Events im Sekunden Bereich liegt. Dinge wie Autosklaierung, Starte, Restarten der App übernimmt die Plattform. Verrechnet wird nur die **reine CPU**-Zeit die mein App-Code benötigt. 

Es gibt *Stateless* und *Statefull* Functions (=`Durable Functions`). Im zweiten Fall erhält der Code einen Kontext der den aktuellen State inkludiert.

Bei [[Virtual Machines]] würde ich Geld verbrennen, da ich hier auch die *Idle*-Time der VM zahlen muss.

#AzureFunctions
#AzureComputeServices

