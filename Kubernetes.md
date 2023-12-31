# Cluster Information

### Print the client and server version information

>kubectl version
### Print the supported API resources on the server

> kubectl api-resources
### Print the supported API versions on the server, in the form of "group/version"

> kubectl api-versions
### Print the cluster information

> kubectl cluster-info
### Get the list of the nodes in the cluster

> kubectl  get nodes
### Get information of the master node

> kubectl  get nodes master -o wide
### Get detailed information on the master nodes

> kubectl  describe  nodes  master

# Configuration Information

### Display merged kubeconfig settings

> kubectl  config view
### View the current context

> kubectl  config  current-context
### Set the context, here kubernetes-admin@kubernetes is the context name

> kubectl config  use-context kubernetes-admin@kubernetes
### Display clusters defined in the kubeconfig

> kubectl  config get-clusters
### Describe one or many contexts

> kubectl  config get-contexts