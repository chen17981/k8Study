# Security

## 4. Security kube-config
Using key and crt to query pod
```shell script
curl https://my-kube-playground:6443/api/v1/pods \
  --key admin.key   \
  --cert admin.crt  \
  --cacert ca.crt
```
Or using kubeconfg file.
```shell script
#config file $HOME/.kube/config
--server my-kube-playground:6443
--client-key admin.key
--client-certificate admin.crt
--certificate-authority ca.crt
```

```shell script
kubectl get pods --kubeconfig config
```

### KubeConfig File
There are three sections:
* Clusters
* Contexts
* Users

To view the current config file 
```shell script
kubectl config view
```
Change the current context
```shell script
kubectl config use-context prod-user@production
```

Encode/decode cert
```shell script
cat ca.crt | base64

echo "---" | base64 --decode
```