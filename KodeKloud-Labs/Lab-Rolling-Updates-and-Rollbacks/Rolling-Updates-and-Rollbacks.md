## Set Image Let us try that. Upgrade the application by setting the image on the deployment to kodekloud/webapp-color:v2
`kubectl set image deployments/frontend  simple-webapp=kodekloud/webapp-color:v2`

## Change the deployment strategy to Recreate
```
kubectl edit deployments.apps frontend 

  strategy:
    type: Recreate


-->
  Normal  ScalingReplicaSet  45s    deployment-controller  Scaled down replica set frontend-b9c6c8d8 to 0
  Normal  ScalingReplicaSet  12s    deployment-controller  Scaled up replica set frontend-86c68cc76c to 4
```


