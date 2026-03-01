## Storage in Kubernetes

It is not ideal to store data directly into pods , as they would eventually die out and their data isn't persisted anywhere. So we need to have something external at the namespace level which takes care of persisting our data. Hence comes the concept of PV (persistent volumes) and PVC (persistent volume claims) 


### Persistent Volume 
- A PersistentVolume (PV) is a cluster-wide Kubernetes resource that **represents** the actual storage provisioned in the underlying infrastructure and made available for consumption inside the cluster. Again its just the representation and not the physical storage itself .

- It is an abstraction that represents and encapsulates the details of underlying storage, exposing it as a standardized, consumable resource inside Kubernetes.

```
Cloud Disk (real physical thing)
        ↓
PV (Kubernetes object describing it)
        ↓
PVC (request for it)
        ↓
Pod (mounts it)
```
----- 

### Persistent Volume Claim (PVC)
- A PersistentVolumeClaim (PVC) is a namespace-scoped request for storage made by an **application**.

- It represents demand. If PV is supply, PVC is demand.

A PVC does NOT describe infrastructure details.It only declares demands of the app:

- How much storage (e.g., 10Gi) - “I need 20Gi”
- Access mode (ReadWriteOnce, ReadWriteMany) - “I need ReadWriteMany”
- Storage class (performance tier) - “I need this performance tier”


#### Is PVC infrastructure independent?
- Yes. The same PVC can work on AWS, Azure, NFS, etc. The app does not change.
Only the backend storage changes.

- The Decoupling of PV and PVC is made in this order so that if there is change in storage type, only on one of the resources shall handle it. The entire logic of a varying storage type is kept abstraced from the PVC and the PV shall handle it alone.

#### What happens after you create a PVC?
- Kubernetes looks for a matching PV. <br/>
If it finds one → it binds. 
If not → it may create one dynamically (if StorageClass exists).
If nothing matches → PVC stays Pending.

- For a successful bind, this condition must be true: PV.capacity ≥ PVC.request
- There exists a 1:1 relation between a PVC and a bound PV.


#### What if PV is bigger than PVC?

It still binds (PV ≥ PVC rule). PVC does NOT increase in size. The underlying disk may be bigger, but PVC only asked for minimum required size.


---- 
### What do we gain with PV and PVC ?
- The PVC gets mounted on the pod(s) as volume. The pod(s) can now access the persistent storage to store data.

- A single PVC can be mounted to multiple pods.