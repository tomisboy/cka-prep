## How many static pods exist in this cluster in all namespaces?
```
controlplane ~ ➜  k get pods -A
NAMESPACE     NAME                                  
kube-system   coredns-6d4b75cb6d-d65qg              
kube-system   coredns-6d4b75cb6d-qf7bf              
kube-system   etcd-controlplane    <--                  
kube-system   kube-apiserver-controlplane <--
kube-system   kube-controller-manager-controlplane <--
kube-system   kube-flannel-ds-kx9xr                 
kube-system   kube-flannel-ds-q8pdg                 
kube-system   kube-proxy-nhtsl                      
kube-system   kube-proxy-pklqr                      
kube-system   kube-scheduler-controlplane  <--
```

## Create a static pod named static-busybox that uses the busybox image and the command sleep 1000
`k run static-busybox --image busybox sleep 1000 --dry-run=client -o=yaml > /etc/kubernetes/manifests/busyboy.yaml`


## We just created a new static pod named static-greenbox. Find it and delete it.

```
ssh node01
ps aux | grep kubelet 
Search for --pod-manifest-path or --config

or cat /var/lib/kubelet/config.yaml
```
