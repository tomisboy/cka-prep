## Create a taint on node01 with key of spray, value of mortein and effect of NoSchedule
`kubectl taint nodes node01 spray=mortein:NoSchedule`

## Create another pod named bee with the nginx image, which has a toleration set to the taint mortein.
```
apiVersion: v1
kind: Pod
metadata:
  name: bee
spec:
  containers:
  - image: nginx
    name: bee
  restartPolicy: Always
  tolerations:
    - key: "spray"
      operator: "Equal"
      value: "mortein"
      effect: "NoSchedule"       
```


## Remove the taint on controlplane, which currently has the taint effect of NoSchedule.
`kubectl taint nodes controlplane node-role.kubernetes.io/control-plane:NoSchedule-`