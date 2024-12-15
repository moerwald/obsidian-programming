
Hier ist die überarbeitete Version deines Textes:

---

Die Einrichtung von MetalLB ist relativ unkompliziert. Zunächst wird das Manifest gemäß der [offiziellen Anleitung](https://metallb.universe.tf/installation/) installiert:

```bash
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.14.8/config/manifests/metallb-native.yaml
```

Wenn Virtual IPs auf Layer-2-Ebene benötigt werden, kann folgendes Manifest angewendet werden:

```yaml
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: first-pool
  namespace: metallb-system
spec:
  addresses:
  - 192.168.0.40-192.168.0.41

---

apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: metallb-l2-advertisement
  namespace: metallb-system
spec:
  ipAddressPools:
    - first-pool
```

Nach der Installation laufen der MetalLB Controller-Pod sowie mehrere Speaker-Pods. Dabei wird auf jedem Host ein Speaker-Pod ausgeführt. Um die Speaker-Pods nur auf den Worker-Nodes zu betreiben, kann ein `NodeSelector` verwendet werden. Zuerst müssen die Worker-Nodes entsprechend gelabelt werden:

```bash
kubectl label node wn1 node-role.kubernetes.io/worker=true
kubectl label node wn2 node-role.kubernetes.io/worker=true
kubectl label node wn3 node-role.kubernetes.io/worker=true
```

Anschließend wird ein `NodeSelector` definiert und per Patch angewendet:

```yaml
spec:
  template:
    spec:
      nodeSelector:
        node-role.kubernetes.io/worker: "true"
```

Der Patch wird dann wie folgt auf das DaemonSet angewendet:

```bash
kubectl patch daemonset speaker -n metallb-system --patch "$(cat patch-speaker-daemonset.yaml)"
```

#Kubernetes
