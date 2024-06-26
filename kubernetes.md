# Kubernetes

Powerful container orchestration system for managing enterprise level containerized applications

# Short and sweet architecture

- You run <code>kubectl run [OPTIONS]</code>
- The k8s control plane gets the API request and instructs a cluster node to create a pod with the given name
- The <code>kubelet agent</code> running on the node then instructs the container runtime (Docker/containerd etc) to create a container in the pod
- The runtime spins up the container from the image passed into <code>kubectl run [OPTIONS]</code>

# Setup

<code>kubectl version</code> - displays the version and acts as a test to the API</br>
<code>kubectl api-resources</code> - displays the API resources available, inc. API version and kind</br>
<code>kubectl api-versions</code> - displays the API versions available</br>

# Designing YAML files

- Kubernetes is best used declaratively
- The .yaml file options are many in k8s!
- Use the following commands to help find keys and values to produce .yaml configurations

<code>kubectl api-resources</code> - see above in 'Setup'</br>
<code>kubectl api-versions</code> - see above in 'Setup'</br>
<code>kubectl explain [resource] --recursive</code> - display all possible keys for [resource] and the key type</br>
<code>kubectl explain [resource].[key]</code> - display all possible values for [key] under [resource] (e.g. services.spec)</br>
<code>kubectl explain [resource].[key].[sub_key]</code> - same as above drilled further to show possible values of [sub_key]</br>

# Viewing resources

### Get

<code>kubectl get [name]</code> - show the resource called [name]</br>
<code>kubectl get [name] -o [output]</code> - show the resource called [name] in [output] format</br>
<code>kubectl get pods</code> - show all pods</br>
<code>kubectl get nodes</code> - show all nodes</br>
<code>kubectl get node [name]</code> - show node called [name]</br>
<code>kubectl get service</code> - show all services</br>
<code>kubectl get namespaces</code> - show all namespaces</br>
<code>kubectl get all</code> - show all resources in the current namespace</br>

### Describe

<code>kubectl describe [name]</code> - show detailed status of the resource [name]</br>

### Event

<code>kubectl event [name]</code> - show detailed event log of the resource [name]</br>
<code>kubectl get events --watch-only</code> - show live log stream of the current state only</br>

### Log

<code>kubectl logs deploy/[name]</code> - show logs of the first pod in a deployment called [name]</br>
<code>kubectl logs deploy/[name] --follow --tail 1</code> - show the last log entry of the first pod in a deployment called [name]</br>
<code>kubectl logs pod/[name] -c [container]</code> - show specific [container] logs in pod called [name]</br>
<code>kubectl logs pod/[name] --all-containers=true</code> - show logs for all containers</br>
<code>kubectl logs pod/[name] -l [key=value]</code> - show logs for containers with the label [key=value]</br>

### Watch

<code>kubectl get [resource] -w</code> - show all resources of type [resource] and watch for changes (sends changes to stdout)</br>

# Pods

### Run a pod

<code>kubectl run [name] --image [image]</code> - runs a container in a pod called [name] from [image]</br>
<code>kubectl run [name] --rm -it --image [image] -- [command]</code> - run [command] on an interactive container that's deleted on kill</br>
<code>kubectl run [OPTIONS] --dry-run=client -o yaml</code> - see what would happen if you ran the command</br>

### Delete a pod

<code>kubectl delete pod [name]</code> - delete a pod called [name]</br>

# Jobs

<code>kubectl create job [name] --image [image]</code> - bath process to run a single pob and then delete it</br>

# Deployments

### Create a deployment

<code>kubectl create deployment [name] --image [image]</code> - creates a deployment called [name] using [image]</br>

### Scale a deployment

<code>kubectl scale deployment [name] --replicas [num]</code> - scales a deployment called [name] to [num] replicas</br>

### Delete a deployment

<code>kubectl delete deployment [name]</code> - delete a deployment called [name]</br>

# Services

### Types

<code>ClusterIP (default)</code> - Exposes the Service on a cluster-internal IP (only reachable from within the cluster). You can expose the Service to the public internet using an Ingress or a Gateway.</br>
<code>NodePort</code> - Exposes the Service on each Node's IP at a static port (the NodePort). To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of type: ClusterIP.</br>
<code>LoadBalancer</code> - Exposes the Service externally using an external load balancer. Kubernetes does not directly offer a load balancing component (you must provide one), or you can integrate your Kubernetes cluster with a cloud provider.</br>
<code>ExternalName</code> - Maps the Service to the contents of the externalName field (for example, to the hostname api.foo.bar.example). The mapping configures your cluster's DNS server to return a CNAME record with that external hostname value. No proxying of any kind is set up.</br>

### Exposing services

<code>kubectl expose deploy/[name] --port [port]</code> - expose a ClusterIP deployment called [name] on port [port]</br>
<code>kubectl expose [OPTIONS] --type NodePort</code> - expose a NodePort deployment</br>
<code>kubectl expose [OPTIONS] --type LoadBalancer</code> - expose a LoadBalancer deployment</br>

# Apply

<code>kubectl apply -f [file].yaml</code> - deploys a k8s environment from [file].yaml</br>
<code>kubectl apply -f [directory]/</code> - deploys a k8s environment from a [directory] containing config files</br>
<code>kubectl apply -f [URL]/[file].yaml</code> - deploys a k8s environment by pulling [file].yaml from a remote [URL]</br>

#### WARNING

- Be carful with <code>kubectl apply -f [URL]/[file].yaml</code>
- This will run a file you just pulled from the internet on your system **!!**
- Use <code>curl -L [URL]/[file].yaml</code> to view the file before you decide to run it

# Diff

<code>kubectl diff -f [URL]/[file].yaml</code> - shows the difference between the running spec and the spec in [URL]/[file].yaml</br>

# Labels

- Listed under <code>metadata</code> in a .yaml specification file
- Key/value pair that describes the resource
  - e.g. <code>app=nginx</code>
- Can be used to identify, group, and filter resources

<code>kubectl get [resource] -l [key]=[value]</code> - show any [resource] labelled with [key]=[value]</br>
<code>kubectl apply [file].yaml -l [key]=[value]</code> - only apply resources from [file].yaml labelled with [key]=[value]</br>

### Label Selectors

- Listed under <code>spec</code> in a .yaml specification file
- Linking mechanism to tell Deployments and Services which pods are under their control
- Can be used to
  - link dependencies to a resource
  - control which pods go to which nodes in a cluster
- In Service and Deployment YAML files the labels must match for deployment to work
  - <code>spec.selector.matchLabels.[key]=[value]</code> should match <code>spec.template.metadata.labels.[key]=[value]</code>

# Storage

- <code>Volumes</code> - Tied to the lifecycle of a pod. Shared by all containers in the pod</br>
- <code>PersistentVolumes</code> - Outlives the lifecycle pods. Shared multiple pods</br>
- <code>CSI plugins</code> - 3rd party vendor storage accessed by the CSI (Container Storage Interface) standard API

# Ingress

- Layer 7 traffic routing to containers running in K8s pods (not included by default)
- Basically a Web proxy that routes traffic to the correct container
- Popular proxies that <code>Ingress Controllers</code> can forward traffic for include
  - Nginx, Traefik, HAProxy, F5, Envoy, Istio etc

# Operator pattern

- 3rd party resources and controllers for extending the K8s API and CLI
- Woks well with databases, monitoring tools, backups, and custom ingress
- [Operator pattern](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/)
