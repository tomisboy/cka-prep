## How many Deployments, Pods and ReplicaSets exist on the system?
`k get all`


## Create a new Deployment with the below attributes using your own deployment definition file.
###  Name: httpd-frontend;
### Replicas: 3;
### Image: httpd:2.4-alpine

`k create deployment httpd-frontend --image httpd:2.4-alpine --replicas=3`