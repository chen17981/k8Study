# Security

## 3b. TLS in k8s
Server certificates for servers
* kube-api server: apiserver.crt, apiserver.key
* etcd server: etcdserver.crt, etcdserver.key
* kubelet server: kubelet.crt, kubelet.key

Client certificates for clients
* admin.crt, admin.key
* scheduler.crt, scheduler.key
* controller.crt, controller.key
* kube-proxy.crt, kube-proxy.key

### Generate Certificates

```shell script
openssl genrsa -out ca.key 2048

openssl req -new -key ca.key -subj "/CN=KUBERNATES-CA" -out ca.csr

openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt
```

### View Certificates
```shell script
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
```

```shell script
kubectl logs etcd-master

docker logs <container-id>
```

### Manage Certificates
