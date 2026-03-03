# Networking in K8s Environment

### What is a Service in Kubernetes?

- A Service in Kubernetes is a stable network endpoint that exposes a set of Pods.

- Since Pods are ephimeral and have changing IP addresses, a Service provides a stable IP and a stable DNS name. Also some Load balancing across matching Pods.

- A service knows always the IPs of all the pods under its banner. To consistenly access, we use a service.


### Need of a Regulator 
- By default ,all Pods can talk to all other Pods in the cluster (Flat network model).

- This is where we need to regulate to ensure safety measures. 

- A new kind of object : NetworkPolicy comes in aid to address this issue.
