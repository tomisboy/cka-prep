## The elephant pod runs a process that consume 15Mi of memory. Increase the limit of the elephant pod to 20Mi.
```
kubectl run elephant --image polinux/stress  --dry-run=client -o=yaml > elephant.yaml

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: elephant
  name: elephant
spec:
  containers:
  - image: polinux/stress
    name: elephant
    resources:
      limits:
        memory: 20Mi
```