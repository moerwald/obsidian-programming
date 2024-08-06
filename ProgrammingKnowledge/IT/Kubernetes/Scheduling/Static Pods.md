

---
tags:
- Kubernetes
- DevOps
- Static Pods
- Kubelet
---

# Static Pods in Kubernetes

In this article, we take a detailed look at static pods in Kubernetes. This special type of pod allows the Kubelet to function independently of other components of the Kubernetes control plane.

## Introduction

Kubernetes is a complex system consisting of many components, including the kube-apiserver, kube-scheduler, and ETCD datastore. A central role is played by the Kubelet, which runs on every node in the cluster and is responsible for creating pods according to the instructions of the kube-apiserver.

But what happens if there is no kube-apiserver, kube-scheduler, or ETCD cluster? What if the Kubelet is operating alone on a node? This is where static pods come into play.

## What are Static Pods?

Static pods are pods that are managed directly by the Kubelet, without the intervention of the API server or other components of the Kubernetes cluster. These pods are created using pod definition files stored in a specific directory on the node.

### How They Work

The Kubelet on a host regularly reads the pod definition files from a specified directory to create the corresponding pods. This folder can be chosen freely and is configured via the `pod-manifest-path` option when starting the Kubelet service.

For example, the path could be configured as follows:
```sh
--pod-manifest-path=/etc/kubernetes/manifests
```


Alternatively, this path can also be defined in a configuration file passed with the `--config` option:

```yaml
staticPodPath: /etc/kubernetes/manifests
```

## Managing Static Pods

A static pod is not only created but also monitored and restarted by the Kubelet if the application crashes. Changes to the pod definition files cause the Kubelet to recreate the affected pods. Deleting a file will automatically remove the corresponding pod.

Since the Kubelet can manage pods independently in this way, it is possible to define and operate essential cluster components, such as the API server, controller, and ETCD, as static pods.

## Differences Between Static Pods and DaemonSets

A common point of confusion is the difference between static pods and DaemonSets. While static pods are created directly by the Kubelet independently of the Kubernetes control plane, DaemonSets are managed via the kube-apiserver and a DaemonSet controller. However, both types of pods are ignored by the kube-scheduler.

## Use Cases

Static pods are particularly useful for running the components of the Kubernetes control plane itself. By placing the appropriate pod definition files in the manifest directory, key services such as the API server, controller, and ETCD can be provided as pods. If any of these services crash, the Kubelet ensures they are automatically restarted.

## Conclusion

Static pods offer a robust way to manage Kubernetes nodes independently and provide essential services without direct dependence on the control plane. They are an important part of understanding and operating a Kubernetes cluster.


