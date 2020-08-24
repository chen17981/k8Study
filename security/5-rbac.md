# Security

## 5. RBAC

### API Groups
The core group
/api -> /v1 -> pods

The named group
/apis -> /apps -> /v1 -> /deployments

```shell script
kubectl proxy                  # starting kubectl proxy

curl http://localhost:8001 -k  # list all api paths.
```

### RBAC
Create a role
```yaml
# dev-role.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: dev
rules:
- apiGroups: ["]
  resources: ["pods"]
  verbs: ["list", "get", "create", "update"]
```

Binding a role to a user
```yaml
#binding.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata: 
  name: dev-binding
subject:
- kind: User
  name: dev-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: dev
  apiGroup: rbac.authorization.k8s.io
```

To view roles and rolebindings
```shell script
kubectl get roles

kubectl get rolebindings
```

Check access
```shell script
kubectl auth can-i create deployments

kubectl auth can-i create deployments --as dev-user --namespace test
```

### Cluster Roles and Rolebindings
View namespaced resources, 
```shell script
kubeclt api-resources --namespaced=true
```

View non-namespaced resources,
```shell script
kubectl api-resources --namespaced=false
```

