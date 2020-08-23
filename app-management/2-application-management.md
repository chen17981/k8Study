# Application Management

## 2. Application Configuration

### Configuring command and arguments on applications
Setting the entry point for docker
```shell script
docker run --name ubuntu-sleeper --entrypoint sleep2.0 ubuntu-sleeper 10
```

### Configuring environment variables
Setting environment variables via docker
```shell script
docker run -e APP_COLOR=pink simple-webapp
```

* configMap
  * create a config map
  ```shell script 
  kubectl create configmap <config-name> --from-literal=<key>=<value>
  
  kbuectl create configmap <config-name> --from-file=<path-to-file>
  ```
  Or, using a config yaml file.
  ```yaml
  --- config.yml
  apiVersion: v1
  kind: ConfigMap
  metadata:
    name: my-config
  data:
    APP_COLOR: blue
    APP_MODE: prod
  ```
  ```shell script
  kubectl create -f config.yml
  ```
  
  * use the config map
  ```yaml
  containers:
  - envFrom:
    - configMapRef:
        name: my-config
  ```

* secretKey
  * create a secrete
  
  * inject a secrete to a pod

### Configuring secretes


## Useful links

* 