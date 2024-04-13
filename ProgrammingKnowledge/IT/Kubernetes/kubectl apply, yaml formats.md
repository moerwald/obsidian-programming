

## Kubernetes Configuration YAML

- Jedes File enthält ein oder mehrere Manifests
- Jedes Manifest beschreibt ein API-Objekt (deployment, job, secret)
- Jedes Manifest besteht aus vier Teilen:
	- `apiVersion:`
	- `kind:`
	- `metadata:`
	- `spec:`
	  
	  
	![[Pasted image 20240408222909.png]]


## Welche `kinds` und `API versions` gibt es?

Möchte man ein YAML erstellen, weiß man Anfangs nicht, welche API-Objekte es gibt. Diese Objekte lassen sich über folgendes Command (auf einem aktiven Cluster) anzeigen:

```
kubectl api-resources
```

```
controlplane $ kubectl api-resources
NAME                              SHORTNAMES   APIVERSION                        NAMESPACED   KIND
bindings                                       v1                                true         Binding
componentstatuses                 cs           v1                                false        ComponentStatus
configmaps                        cm           v1                                true         ConfigMap
endpoints                         ep           v1                                true         Endpoints
events                            ev           v1                                true         Event
limitranges                       limits       v1                                true         LimitRange
namespaces                        ns           v1                                false        Namespace
nodes                             no           v1                                false        Node
persistentvolumeclaims            pvc          v1                                true         PersistentVolumeClaim
persistentvolumes                 pv           v1                                false        PersistentVolume
pods                              po           v1                                true         Pod
podtemplates                                   v1                                true         PodTemplate
replicationcontrollers            rc           v1                                true         ReplicationController
resourcequotas                    quota        v1                                true         ResourceQuota
secrets                                        v1                                true         Secret
serviceaccounts                   sa           v1                                true         ServiceAccount
services                          svc          v1                                true         Service
mutatingwebhookconfigurations                  admissionregistration.k8s.io/v1   false        MutatingWebhookConfiguration
validatingwebhookconfigurations                admissionregistration.k8s.io/v1   false        ValidatingWebhookConfiguration
customresourcedefinitions         crd,crds     apiextensions.k8s.io/v1           false        CustomResourceDefinition
apiservices                                    apiregistration.k8s.io/v1         false        APIService
controllerrevisions                            apps/v1                           true         ControllerRevision
daemonsets                        ds           apps/v1                           true         DaemonSet
```


`kubectl api-versions` gibt alle API Versions aus.

`kind:` + `apiVersion:` ergibt die Resource die man anlegen möchte.

>[!note]
>bei `metadata:` braucht man "nur" die `name:` Property definieren


## `spec:`


` kubectl explain services --recursive` liefert alle Keys die eine `kind` supported. Allerdings gibt es hier keine Beschreibung. Mit `kubectl services.spec` erhält man die Spezifikation inkl. Beschreibung. Via `kubectl explain services.spec.selector` kann man sich die einzelne Spec ausgeben lassen.


#Kubernetes