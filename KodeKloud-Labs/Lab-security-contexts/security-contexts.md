## Edit the pod ubuntu-sleeper to run the sleep process with user ID 1010.
``
kubectl get pods ubuntu-sleeper -o=yaml > sleeper.yaml
k delete pod ubuntu-sleeper --grace-period=0 --force 

vi sleeper.yaml 

spec:
  containers:
  - command:
    - sleep
    - "4800"
    image: ubuntu
    imagePullPolicy: Always
    name: ubuntu
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-6hmvw
      readOnly: true
    securityContext:
      runAsUser: 1010
``

## Update pod ubuntu-sleeper to run as Root user and with the SYS_TIME capability.

``
spec:
  containers:
  - command:
    - sleep
    - "4800"
    image: ubuntu
    imagePullPolicy: Always
    name: ubuntu
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-6hmvw
      readOnly: true
    securityContext:
      runAsUser: 0
      capabilities:
        add: ["SYS_TIME"]
``