# Networking

## 4. Ingress

### Ingress Controller

Check the namespace where the ingress resource is deployed.
```shell script
master $ kubectl get ingress --all-namespaces
NAMESPACE   NAME                 CLASS    HOSTS   ADDRESS   PORTS   AGE
app-space   ingress-wear-watch   <none>   *                 80      10m
```

Create an ingress resource.
```shell script
master $ cat ingress-pay.yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: test-ingress
  namespace: critical-space
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /pay
        backend:
          serviceName: pay-service
          servicePort: 8282
```

#### Practice
Deploy an Ingress Controller

Step 1. create a namespace called ingress-space.
```shell script
kubectl create namespace ingress-space
```

Step 2. create a configMap in the namespace.
```shell script
kubectl create configmap nginx-configuration -n ingress-space
```

Step 3. create a service account in the namespace.
```shell script
kubectl create serviceaccount ingress-serviceaccount --namespace ingress-space
```

Step 4. create roles and roleBindings for the account.

```shell script
master $ kubectl get roles,rolebindings --namespace ingress-space
NAME                                          CREATED AT
role.rbac.authorization.k8s.io/ingress-role   2020-08-27T02:19:18Z

NAME                                                         ROLE                AGE
rolebinding.rbac.authorization.k8s.io/ingress-role-binding   Role/ingress-role   58s
```

Step 5. create a deployment for the ingress-controller.
```shell script
master $ cat ingress-controller.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ingress-controller
  namespace: ingress-space
spec:
  replicas: 1
  selector:
    matchLabels:
      name: nginx-ingress
  template:
    metadata:
      labels:
        name: nginx-ingress
    spec:
      serviceAccountName: ingress-serviceaccount
      containers:
        - name: nginx-ingress-controller
          image: quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.21.0
          args:
            - /nginx-ingress-controller
            - --configmap=$(POD_NAMESPACE)/nginx-configuration
            - --default-backend-service=app-space/default-http-backend
          env:
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: POD_NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
          ports:
            - name: http
              containerPort: 80
            - name: https
              containerPort: 443
```

Step 6. create a service to make Ingress available to external users.
```shell script
kubectl expose deployment -n ingress-space ingress-controller --type=NodePort --port=80 --name=ingress --dry-run -o yaml >ingress.yaml
```

```shell script
master $ cat ingress-service.yaml
---
apiVersion: v1
kind: Service
metadata:
  name: ingress
  namespace: ingress-space
spec:
  type: NodePort
  ports:
  - port: 80
    targetPort: 80
    protocol: TCP
    nodePort: 30080
    name: http
  - port: 443
    targetPort: 443
    protocol: TCP
    name: https
  selector:
    name: nginx-ingress
```

Step 7. create the ingress resource.
```shell script
master $ cat ingress-resource.yaml
---
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: ingress-wear-watch
  namespace: app-space
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
spec:
  rules:
  - http:
      paths:
      - path: /wear
        backend:
          serviceName: wear-service
          servicePort: 8080
      - path: /watch
        backend:
          serviceName: video-service
          servicePort: 8080
```