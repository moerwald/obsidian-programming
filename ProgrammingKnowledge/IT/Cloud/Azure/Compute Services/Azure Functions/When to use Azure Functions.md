#  When to use Azure Functions

[Referenz](https://docs.microsoft.com/en-us/learn/modules/azure-compute-fundamentals/azure-functions)

---
**Serverless**: 

> _Serverless_ computing is the abstraction of servers, infrastructure, and operating systems. With serverless computing, Azure takes care of managing the server infrastructure and the allocation and deallocation of resources based on demand. Infrastructure **isn't your responsibility**. **Scaling and performance are handled automatically.** You're billed only for the exact resources you use. There's **no need to even reserve capacity**.

---

Azure Functions machen Sinn wenn man auf **Events** wartet, sprich Event-getriggert arbeitet. Die Wartezeit bis das Event kommt wird **nicht** verrechnet.

Sererless Computing hat drei Eigenschaften:

1. Die Infrastruktur, der Server und das OS werden **abstrahiert**. Der Code der Ausgeführt werden soll definiert ein Behaviour und ein Binding (wie soll die Verbindung auf ein ext. Service (Twitter, Facebook)) erfolgen. Dies geht soweit, dass der Code eventuell immer auf anderen Servern ausgeführt wird.
2. **Skalierung** in Abhängigkeit der Event-Rate. Azure Funktions kann basierend auf den angegebenen Function Metadaten entscheiden die Function mehrfach laufen zu lassen, z.B. in Abhängigkeit der Event-Rate/Sekunde.
3. **Mikroverrechnung**: Es wird nur die Zeit abgerechnet in der die Funktion läuft. Altes Modell: Webserver läuft ein ganzes Monat. Obwohl die Website nur einmal besucht wurde, wird das ganze Monat verrechent. Bei **Functions NICHT**.

Es gibt zwei Implementierungen von Azure Functions:

- [[Azure Functions]]
- [[Azure Logic Apps]] 


## Functions vs. Logic Apps
Mit beiden Varianten können komplexe Szenarien gebaut werden. Wobei bei Functions jeder Step gecoded wird. In diesen Szenarien kann ich `Functions` mit `Logic Apps` mischen! Ich kann aus einer `Function` eine `Logic App` aufrufen und umgekehrt.

|-- | **Functions** |**Logic Apps** |
|-------------------|---------------------------------|---------------------------------------|
|State|Normally stateless, but Durable Functions provide state. |Stateful.|
|Development|Code-first (imperative).|Designer-first (declarative).|
|Connectivity|About a dozen built-in binding types. Write code for custom bindings.|Large collection of connectors. Enterprise Integration Pack for B2B scenarios. Build custom connectors.  |
|Actions|Each activity is an Azure function. Write code for activity functions.|Large collection of ready-made actions.|
|Monitoring|Azure Application Insights.|Azure portal, Log Analytics.|
|Management|REST API, Visual Studio.|Azure portal, REST API, PowerShell, Visual Studio.|
|Execution context|Can run locally or in the cloud.|Runs only in the cloud.|


#AzureComputeServices