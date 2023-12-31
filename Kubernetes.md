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



# Namespaces

### Get all namespaces

> kubectl  get namespaces
### Get namespace information in yaml format

> kubectl  get namespaces -o yaml
### Describe the default namespace

> kubectl  describe  namespace default
### Create a new namespace

> kubectl  create namespace my-namespace
### Delete the namespace

> kubectl  delete namespace my-namespace


# Pods

### Get pods from the current namespace

> kubectl get pods
### Get pods from all the namespaces

> kubectl get pods --all-namespaces
### Get pods from the specified namespace

> kubectl get pods -namespace=my-namespace
### Create a pod

> kubectl  run my-pod-1 --image=nginx:latest --dry-run
### see how the pod would be processed

> kubectl  run my-pod-1 --image=nginx:latest --dry-run=client
### Create a pod in the specified namespace

> kubectl  run my-pod-2 --image=nginx:latest --namespace=my-namespace
### Create a pod with a label to it

> kubectl  run nginx --image=nginx -l --labels=app=test
### Get all pods with label output

> kubectl get pods --show-labels
### Get pods with exapanded/wide output

> kubectl  get pods -o wide
### List pods in a sorted order

> kubectl  get pods --sort-by=.metadata.name
### Get logs of the pod

> kubectl  logs  my-pod-1
### Get pods within the specified namespace with exapanded/wide output

> kubectl get pods my-pod-2 --namespace=my-namespace -o wide
### Get logs of the pod within the specified namespace

> kubectl  logs  my-pod-2 --namespace=my-namespace
### Describe the pod

> kubectl  describe  pod my-pod-1
### Describe the pod within the specified namespace

> kubectl describe  pods my-pod-1 --namespace=my-namespace
### Delete the pod from the current namespace

> kubectl  delete pod my-pod-1
### Delete the pod from the specified namespace

> kubectl delete  pods my-pod-1 --namespace=my-namespace