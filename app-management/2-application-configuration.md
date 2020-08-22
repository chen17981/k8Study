# Application Management

## Rolling Update

Deployment Strategy
* Default: rolling update.

RollBack

```shell script
kubectl rollout undo deployment/myapp-deployment
```

Command Summary
* Create
```shell script
kubectl create -f deployment-def.yml
```

* Get
```shell script
kubectl get deployments
```

* Update
```shell script
kubectl apply -f deployment-def.yml

kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1
```

* Status
```shell script
kubectl rollout status deployment/myapp-deployment

kubectl rollout history deployment/myapp-deployment
```

* Rollback
```shell script
kubectl rollout undo deployment/myapp
```

## Useful links

* Performing rolling updates 
https://cloud.google.com/kubernetes-engine/docs/how-to/updating-apps#kubectl-set