

Before installing istio the namespace has to be set to privileged!!

```
kubectl create namespace istio-system;kubectl label namespace istio-system pod-security.kubernetes.io/enforce=privileged --overwrite
```

The followe the instructions under: [Istio / Getting Started](https://istio.io/latest/docs/setup/getting-started/)


For the test application create a namespace and activate istio sidecar-proxy-injection:

```
kubectl create ns test-app
kubectl label namespace test-app istio-injection=enabled
```

On default Talos installation Pods won't be created due following error:

```
15s (x4 over 33s)       Warning   FailedCreate        ReplicaSet/reviews-v1-598b896c9d       (combined from similar events): Error creating: pods "reviews-v1-598b896c9d-8mhlj" is forbidden: violates PodSecurity "baseline:latest": non-default capabilities (container "istio-init" must not include "NET_ADMIN", "NET_RAW" in securityContext.capabilities.add)
```

Adapt the namespace

```
kubectl label namespace test-app pod-security.kubernetes.io/enforce=privileged --overwrite
```

#istio 
#Talos 