
`Deployment` ist eine Resource die mit Kubernetes erzeugt werden kann. 

Ein Deployment kann via 

```
kubectl create depoyment my-apache --image httpd
```

erzeugt werden.

Möchte man sich anzeigen lassen was passiert, kann man 

```
kubectl get all
```

verwenden:
```
controlplane $ kubectl get all
NAME                             READY   STATUS    RESTARTS   AGE
pod/my-apache-5bd7979764-ld8hw   1/1     Running   0          5m2s
pod/my-apache-5bd7979764-nwmql   1/1     Running   0          5m10s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   34d

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/my-apache   2/2     2            2           5m10s

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/my-apache-5bd7979764   2         2         2       5m10s
```


Im Hintergrund erzeugt das `kubectl` command eine YAML-description die man sich mit mit

```
kubectl get deploy/my-apache  -o yaml
```

anzeigen lassen kann.


#### Pods anzeigen lassen

```
controlplane $ kubectl get pods
NAME                         READY   STATUS    RESTARTS   AGE
my-apache-5bd7979764-ld8hw   1/1     Running   0          8m56s
my-apache-5bd7979764-nwmql   1/1     Running   0          9m4s
```

#### Nodes anzeigen lassen

```
controlplane $ kubectl get node 
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   34d   v1.29.0
node01         Ready    <none>          34d   v1.29.0
```


## Resources anzeigen lassen

Mit 

```
kubectl describe deploy my-apache
```

kann man sich Info in human-readable Form anzeigen lassen:


```
NAME                             READY   STATUS    RESTARTS   AGE
pod/my-apache-5bd7979764-ld8hw   1/1     Running   0          5m2s
pod/my-apache-5bd7979764-nwmql   1/1     Running   0          5m10s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   34d

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/my-apache   2/2     2            2           5m10s

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/my-apache-5bd7979764   2         2         2       5m10s
controlplane $ kubectl describe deploy my-apache    
Name:                   my-apache
Namespace:              default
CreationTimestamp:      Sat, 06 Apr 2024 20:31:23 +0000
Labels:                 app=my-apache
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=my-apache
Replicas:               2 desired | 2 updated | 2 total | 2 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=my-apache
  Containers:
   httpd:
    Image:        httpd
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Progressing    True    NewReplicaSetAvailable
  Available      True    MinimumReplicasAvailable
OldReplicaSets:  <none>
NewReplicaSet:   my-apache-5bd7979764 (2/2 replicas created)
Events:
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  6m49s  deployment-controller  Scaled up replica set my-apache-5bd7979764 to 1
  Normal  ScalingReplicaSet  6m41s  deployment-controller  Scaled up replica set my-apache-5bd7979764 to 2 from 1
```

>[!note]
>`describe` zeigt uns auch eine Eventliste der jeweiligen Resource an

### PODs

```
controlplane $ kubectl describe pod/my-apache-5bd7979764-ld8hw
Name:             my-apache-5bd7979764-ld8hw
Namespace:        default
Priority:         0
Service Account:  default
Node:             controlplane/172.30.1.2
Start Time:       Sat, 06 Apr 2024 20:31:31 +0000
Labels:           app=my-apache
                  pod-template-hash=5bd7979764
Annotations:      cni.projectcalico.org/containerID: 2a63822bacc70c07f2e23f54b8d42ea4ebda04da4b512d98b0f6474fb860618f
                  cni.projectcalico.org/podIP: 192.168.0.5/32
                  cni.projectcalico.org/podIPs: 192.168.0.5/32
Status:           Running
IP:               192.168.0.5
IPs:
  IP:           192.168.0.5
Controlled By:  ReplicaSet/my-apache-5bd7979764
Containers:
  httpd:
    Container ID:   containerd://49eb869928f5d62bd9103917dbb9d7220a3125df7354df2f8a08baed80114f49
    Image:          httpd
    Image ID:       docker.io/library/httpd@sha256:8a1bbe23f2733589625dedde0fb9687419d02cf2ec542c5bd411798b4b47ada3
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Sat, 06 Apr 2024 20:31:38 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-2lggl (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       True 
  ContainersReady             True 
  PodScheduled                True 
Volumes:
  kube-api-access-2lggl:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  9m49s  default-scheduler  Successfully assigned default/my-apache-5bd7979764-ld8hw to controlplane
  Normal  Pulling    9m49s  kubelet            Pulling image "httpd"
  Normal  Pulled     9m43s  kubelet            Successfully pulled image "httpd" in 5.991s (5.991s including waiting)
  Normal  Created    9m43s  kubelet            Created container httpd
  Normal  Started    9m43s  kubelet            Started container httpd
```


## Watch

Mithilfe des `-w` Parameters kann man sich "live" Changes von Resource anzeigen lassen. Beispiel:

```
controlplane $ kubectl get pods -w
NAME                         READY   STATUS    RESTARTS   AGE
my-apache-5bd7979764-l9bdn   1/1     Running   0          3s
my-apache-5bd7979764-nwmql   1/1     Running   0          17m
my-apache-5bd7979764-nwmql   1/1     Terminating   0          18m
my-apache-5bd7979764-n7hmx   0/1     Pending       0          0s
my-apache-5bd7979764-n7hmx   0/1     Pending       0          0s
my-apache-5bd7979764-n7hmx   0/1     ContainerCreating   0          0s
my-apache-5bd7979764-n7hmx   0/1     ContainerCreating   0          0s
my-apache-5bd7979764-nwmql   1/1     Terminating         0          18m
my-apache-5bd7979764-nwmql   0/1     Terminating         0          18m
my-apache-5bd7979764-nwmql   0/1     Terminating         0          18m
my-apache-5bd7979764-nwmql   0/1     Terminating         0          18m
my-apache-5bd7979764-nwmql   0/1     Terminating         0          18m
my-apache-5bd7979764-n7hmx   1/1     Running             0          1s
```

Parallel wurden Pods mit Hilfe von `kubectl delete pods alksjflk` geölscht. Man sieht, dass ein neuer Pod gestartet wurde -> **Grund**: Das Deployment definiert zwei Replicas.

## Events

Events zeigt alle Events auf dem Cluster an. Man kann sich via `-watch-only` die aktuellen Changes anzeigen lassen:

```
controlplane $ kubectl get events --watch-only
LAST SEEN   TYPE     REASON    OBJECT                           MESSAGE
0s          Normal   Killing   pod/my-apache-5bd7979764-w9fwg   Stopping container httpd
0s          Normal   SuccessfulCreate   replicaset/my-apache-5bd7979764   Created pod: my-apache-5bd7979764-c2g9l
0s          Normal   Scheduled          pod/my-apache-5bd7979764-c2g9l    Successfully assigned default/my-apache-5bd7979764-c2g9l to controlplane
0s          Normal   Pulling            pod/my-apache-5bd7979764-c2g9l    Pulling image "httpd"
0s          Normal   Pulled             pod/my-apache-5bd7979764-c2g9l    Successfully pulled image "httpd" in 244ms (244ms including waiting)
0s          Normal   Created            pod/my-apache-5bd7979764-c2g9l    Created container httpd
0s          Normal   Started            pod/my-apache-5bd7979764-c2g9l    Started container httpd
```


#Kubernetes