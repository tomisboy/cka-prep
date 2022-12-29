## Configure a volume to store these logs at /var/log/webapp on the host.
```
k get pods webapp -o=yaml > webapp.yaml
vi webapp.yaml

apiVersion: v1
kind: Pod
metadata:
  name: webapp
  namespace: default
spec:
  containers:
  - env:
    - name: LOG_HANDLERS
      value: file
    image: kodekloud/event-simulator
    imagePullPolicy: Always
    name: event-simulator
    volumeMounts:
    - mountPath: /log
      name: webapp-volume
  
  volumes:
  - name: webapp-volume
    hostPath:
      path:  /var/log/webapp
      type: Directory


kubectl replace -f webapp.yaml --force 
```

## Create a Persistent Volume with the given specification.
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name:  pv-log
spec:
  capacity:
    storage: 100Mi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: "/pv/log"
  persistentVolumeReclaimPolicy: Retain

```

## Let us claim some of that storage for our application. Create a Persistent Volume Claim with the given specification.
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: claim-log-1   
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 50Mi
```


## Update the webapp pod to use the persistent volume claim as its storage.
```
apiVersion: v1
kind: Pod
metadata:
  name: webapp
  namespace: default
spec:
  containers:
  - env:
    - name: LOG_HANDLERS
      value: file
    image: kodekloud/event-simulator
    imagePullPolicy: Always
    name: event-simulator
    volumeMounts:
    - mountPath: /log
      name: webapp-volume

  volumes:
  - name: webapp-volume
    persistentVolumeClaim:
      claimName: claim-log-1


 k replace -f webapp-pvc.yaml --force
```

