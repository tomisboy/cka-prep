# Cheatcheat:
https://kubernetes.io/docs/reference/kubectl/cheatsheet/

## autocomplete
```
source <(kubectl completion bash) # set up autocomplete in bash into the current shell, bash-completion package should be installed first.
echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanently to your bash shell.

```
## Alias
```
alias k=kubectl
complete -o default -F __start_kubectl k
```
## Creating YAML:
Generate POD Manifest YAML file (-o yaml). Don't create it(--dry-run)

`kubectl run nginx --image=nginx --dry-run=client -o yaml`

`kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml`

## imperativ vs declaratriv
### Services :
*Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379*

``kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml``
(This will automatically use the pod's labels as selectors)
<br>
or<br>
``kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml`` 
(This will not use the pods labels as selectors, instead it will assume selectors as app=redis. You cannot pass in selectors as an option. So it does not work very well if your pod has a different label set. So generate the file and modify the selectors before creating the service)


*Create a Service named nginx of type NodePort to expose pod nginx's port 80 on port 30080 on the nodes:*

``kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml``
((This will automatically use the pod's labels as selectors, but you cannot specify the node port. You have to generate a definition file and then add the node port in manually before creating the service with the pod.))
<br>
or<br>
``kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml`` 
(This will not use the pods labels as selectors)


## fast delete
`kubectl delete pods <pod> --grace-period=0 --force`


## get current context 
``kubectl config current-context``

## switch context
``kubectl config use-context cluster2``

## switch context when using different kubeconfigfile
``kubectl config --kubeconfig=/root/my-kube-config use-context research``

## get shortcuts and api ressources 
` k api-resources `


## link to install cni
https://v1-22.docs.kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/#set-up-the-first-control-plane-node

## place pod on node x
nodeName : nodeX