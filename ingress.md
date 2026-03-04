# Kubernetes Request Flow with Ingress Controller

### INGRESS
- In a typical Kubernetes setup, external users access applications through an Ingress architecture. This setup allows multiple services inside the cluster to be exposed through a single external entry point while maintaining internal service discovery and load balancing. 

- This Ingress service has to ofc be exposed using a cloud native load Balancer , but this is a one time job and you need not maintain load balancers for each service. BIG WIN


## Key components involved:

The system routes external traffic through these layers until it reaches the target application container.

### Architecture Diagram
```
User
  │
  ▼
Cloud Load Balancer (Public IP)
  │
  ▼
Service (type: LoadBalancer)
  │
  ▼
NGINX Ingress Controller Pods
  │
  ▼
Ingress Rules
  │
  ▼
Service (ClusterIP)
  │
  ▼
Application Pods
```


```The LoadBalancer exposes the cluster, while the Ingress Controller performs Layer-7 routing based on rules defined in the Ingress resource.```

---- 

### Component Breakdown

#### Ingress Controller 
   - The Ingress Controller is the actual reverse proxy implementation that processes incoming HTTP/HTTPS requests.
   - e.g: Nginx-ingres-controller 
   - It is deployed as a Deploymentm, running multiple NGINX pods

   - Example structure:
        ```
        Deployment
        ├── nginx-ingress-controller-pod-1
        ├── nginx-ingress-controller-pod-2
        └── nginx-ingress-controller-pod-3
        ```

   - A Service exposes these pods internally and connects them to the external LoadBalancer.

Responsibilities:
- Acts as a Layer-7 reverse proxy
- Watches Kubernetes for Ingress resources
- Dynamically generates NGINX routing configuration

#### Ingress Resource

The Ingress object defines the routing rules for incoming requests. (kind of like the nginx.conf routing rules)

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: api-routing
spec:
  rules:
  - host: api.example.com
    http:
      paths:
      - path: /users
        pathType: Prefix
        backend:
          service:
            name: user-service
            port:
              number: 80

```
It means:
api.example.com/users → user-service (All the requests coming to this endpoint shall be redirected to that service)


