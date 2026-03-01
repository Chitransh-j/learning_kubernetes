## Deployments
Pods are rarely created out on their own in a prod environment. They are created as a part of deployments.

### In Kubernetes 
- A deployment creates a replicaSet (another type of K8s resource) , which in turn creates the specified number of pods per the manifest. 

- A K8s deployment resource is made in such a way that it EXPECT changes. Any other running resouce would decline change but a deployment handles them in an efficient manner.

- A change in a deployment file (and kubectl applying it) leads to creation of a new replica set and deletion of old one instantly. The process happens in such a manner that we get zero downtime.


### Commands for Rollout Controls
```bash
kubectl rollout history deploy <deployment-name> # Lists down all the revisions (basically versions of a deployment)

kubectl rollout undo <deployment-name> # switch to the last deployment revision
```