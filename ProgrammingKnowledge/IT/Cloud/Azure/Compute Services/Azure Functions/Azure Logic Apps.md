# Azure Logic Apps

[Referenz](https://docs.microsoft.com/en-us/learn/modules/azure-compute-fundamentals/azure-functions)

Im Grunde das Gleiche wie  [[Azure Functions]]. Allerdings kann ich damit Business Scenarios implementieren. Hier wird **kein Code** sondern vorgefertigte **Logikblöcke** verwendet. Die Logikblöcke werden in einem **Workflow** zusammengefasst. Ein Logikblock hängt an einem **Trigger** . Der Trigger kann eine externen Quelle oder ein Timer sein.

Wenn der Trigger feuert erzeugt die `Logic Apps` -Engine eine App-Instanz, die den Workflow abarbeitet. Der Workflow besteht aus `Actions`, die wiederum Loop und Conditions beinhalten können.

---
**Beispiel**

Du hast ein Azure Fileshare. Jedes wenn ein neues File hochgeladen wird möchtest du einen E-Mail mit dem Filenamen erhalten

---




#AzureComputeServices