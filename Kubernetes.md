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


# Deployments

### Get a list of deployments from the current namespace

> kubectl  get deployments
### Get a list of deployments from the specified namespace

> kubectl  get deployments --namespace=my-namespace
### Create a deployment

> kubectl  create deployment my-deployment-1 --image=nginx
### Get the specified deployment

> kubectl  get deployment my-deployment-1
### Get the specified deployment with its labels

> kubectl  get deployment my-deployment-1 --show-labels
### Describe the specified deployment

> kubectl describe  deployments my-deployment-1
### Get details of the deployment in yaml format

> kubectl  get deployment my-deployment-1 -o yaml
### Change image in the existing deployment

> kubectl  set image deployment my-deployment-1 nginx=nginx:1.16.1
### View rollout history

> kubectl rollout history deployment my-deployment-1
### Undo a previous rollout

> kubectl rollout undo deployment my-deployment-1
### Go back the specific version of the rollout history

> kubectl rollout undo deployment my-deployment-1 --to-revision=2
### Show the status of the rollout

> kubectl rollout status deployment my-deployment-1
### Restart a resource

> kubectl rollout restart deployment my-deployment-1
### Scale deployment to 3

> kubectl scale --replicas=3 deployment my-deployment-1
### Scale from current count to the desired

> kubectl scale --current-replicas=3 --replicas=5 deployment my-deployment-1
This will create an HPA (Horizontal Pod Aotuscaler)

> kubectl autoscale deployment my-deployment-1 --min=2 --max=10


# Services

First, create a pod with the label app=myapp.

Then:

### Create a pod with a label

> kubectl run my-pod --image=nginx --labels=app=myapp
### Create a service of type NodePort which will use pod's labels for selector but we have to specify the type, so create a definition file first and then create a service

> kubectl expose pod my-pod --port=80 --name nginx-service --type=NodePort --dry-run=client -o yaml
### Create a Service which will have type type NodePort but this will not have selector as my-app

> kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml
### Get services from the current context

> kubectl  get service
### Get details of the services

> kubectl  get service -o wide
### Get services with labels on them

> kubectl  get service --show-labels
### Get services from all the namespaces

> kubectl  get services --all-namespaces
### Describe the service to know more about it

> kubectl  describe  service nginx-service
### Get a particular service

> kubectl  get  service nginx-service
### Delete the service

> kubectl  delete service nginx-service


# Manage Objects from .yaml/.yml files

First, create a definition file for a pod

### Create a definition file for pod

> kubectl  run mypod --image=nginx --dry-run=client -o yaml > my-pod.yml
### Create an object

> kubectl  create -f my-pod.yml
### Delete the object

> kubectl  delete -f my-pod.yml