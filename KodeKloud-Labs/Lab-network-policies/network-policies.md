## Create a network policy to allow traffic from the Internal application only to the payroll-service and db-service.

![img](.\kubernetes-ckad-network-policies-9.jpg)

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: internal-policy
spec:
  podSelector:
    matchLabels:
      name: internal

  policyTypes:
    - Ingress
    - Egress
  ingress: ## Ingress an Internal Pod is allowed
    - {}

  egress:
  - to :
    - podSelector:
        matchLabels:
          name: mysql
    ports:
      - protocol: TCP
        port: 3306

  - to :
    - podSelector:
        matchLabels:
          name: payroll
    ports:
      - protocol: TCP
        port: 8080 
```