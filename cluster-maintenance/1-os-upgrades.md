# Cluster Maintenance

## Before node maintenance
We need to take node01 out for maintenance. Empty the node of all applications and mark it unschedulable.
```shell script
kubectl drain node01 --ignore-daemonsets

node/node01 cordoned
WARNING: ignoring DaemonSet-managed Pods: kube-system/kube-flannel-ds-amd64-fzdd7, kube-system/kube-keepalived-vip-brv68, kube-system/kube-proxy-v87xq
evicting pod default/red-59d898f784-spcr8
evicting pod default/blue-8455cd8cd7-f6vkr
evicting pod default/red-59d898f784-ml78t
pod/red-59d898f784-spcr8 evicted
pod/red-59d898f784-ml78t evicted
pod/blue-8455cd8cd7-f6vkr evicted
node/node01 evicted
```

## After node maintenance
The maintenance tasks have been completed. Configure the node to be schedulable again.
```shell script
kubectl uncordon node01
```

## Make a node unschedulable
Node03 has our critical applications. We do not want to schedule any more apps on node03. 
Mark node03 as unschedulable but do not remove any apps currently running on it . 
```shell script
kubectl cordon node03
```

