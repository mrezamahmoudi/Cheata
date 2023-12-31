# Cluster Information

### Print the client and server version information

kubectl version


### Print the supported API resources on the server

kubectl api-resources
### Print the supported API versions on the server, in the form of "group/version"

kubectl api-versions
### Print the cluster information

kubectl cluster-info
### Get the list of the nodes in the cluster

kubectl  get nodes
### Get information of the master node

kubectl  get nodes master -o wide
### Get detailed information on the master nodes

kubectl  describe  nodes  master