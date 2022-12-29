https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/

## What is the current version of the cluster?
`kubelet --version`


Check for Tains, ensure that on other Nodes the Pods can be shedduled

## Upgrade Controlplane:

### Drain Controlplane to mark it UnSchedulable:
`kubectl drain controlplane  --ignore-daemonsets`

### Update Kubeadm:
```
 apt-mark unhold kubeadm && \
 apt-get update && apt-get install -y kubeadm=1.25.0-00 && \
 apt-mark hold kubeadm
```

### Update Kubernetes
`sudo kubeadm upgrade apply v1.25.0`

### Update Kubelet
```
apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.25.0-00 kubectl=1.25.0-00 && \
apt-mark hold kubelet kubectl

sudo systemctl daemon-reload
sudo systemctl restart kubelet
```

### Mark the controlplane node as "Schedulable" again
``kubectl uncordon controlplane ``

## Upgrade node.:

### Drain node to mark it UnSchedulable:
`kubectl drain node01  --ignore-daemonsets`
SSH into node:

### Update Kubeadm:
```
 apt-mark unhold kubeadm && \
 apt-get update && apt-get install -y kubeadm=1.25.0-00 && \
 apt-mark hold kubeadm
```
### Update Kubernetes
`sudo kubeadm upgrade node`

### Update Kubelet
```
apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.25.0-00 kubectl=1.25.0-00 && \
apt-mark hold kubelet kubectl

sudo systemctl daemon-reload
sudo systemctl restart kubelet
```
back to master controlplane

### Mark the node node as "Schedulable" again
``kubectl uncordon node01 ``