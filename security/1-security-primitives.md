# Security

## 1. Security Primitives

### Basics
* Who can access (Authentication)
  * Files -- username and passwords
  * Files -- username and tokens
  * Certificates
  * External Auth providers -- LDAP
  * Service account
  
* What can they do (Authorization)
  * RBAC authorization
  * ABAC authorization
  * Node authorization
  * Webhook mode
  
### TLS Certificates
All communications among k8s components like etcd cluster, kube-apiserver, kube-controller-manager,
kube-scheduler, kubelet, and kube-proxy are secured via TLS encryption.

### Communications between applications within cluster
By default, all pods can access all other pods within the cluster. You can restrict access between
them using network policies.

