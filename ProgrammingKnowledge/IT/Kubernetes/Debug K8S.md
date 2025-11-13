


### Use Curl pod

```
kubectl run curlpod --rm -it --image=curlimages/curl --restart=Never -- curl -v http://istio-ingressgateway.istio-system.svc.cluster.local/productpage
```


#Kubernetes 
#Debug
#Curl