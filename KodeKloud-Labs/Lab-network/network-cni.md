## default path What is the path configured with all binaries of CNI supported plugins?
`ls /opt/cni/bin/`


## What binary executable file will be run by kubelet after a container and its associated namespace are created.
`cat /etc/cni/net.d/10-flannel.conflist `

## What network range are the nodes in the cluster part of?
```
ip a | grep eth0
controlplane ~ ➜  ipcalc 10.28.243.9/24
Address:   10.28.243.9          00001010.00011100.11110011. 00001001
Netmask:   255.255.255.0 = 24   11111111.11111111.11111111. 00000000
Wildcard:  0.0.0.255            00000000.00000000.00000000. 11111111
=>
Network:   10.28.243.0/24       00001010.00011100.11110011. 00000000
HostMin:   10.28.243.1          00001010.00011100.11110011. 00000001
HostMax:   10.28.243.254        00001010.00011100.11110011. 11111110
Broadcast: 10.28.243.255        00001010.00011100.11110011. 11111111
Hosts/Net: 254                   Class A, Private Internet
```

## Ip Range from Pods
```
 k run busybox --image busybox -- sleep 20000
 k exec -it busybox -- /bin/sh -c "ip a" | grep eth
 13: eth0@if14: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1376 qdisc noqueue 
    link/ether 72:c2:70:17:40:0b brd ff:ff:ff:ff:ff:ff
    inet 10.50.192.1/16 brd 10.50.255.255 scope global eth0
```

## What is the IP Range configured for the services within the cluster?
```
controlplane ~ ➜  cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep cluster-ip-range
    - --service-cluster-ip-range=10.96.0.0/1
```
cat /var/lib/kube-proxy/config.conf