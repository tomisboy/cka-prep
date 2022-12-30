## Where is the configuration file located for configuring the CoreDNS service?



```
k describe pods -n kube-system coredns-6d4b75cb6d-8qwpg 
k describe replicatset -n kube-system coredns-6d4b75cb6d-8qwpg 
Args:
      -conf
      /etc/coredns/Corefile  #<<<<--
    State:          Running
      Started:      Fri, 30 Dec 2022 11:55:19 +0000
    Ready:          True
    Restart Count:  0
    Limits:
      memory:  170Mi
    Requests:
      cpu:        100m
      memory:     70Mi
    Liveness:     http-get http://:8080/health delay=60s timeout=5s period=10s #success=1 #failure=5
    Readiness:    http-get http://:8181/ready delay=0s timeout=1s period=10s #success=1 #failure=3
    Environment:  <none>
    Mounts:
      /etc/coredns from config-volume (ro)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-2jnfz (ro)
Conditions:
```