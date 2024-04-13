
Wir verwenden HTTPENV, ein Webserver der sein lokales Environment zurück gibt. 


```
 kubectl create deployment httpenv --image=bretfisher/httpenv
 kubectl scale deploy/httpenv --replicas=10
 kubectl expose deployment httpenv --port 8888
```

Check service:

```
$ kubectl get service
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
httpenv      ClusterIP   10.152.183.128   <none>        8888/TCP   42s
kubernetes   ClusterIP   10.152.183.1     <none>        443/TCP    3d
```



#Kubernetes 