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

ReclaimPolicy
* Retain: after pvc is deleted, the pv is not deleted, but not avaiable for re-use by other pod.
* Delete: once pvc is deleted, the pv is also deleted as soon as possible.
* Recycle: the data on the pv will be deleted, and make the pv available for use.


### Practices

```yaml
master $ cat webapp-pod-hostpath.yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp
spec:
  containers:
  - name: event-simulator
    image: kodekloud/event-simulator
    env:
    - name: LOG_HANDLERS
      value: file
    volumeMounts:
    - mountPath: /log
      name: log-volume

  volumes:
  - name: log-volume
    hostPath:
      # directory location on host
      path: /var/log/webapp
      # this field is optional
      type: Directorymaster $
```

Create a PV
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-log
spec:
  accessModes:
    - ReadWriteMany
  capacity:
    storage: 100Mi
  hostPath:
    path: /pv/logmaster $
```

Create a PVC
```yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: claim-log-1
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 50Mi
```

Create a pod using the PVC
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp
spec:
  containers:
  - name: event-simulator
    image: kodekloud/event-simulator
    env:
    - name: LOG_HANDLERS
      value: file
    volumeMounts:
    - mountPath: /log
      name: log-volume

  volumes:
  - name: log-volume
    persistentVolumeClaim:
      claimName: claim-log-1
```


