# Networking

## 1. Pod Networking

### Networking Model
* Every pod should haven an IP address.
* Every pod should be able to communicate with every other pod in the same ndoe.
* Every pod should be able to communicate with every other pod on other nodes without NAT.

### Container Network Interface
* Container runtime much create network namespaces.
* Identify network the container must attach to.
* Container runtime to invoke network plugin (bridge) when container is added.
* Container runtime to invoke network plugin (bridge) when container is deleted.
* JSON format of the network configuration.

Configuring CNI
```shell script
#kubelet.service
ExecStart=/user/local/bin/kubelet
 ...
 --network-plugin=cni \
 --cni-bin-dir=/opt/cni/bin \
 --cni-conf-dir=/etc/cni/net.d \
 ...
```
View kubelet options
```shell script
ps -aux | grep kubelet
```

CNI plugin and binary directory
```shell script
ls /opt/cni/bin
```

CNI config directory
```shell script
ls /etc/cni/net.d
```

### Weaveworks

Deploy ```weave-net``` networking solution.
```shell script
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
```

IPAM (IP Address Management)


### Practices
Check the number of weave pods
```shell script
kubectl get pods -n kube-system
```

Check the name of bridge created by weave
```shell script
ip link
```

Check pod IP range configured by weave
```shell script
ip addr show weave
```
