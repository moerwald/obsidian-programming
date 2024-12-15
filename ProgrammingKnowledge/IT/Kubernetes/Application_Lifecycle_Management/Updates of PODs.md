
# Understanding Updates and Rollbacks in Kubernetes Deployments

### Introduction
In the context of Kubernetes, managing updates and rollbacks of deployments is essential for maintaining application stability and ensuring continuous delivery. This article provides a comprehensive guide on how to perform updates and rollbacks in Kubernetes deployments.

### Creating and Managing Rollouts

#### Initial Deployment
When you create a deployment for the first time, Kubernetes triggers a rollout. This initial rollout is considered **Revision 1**.

#### Updating a Deployment
When you update the application (e.g., by changing the container image version), Kubernetes creates a new rollout, resulting in **Revision 2**. Each subsequent update generates a new revision, allowing you to track changes and revert to previous versions if needed.

#### Viewing Rollout Status
To check the status of a rollout, use the following command:
```bash
kubectl rollout status [deployment_name]
```

#### Viewing Rollout History
To see the history of rollouts, use:
```bash
kubectl rollout history [deployment_name]
```

![[Pasted image 20240806213623.png]]
### Deployment Strategies

#### Recreate Strategy
This strategy involves destroying all instances of the current version before deploying new instances. While simple, it causes downtime as the application becomes temporarily unavailable. This is not the default strategy.

#### Rolling Update Strategy
This default strategy updates instances gradually, ensuring that some instances of the application remain available during the update process. It updates the application in a seamless manner, reducing downtime.

### Performing Updates

#### Using Deployment Files
Update the deployment definition file to reflect the new changes and apply them with:
```bash
kubectl apply -f [deployment_file]
```
This triggers a new rollout and creates a new revision.

#### Using kubectl set image
To update the container image directly, use:
```bash
kubectl set image deployment/[deployment_name] [container_name]=[new_image]
```
Be cautious with this approach as it might lead to inconsistencies with your deployment files.

### Detailed Deployment Information
To get detailed information about a deployment, use:
```bash
kubectl describe deployment [deployment_name]
```
This command shows how Kubernetes scales replicas during updates, whether using the Recreate or Rolling Update strategy.

### Rollbacks

#### Rolling Back to a Previous Revision
If an update causes issues, you can rollback to a previous revision with:
```bash
kubectl rollout undo deployment/[deployment_name]
```
Kubernetes destroys the pods in the current replicaset and restores the previous replicaset.

#### Listing Replicasets
To see the replicasets, use:
```bash
kubectl get replica sets
```
Before rollback, you will see the current replicaset with the updated pods and the old replicaset with zero pods. After rollback, this reverses.

![[Pasted image 20240806214836.png]]

### Summary of Commands
- **Create a Deployment:** `kubectl create -f [deployment_file]`
- **List Deployments:** `kubectl get deployments`
- **Update a Deployment:** `kubectl apply -f [deployment_file]` or `kubectl set image deployment/[deployment_name] [container_name]=[new_image]`
- **View Rollout Status:** `kubectl rollout status [deployment_name]`
- **Undo a Rollout:** `kubectl rollout undo deployment/[deployment_name]`

### Conclusion
Understanding updates and rollbacks in Kubernetes is crucial for maintaining application reliability and minimizing downtime. By following these guidelines and using the provided commands, you can effectively manage your Kubernetes deployments.


#Kubernetes