# Cluster Maintenance

## Backup

* Backup K8s resources
```shell script
kubectl get all --all-namespaces -o yaml > all-deploy-svc.ymal
```

* Backup Etcd
```shell script
export ETCDCTL_API=3

etcdctl snapshot save snapshot.db

etcdctl snapshot status snapshot.db
```

## Restore
* Restore etcd cluster
```shell script
service kube-apiserver stop

etcdctl snapshot restore snapshot.db 

service etcd restart

service kube-apiserver start
```

Look at the ETCD Logs using command  or check the ETCD pod 
```shell script
kubectl logs etcd-master -n kube-system

kubectl describe pod etcd-master -n kube-system
```

## Useful links

* Backing up an etcd cluster 
https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#backing-up-an-etcd-cluster

* etcd recovery
https://github.com/etcd-io/etcd/blob/master/Documentation/op-guide/recovery.md

https://github.com/mmumshad/kubernetes-the-hard-way/blob/master/practice-questions-answers/cluster-maintenance/backup-etcd/etcd-backup-and-restore.md