## Get Authoization-mode
```
k describe pod -n kube-system kube-apiserver-controlplane | grep "authorization-mode"
      --authorization-mode=Node,RBAC    ## <----
```

## get roles 
``k get role.rbac``

## What are the resources the kube-proxy role in the kube-system namespace is given access to?
```
k describe  role.rbac -n kube-system kube-proxy 

Name:         kube-proxy
Labels:       <none>
Annotations:  <none>
PolicyRule:
  Resources   Non-Resource URLs  Resource Names  Verbs
  ---------   -----------------  --------------  -----
  configmaps  []                 [kube-proxy]    [get]

```


## Which account is the kube-proxy role assigned to?
```
k get rolebindings.rbac.authorization.k8s.io  -n kube-system kube-proxy -o=yaml
k describe rolebindings.rbac.authorization.k8s.io  -n kube-system kube-proxy 

Name:         kube-proxy
Labels:       <none>
Annotations:  <none>
Role:
  Kind:  Role
  Name:  kube-proxy
Subjects:
  Kind   Name                                             Namespace
  ----   ----                                             ---------
  Group  system:bootstrappers:kubeadm:default-node-token    # <---

```

## Check permissions
### Inspect the permissions granted to the user. Check if the user can list pods in the default namespace.
`kubectl auth can-i list pods --as dev-user`


## Create the necessary roles and role bindings required for the dev-user to create, list and delete pods in the default namespace.
- Role: developer
- Role Resources: pods
- Role Actions: list
- Role Actions: create
- Role Actions: delete
- RoleBinding: dev-user-binding
- RoleBinding: Bound to dev-user

```
kubectl create role developer --verb=list --verb=delete --verb=create --verb=get --resource=pods --dry-run=client -o=yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  creationTimestamp: null
  name: developer
rules:
- apiGroups:
  - ""
  resources:
  - pods
  verbs:
  - list
  - delete
  - create
  - get

kubectl create rolebinding dev-user-binding --role=developer --user=dev-user --dry-run=client -o=yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  creationTimestamp: null
  name: dev-user-binding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: developer
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: dev-user
```

` kubectl auth can-i get pods/blue --as dev-user --namespace blue`

## Add a new rule in the existing role developer to grant the dev-user permissions to create deployments in the blue namespace.
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  creationTimestamp: "2022-12-29T15:50:16Z"
  name: developer
  namespace: blue
  resourceVersion: "2754"
  uid: 475cc837-c2a4-4a42-ab41-ca64b021fe2f
rules:
- apiGroups:
  - ""
  resourceNames:
  - blue-app
  - dark-blue-app
  resources:
  - pods
  verbs:
  - get
  - watch
  - create
  - delete

  
- apiGroups:
  - apps
  resources:
  - deployments
  verbs:
  - get
  - watch
  - create
  - delete
~           
~             
```