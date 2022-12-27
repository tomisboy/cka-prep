## Create a new pod with the nginx image.
`kubectl run nginx --image=nginx`

## How many pods are created now?
`k get pods -n default`

## What is the image used to create the new pods?
`k describe pod  newpods-9rtfc`  --> busybox


## Which nodes are these pods placed on?
`k describe pod  newpods-9rtfc`  --> busybox
```
Name:         newpods-9rtfc
Namespace:    default
Priority:     0
Node:         controlplane/172.25.1.75   <--
```

## What does the READY column in the output of the kubectl get pods command indicate?
`Running Containers in POD/Total Containers in POD`

## Delete the webapp Pod.
` k delete pods webapp `
## Create a new pod with the name redis and with the image redis123.
### Use a pod-definition YAML file. And yes the image name is wrong!


```
apiVersion: v1
kind: Pod
metadata:
  name: redis
spec:
  containers:
  - name: redis
    image: redis123
```


## Now change the image on this pod to redis.
`kubectl edit pod redis `
