## Update the environment variable on the POD to display a green background
```
kubectl get pods webapp-color -o=yaml > new-pink-app.yaml

vi new-pink-app.yaml


apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2022-12-28T12:51:01Z"
  labels:
    name: webapp-color
  name: webapp-color
  namespace: default
  resourceVersion: "680"
  uid: 7278feef-1677-4064-84b7-b2db5bf6d34c
spec:
  containers:
  - env:
    - name: APP_COLOR
      value: green


k apply -f new-pink-app.yaml
```

## Identify the database host from the config map db-config
`kubectl describe cm db-config `


## Create a new ConfigMap for the webapp-color POD. Use the spec given below.
```
kubectl create configmap my-config --from-literal=APP_COLOR=darkblue 

oder:
apiVersion: v1
kind: ConfigMap
metadata:
  name: webapp-config-map
data:
  APP_COLOR: "darkblue"
```


## Update the environment variable on the POD to use the newly created ConfigMap
```
apiVersion: v1
kind: Pod
metadata:
  labels:
    name: webapp-color
  name: webapp-color
  namespace: default
spec:
  containers:
  - env:
    - name: APP_COLOR
      valueFrom:
        configMapKeyRef:
          name: webapp-config-map           # The ConfigMap this value comes from.
          key: APP_COLOR


    image: kodekloud/webapp-color
    imagePullPolicy: Always
    name: webapp-color

```

## The reason the application is failed is because we have not created the secrets yet. Create a new secret named db-secret with the data given below.
```
kubectl create secret generic db-secret --from-literal=DB_Host=sql01 --from-literal=DB_User=root --from-literal=DB_Password=password123
```

## Configure webapp-pod to load environment variables from the newly created secret.
```
apiVersion: v1
kind: Pod
metadata:
  labels:
    name: webapp-pod
  name: webapp-pod
spec:
  containers:
  - image: kodekloud/simple-webapp-mysql
    imagePullPolicy: Always
    name: webapp
    envFrom:
    - secretRef:
        name: db-secret
```