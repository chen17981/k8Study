# Cluster Maintenance

## K8s Release
K8s control Plane
* kube-apiserver
* controller-manager
* kube-scheduler
* kubelet
* kube-proxy
* kubectl

External Components
* etcd cluster
* CoreDNS

## Cluster Upgrade Process
K8s only support the most recent three minor releases.

If K8s cluster is managed by ```kubeadm```, we can use the cmds below for the upgrade.
```shell script
kubeadm upgrade plan

kubeadm upgrade apply
```
Upgrade Steps:
* upgrade master nodes
```shell script
  kubectl drain master --ignore-daemonsets

  apt-get upgrade -y kubeadm=1.12.0-00
 
  kubeadm upgrade apply v1.12.0

  apt-get upgrade -y kubelet=1.12.0-00

  systemctl restart kubelet

  kubectl uncordon master
```

* upgrade work nodes
```shell script
  kubectl drain node-1      # from master
    
  apt-get upgrade -y kubeadm=1.12.0-00 # from the node
    
  apt-get upgrade -y kubelet=1.12.0-00 # from the node
    
  kubeadm upgrade node config --kubelet-version v1.12.0 # from the node

  systemctl restart kubelet

  kubectl uncordon node-1    # from master
```


