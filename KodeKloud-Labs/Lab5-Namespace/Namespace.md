## Create a POD in the finance namespace.
`kubectl run --image redis redis --namespace finance`

## Which namespace has the blue pod in it?
`kubectl get pods -A`