# Storage

## 2. Container Storage Interfaces

The container runtime interface is a standard that defines how an orchestration solution like k8s
would communication with container runtime like Docker. 

In future, if any new container runtime is developed, they can simply follow the CRI standard.

Similarly, to support different networking solutions, the container networking interface was introduced.

There is also container storage interface.
