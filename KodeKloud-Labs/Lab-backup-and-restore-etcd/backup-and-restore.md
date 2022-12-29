## What is the version of ETCD running on the cluster?
AS ROOT
`Look at the ETCD Logs OR check the image used by ETCD pod.`

/etc/kubernetes/pki/etcd/server.crt
/etc/kubernetes/pki/etcd/ca.crt
## make snapshot of etcd
```
ETCDCTL_API=3 etcdctl --endpoints 127.0.0.1:2379 \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot save /opt/snapshot-pre-boot.db
```

### restore etcd
```
ETCDCTL_API=3 etcdctl --endpoints 127.0.0.1:2379 \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot restore \
--data-dir /var/lib/etcd-from-backup \
/opt/snapshot-pre-boot.db
```

## edit ETCD Config to Use new Folder /var/lib/etcd-from-backup
```
vi /etc/kubernetes/manifests/etcd.yaml 
 volumes:
  - hostPath:
      path: /etc/kubernetes/pki/etcd
      type: DirectoryOrCreate
    name: etcd-certs
  - hostPath:
      path: /var/lib/etcd-from-backup  # < change this to new location where snapshot is restored
      type: DirectoryOrCreate
    name: etcd-data

```

https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/