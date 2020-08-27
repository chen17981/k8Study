# Networking

## 3. DNS in K8s

FQDN for service: 

Hostname - Namespace - Type - Root 

web-svc.apps.svc.cluster.local

#### How k8s implements DNS.

Check the DNS server config
```shell script
cat /etc/resolv.conf
```

#### Practices

Check the configuration file for configuring coreDNS.
```shell script
kubectl -n kube-system describe deployments.apps coredns | grep -A2 Args | grep Corefile
```