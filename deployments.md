## Deployments
Pods are rarely created out on their own in a prod environment. They are created as a part of deployments.

In Kubernetes -> 
A deployment creates a replicaSet (another type of K8s resource) , which in turn creates the specified number of pods per the manifest. 
