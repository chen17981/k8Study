# Networking

## 2. Service Networking
Service is not related to a node, it is a cluster level resource.

kube-proxy is related service.

Check the service cluster ip range
```shell script
ps aux | grep kube-api-server
```

Check iptables for services
```shell script
iptables -L -t net | grep db-service
```

Check when iptables creates a record for service.
```shell script
cat /var/log/kube-proxy.log
```

Check the range of IP addresses configured for PODs on this cluster.
```shell script
kubectl logs <weave-pod-name> weave -n kube-system
```

Check the IP range configured for service.
```shell script
cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep cluster-ip-range
```

Check the type of proxy configured by kube-proxy.
```shell script
kubectl logs kube-proxy-ft6n7 -n kube-system
```