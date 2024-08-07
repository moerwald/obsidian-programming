

Use namespaces to seperate PODS. You can define quotas on a namespace:

```yaml

apiVersion: v1
kind: ResourceQuota
metadata:
	name: compute-quota
	namespace: dev
spec:
	hard:
		pods: "10"
		requests.cpu: "4"
		requests.memory: 5Gi
		limits.cpu: "10"
		limits.memory: 10Gi
```

PODs inside the same namespace can address each other via a simple name, e.g. `database`. If you want to address a POD in a other namespace you' ve to use the FQDN, e.g. webapp.app.scv.cluster.local.

## Tell kubectl to use another namespace


With this command:

```bash
kubectl config set-context $(kubectl config current-context) --namespace=dev
```


all upfollowing kubectl commands will query the `dev` namespace.


#Kubernetes