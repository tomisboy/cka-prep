

## Create a pod with the ubuntu image to run a container to sleep for 5000 seconds. Modify the file ubuntu-sleeper-2.yaml.

```
apiVersion: v1 
kind: Pod 
metadata:
  name: ubuntu-sleeper-2 
spec:
  containers:
  - name: ubuntu
    image: ubuntu
    command: ["sleep"]
    args: ["5000"]
```

## Create a pod with the given specifications. By default it displays a blue background. Set the given command line arguments to change it to green.
```
apiVersion: v1
kind: Pod
metadata:
  name: webapp-green
  labels:
      name: webapp-green
spec:
  containers:
  - name: webapp-green
    image: kodekloud/webapp-color
    args: ["--color", "green"]
```