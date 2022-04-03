# When to use containers/kubernetes services instead of VMs

 [Reference](https://docs.microsoft.com/en-us/learn/modules/azure-compute-fundamentals/azure-container-services)

**Problem:** VMs helfen Hardware einzusparen. Allerdings ist der Aufwand ein App in mehreren VMs laufen zu lassen zu hoch. Eine "leichtere" Variante stellen hier Container dar. Container lassen sich *schnell* starten. Deswegen ist ein Restart eines Containers (bzw. der App) darin relativ schnell erldeigt. 

---

**Wichtig**: Vms emulieren Hardware, Container emulieren Operation System.

---

## Was sind Container

Wie schon gesagt emulieren Container Betriebssysteme. Container sind designt um:

- parallele Ausführung ("hochskalieren")
- schnelles starten
- scnelles stoppen

zu ermöglichen.

Es ist möglich mehrere Container in einem OS-Host laufen zu lassen. Würde man selbiges mit VMs versuchen, steigt der Aufwand. Jede VM braucht "viel" Resourcen und benötigt mehr Konfiguration als ein Container


[VMs vs Containers](https://www.microsoft.com/en-us/videoplayer/embed/RE2yuaq?postJsllMsg=true)

## Containers in Azure

Es gibt zwei Arten Container zu verwalten:

- Azure Container Instances
- Azure Kubernetes Service

Azure Kubernetes Service hilft bei der Verwaltung mehrerer Container (=`Orchestration`). Hier kann man definieren, wieviele Instanzen eines Containers laufen sollen, was passiert wenn eine APP im Container crasht ,.... 
Eine Containers Instanz in Kubernets ist ein `Pod`. Kubernets hilft auch bei der Verwaltung von Storage, Netzwerk, Load Balancing.

---
Mithilfe von Container können Microservices gebaut werden:

>For example, you might split a website into a container hosting your front end, another hosting your back end, and a third for storage.

Jeder Container erfühlt eine Aufgabe = Micro Service.

---


## Fazit

Container werden dann verwendet wenn man eine APP schön skalieren möchte und **wenig** Kontrolle (im OS ) benötigt. Wenn man **mehr** Kontrolle im OS-Level benötigt machen VMs mehr Sinn!


#AzureComputeServices