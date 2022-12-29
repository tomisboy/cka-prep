## A new user michelle joined the team. She will be focusing on the nodes in the cluster. Create the required ClusterRoles and ClusterRoleBindings so she gets access to the nodes.

```
controlplane ~ ➜  k create clusterrole nodes-michelle --verb=get,list,watch --resource=nodes --dry-run=client -o=yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  creationTimestamp: null
  name: nodes-michelle
rules:
- apiGroups:
  - ""
  resources:
  - nodes
  verbs:
  - get
  - list
  - watch


controlplane ~ ➜  k create clusterrolebinding nodes-michelle-binding --clusterrole=nodes-michelle --user=michelle --dry-run=client -o=yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  creationTimestamp: null
  name: nodes-michelle-binding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: nodes-michelle
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: michelle

```
## michelle's responsibilities are growing and now she will be responsible for storage as well. Create the required ClusterRoles and ClusterRoleBindings to allow her access to Storage.
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  creationTimestamp: null
  name: storage-admin


rules:
- apiGroups:
  - ""
  resources:
  - persistentvolumes
  verbs:
  - get
  - list
  - watch
  - create
  - delete

- apiGroups:
  - ""
  resources:
  - storageclasses
  verbs:
  - get
  - list
  - watch
  - create
  - delete




controlplane ~ ➜   k create clusterrolebinding michelle-storage-admin  --clusterrole=storage-admin --user=michelle --dry-run=client -o=yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  creationTimestamp: null
  name: michelle-storage-admin
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: storage-admin
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: michelle

```





