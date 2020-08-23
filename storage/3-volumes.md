# Storage

## 3. Volumes

### Volume
```yaml
volumes:
- names: data-volume
  awsElasticBlockStore:
    volumeID: <volume-id>
    fsType: ext4
```

### Persistent Volumes
Persistent volumes are a system-wide storage volume pool.
```yaml
#pv-def.yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-vol1
spec:
  accessModes:
  - ReadWriteOnce
  capacity:
    storage: 1Gi
  awseElasticBlockStore:
    volumeId: <volume-id>
    fsType: ext4
```
```shell script
kubectl create -f pv-def.yaml
```

### Persistent Volume Claim
The k8s create persistent volumes, and user creates persistent volume claims to use persistent volume.

Every PVC is binding to a PV.

```yaml
#pvc-def.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata: 
  name: myclaim
spec:
  accessModes:
  - ReadWriteOnce
  Resources:
    requests:
      storage: 500Mi
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
    - name: myfrontend
      image: nginx
      volumeMounts:
      - mountPath: "/var/www/html"
        name: mypd
  volumes:
    - name: mypd
      persistentVolumeClaim:
        claimName: myclaim
```


