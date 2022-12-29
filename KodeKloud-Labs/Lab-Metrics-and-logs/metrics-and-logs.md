## deploy metricsserver
```
git clone https://github.com/kodekloudhub/kubernetes-metrics-server.git
k apply -f kubernetes-metrics-server

k top node
k top pod
```

## Stream Logs
`k logs webapp-1 -f`