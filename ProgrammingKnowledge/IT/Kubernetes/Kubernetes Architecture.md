
## Aus was besteht K8s?

![[components-of-kubernetes.svg]]
![[Pasted image 20240410215222.png]]

`kube-proxy` kümert sich ums Networking auf dem Node.
`kubelet` redet mit der Container Runtime.

## Control Plane

Control Plane kann über mehrere Server verteilt sein.

- API Server
- etcd
- Scheduler
- Controller Manager

## Der Node

Auf jedem Node befinden sich:

- Kube-Proxy
- Kubelet
- Container Engine (normalerweise Docker)

## Container Runtimes

K8s braucht ein Container Runtime, default ist Docker. Aber es gibt auch andere:
- ContainerD: Docker -> only the runtime
- CRI-O: Maintained by RedHat

K8s verwendet das [`Container Runtime Interface`](https://kubernetes.io/docs/concepts/architecture/cri/) um zwischen versch. Runtimes zu switchen.

## Interacting with K8s

Die Interaktion erfolgt über das API-Service (in der Control Plane). Das API-Service erlaubt uns CRUD auf Resourcen.
Resourcen können sein:
- Node: Physische oder virtuelle Maschine in einem Cluster
- POD: Ein Gruppe von Container, welche auf einem Node laufen (= lowest deployeable Unit)
- Service: Network Endpoint, über den Container ansprechbar gemacht werden


### PODS

PODs sind die kleinste deployable Einheit in K8s. Ein POD kann mehrere Container beinhalten. IP-Adressen werden mit PODs assoziiert. Container innerhalb eines PODs sharen `localhost` und können darüber kommunizieren.

>[!note]
>K8s kann nur PODs verwalten. KEINE Container.



![[Pasted image 20240410221036.png]]


## Services

>[!note]
>a service is a STABLE address for a pod (or a bunch of pods)

Wenn wir uns auf PODs verbinden wollen, brauchen wir Services. Da Services Adressen darstellen müssen diese aufgelöst werden können, hier hilft uns CoreDNS.

Arten von Services:
- ClusterIP
- NodePort
- LoadBalancer
- ExternalName

`kube-proxy` verwaltet Services, via `iptables`.

### ClusterIPs

ClusterIPs sind nur im Cluster verfügbar. Möchte man von außen zugreifen braucht man einen NodePort

### NodePort

ermöglicht den Zugriff von außerhalb des Clusters auf einen Pod. Ports eine Pods werden nach außen auf die PortRange 30.000 - 32.768 gemappt. Der NodePort ist auf **ALLEN** Nodes innerhalb eines Clusters verfügbar.

### LoadBalancer

Ist normalerweise der Weg um auf Pods von außen zuzugreifen. LoadBalancer werden zB vom Cloudprovider zu Verfügung gestellt, und mit einem oder mehrern NodePorts verbunden.

### ExternalName

Ermöglicht es einen externen DNS Name für den Cluster zu setzen.

#Kubernetes 