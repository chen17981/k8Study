# Security

## 2. Authentication
K8s does not manage users, but manage service account.
```shell script
kubectl create serviceaccount sa1

kubectl list serviceaccount
```
All user requests go to kube-apiserver, and kube-apiserver first authenticate requests, then process it.

There are multiple ways for authentication,
* static password file
* static token file
* certificates
* identity services

### TLS Certificates

* What are TLS certs?
* How does k8s use certs?
* How to generate them?
* How to configure them?
* How to view them?
* How to troubleshoot issues related to certs?
