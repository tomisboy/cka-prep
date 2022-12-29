## Create a multi-container pod with 2 containers.
```
kubectl run yellow --image busybox --dry-run=client -o=yaml > yellow.yaml

vi yellow.yaml

apiVersion: v1
kind: Pod
metadata:
  labels:
    run: yellow
  name: yellow
spec:
  containers:
  - image: busybox
    name: lemon
    args: ["sleep", "1000"]

  - image: redis
    name: gold

```

## Edit the pod to add a sidecar container to send logs to Elastic Search. Mount the log volume to the sidecar container.
`kubectl get pod -n elastic-stack app -o=yaml > app.yaml`


```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2022-12-28T16:12:15Z"
  labels:
    name: app
  name: app
  namespace: elastic-stack
  resourceVersion: "1069"
  uid: c8e6d3b3-c3b0-444c-9390-293c772f2bf5
spec:
  containers:
  - image: kodekloud/event-simulator
    imagePullPolicy: Always
    name: app
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /log
      name: log-volume
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-rx22l
      readOnly: true


  - image: kodekloud/filebeat-configured
    name: sidecar
    volumeMounts:
    - mountPath: /var/log/event-simulator/
      name: log-volume

```