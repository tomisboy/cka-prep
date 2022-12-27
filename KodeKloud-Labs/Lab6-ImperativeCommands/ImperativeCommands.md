## Deploy a redis pod using the redis:alpine image with the labels set to tier=db.
`kubectl run --image redis:alpine redis --labels tier=db --dry-run=client -o=yaml`



## Create ClusterIP: Create a service (ClusterIP) redis-service to expose the redis application within the cluster on port 6379.
`kubectl expose pod redis --port=6379 --name=redis-service`



## Create a deployment named webapp using the image kodekloud/webapp-color with 3 replicas.
Try to use imperative commands only. Do not create definition files. <br>
`kubectl create deployment --image kodekloud/webapp-color webapp --replicas=3`


## Create a new pod called custom-nginx using the nginx image and expose it on container port 8080.
Imperative Methode geht hier nicht (?)<br>
Es muss über die deklarative Methode der Port des Containers definiert werden <br>
```
kubectl run --image nginx custom-nginx --dry-run=client -o=yaml > custom-nginx.yaml
vi custom-nginx.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: custom-nginx
  name: custom-nginx
spec:
  containers:
  - image: nginx
    name: custom-nginx
    ports:                            <--
    - containerPort: 8080             <--

kubectl apply -f custom-nginx.yaml
kubectl expose pod custom-nginx --port=8080
```

## Create a new deployment called redis-deploy in the dev-ns namespace with the redis image. It should have 2 replicas.
``k create deployment --image redis redis-deploy --replicas=2 --namespace=dev-ns``



## Create a pod called httpd using the image httpd:alpine in the default namespace. Next, create a service of type ClusterIP by the same name (httpd). The target port for the service should be 80.
``kubectl run --image httpd:alpine httpd --port=80``
``kubectl expose pod httpd --port 80``