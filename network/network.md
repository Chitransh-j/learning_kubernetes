# Networking in K8s Environment

### What is a Service in Kubernetes?

- A Service in Kubernetes is a stable network endpoint that exposes a set of Pods.

- Since Pods are ephimeral and have changing IP addresses, a Service provides a stable IP and a stable DNS name. Also some Load balancing across matching Pods.

- A service knows always the IPs of all the pods under its banner. To consistenly access, we use a service.

- It selects Pods using labels. All pods under the specified labels fall under the same service.


```
Deployment → creates Pods (app=nginx)
Service → selects Pods with app=nginx
```

---- 
### Types of Services:


#### 1. ClusterIP: (Default)
- Accessible only from inside the cluster
- Load balancing handled by kube-proxy
- Internal Pod (wants to communicate) → ClusterIP → kube-proxy → Target Pod (the pod targetted for comm)


#### 2. NodePort: 
- It allows a bunch of pods to be exposed to an external env under the service banner.
- It exposes the Service on every node present in the cluster at a port. 
- Even if Pod is on another node, kube-proxy forwards traffic correctly.
- ```<NodeIP>:NodePort```
- External Client → NodeIP:NodePort → kube-proxy → Pod


#### 3. LoadBalancer: 
- Used in cloud environments
- Cloud provider creates a real external load balancer.
- Gets a public IP.
- Internet → Cloud Load Balancer → Service → Pod 


----- 
<br/>

### Need of a Regulator 
- By default ,all Pods can talk to all other Pods in the cluster (Flat network model).

- This is where we need to regulate to ensure safety measures. 

- A new kind of object : NetworkPolicy comes in aid to address this issue.




