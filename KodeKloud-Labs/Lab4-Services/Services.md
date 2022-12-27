## Create a new service to access the web application using the service-definition-1.yaml file.
Name: webapp-service <br>
Type: NodePort <br>
targetPort: 8080 <br>
port: 8080 <br>
nodePort: 30080 <br>
selector: <br>
  name: simple-webapp <br>

```
---
apiVersion: v1
kind: Service
metadata:
  name: webapp-service
spec:
  type: NodePort
  ports:
    - targetPort: 8080
      port: 8080
      nodePort: 30080
  selector:
    name: simple-webapp
```