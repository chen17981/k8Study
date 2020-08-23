# Storage

## 1. Docker Storage

### Docker Storage Driver
* container layer: read and write
* image layers: read only

Volumes: there are two mounts:
* Volume mount

  In order to have a persistent volume, we can create a volume first.
    ```shell script
    docker volume create data_volume
    ```
    The above cmd will create a volume under ```/var/lib/docker/volumes/data_volume```, then
    to use it, we can 
    ```shell script
    docker run -v data_volume:/var/lib/mysql mysql
    ```
    The data_volume will be mounted at ```/var/lib/mysql``` inside the container.

* Bind mount
    
    If we want to mount a dir in the host machine, we can use the cmd
    ```shell script
    docker run -v <local-path>:<container-path> mysql
    ```

The preferred cmd is using ```mount option```
```shell script
docker run --mount type=bind,source=/data/mysql,target=/var/lib/mysql mysql
```
The docker uses storage drivers to manage the layered architecture.
* AUFS
* ZFS
* BTRFS
* Device Mapper
* Overlay
* Overlay2

It depends on the underlying OS to decide which storage driver is used.

### Volume Drivers

Storage drivers helps manage storage on images and containers. Volumes are not handled by storage drivers,
they are handled by volume driver plugins.





