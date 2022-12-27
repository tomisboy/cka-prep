## How many ReplicaSets exist on the system?
`kubectl get replicatset` --> 0

## What is the image used to create the pods in the new-replica-set?
```
k describe replicasets.apps new-replica-set
Name:         new-replica-set
Namespace:    default
Selector:     name=busybox-pod
Labels:       <none>
Annotations:  <none>
Replicas:     4 current / 4 desired
Pods Status:  0 Running / 4 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  name=busybox-pod
  Containers:
   busybox-container:
    Image:      busybox777  <-----------
    Port:       <none>
    Host Port:  <none>
    Command:
      sh
      -c
      echo Hello Kubernetes! && sleep 3600
```


## Create a ReplicaSet using the replicaset-definition-1.yaml file located at /root/.
### There is an issue with the file, so try to fix it.
```
apiVersion: apps/v1  <--
kind: ReplicaSet
metadata:
  name: replicaset-1
spec:
  replicas: 2
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: nginx                      
```


## Fix the issue in the replicaset-definition-2.yaml file and create a ReplicaSet using it.
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicaset-2
spec:
  replicas: 2
  selector:
    matchLabels:
      tier: frontend    <--  muss gleich sein 
  template:
    metadata:
      labels:
        tier: frontend  <--  muss gleich sein 
    spec:
      containers:
      - name: nginx
        image: nginx
```


## Delete the two newly created ReplicaSets - replicaset-1 and replicaset-2
`k delete replicasets.apps replicaset-1 replicaset-2`

## Scale the ReplicaSet to 5 PODs.
```
kubectl scale --replicas 5 replicaset new-replica-set 
kubectl edit replicaset
```

