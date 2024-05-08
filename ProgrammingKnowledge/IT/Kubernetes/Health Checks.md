
# Zusammenfassung

Let’s dive into the world of Kubernetes probes. These probes play a crucial role in ensuring the reliability and availability of containers within a pod. Here’s a concise summary of the key points from the provided link:

1. **Liveness Probes**:
    
    - Purpose: Detect when a container is in an unrecoverable state.
    - Example Scenario: Catching a deadlock where an application is running but unable to make progress.
    - Implementation: Use a low-cost HTTP endpoint (similar to readiness probes) with a higher `failureThreshold`.
    - Effect: Helps maintain application availability despite bugs.
    - Caution: Must be configured carefully to avoid cascading failures.
2. **Readiness Probes**:
    
    - Purpose: Determine when a container is ready to accept traffic.
    - Significance: A pod is considered ready only when all its containers are ready.
    - Use Case: Controlling which pods serve as backends for services.
    - Impact: When a pod is not ready, it’s removed from service load balancers.
3. **Startup Probes**:
    
    - Purpose: Indicate when a container application has successfully started.
    - Interaction with Other Probes: Liveness and readiness probes wait until the startup probe succeeds.
    - Use Case: Ensuring liveness checks don’t interfere with slow-starting containers.
	
# Detailierte Infos

[kubernetes.io](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)


#Kubernetes 