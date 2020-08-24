# Security

## 7. Network Policy

Ingress Traffic: the requests from outside.
Egress Traffic: the requests to outside.

Network policy is an object, linking a policy to a pod.

```yaml
#network-policy.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-policy
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          name: api-pod
    ports:
    - protocol: TCP
      port: 3306
```