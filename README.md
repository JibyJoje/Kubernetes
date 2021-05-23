# Kubernetes
This repository contains information about basics of Kubernetes and the resources definition files of the most common Kubernetes resources.

## Containers
1. Containers are completely isolated environments that can have their own processes, services, Network Interfaces and mounts just like VM's except that they share the same OS kernel
2. Containers are an executable unit of software in which application code is packaged, along with its libraries and dependencies, in common ways so that it can be run anywhere, whether it be on desktop, traditional IT, or the cloud.
3. To do this, containers take advantage of a form of operating system (OS) virtualization in which features of the OS (in the case of the Linux kernel, namely the namespaces and cgroups primitives) are leveraged to both isolate processes and control the amount of CPU, memory, and disk that those processes have access to.

> Containerzation Explained &rightarrow; [Click Here](https://youtu.be/0qotVMX-J5s)

## Containers vs Virtual Machines
1. The major drawback of Virtual machines is that the Guest OS bloats up the VM requiring extra resources.
2. There is no concept of Guest on Containers as all the containers share the same OS kernel
3. Vm's are larger in size in GB. Whereas the Containers are in MB.
4. VM's take a lot of time to load up due to their Guest OS. Containers boot up instantaneously.
5. The resource utilization of VM's is higher than compared to Containers.

![VM vs Container](https://images.contentstack.io/v3/assets/blt300387d93dabf50e/bltb6200bc085503718/5e1f209a63d1b6503160c6d5/containers-vs-virtual-machines.jpg)

## Containers vs Images
1. **Containers** are running instances of the Container Images
2. **Images** are a complete package/template of the application that you wish to containerize. 
3. Images are immutable (unchangeable) whereas Containers are mutable

## Container Orchestration
1. The process of automatically deploying and managing containers in the environments is called as **Container Orchestration** 
2. Container Orchestration provides **High Availability** as there are multiple instances of our application running on different nodes.
3. The application becomes **Highly Scalable** as and when the traffic on the application increases/decreases.
4. It can help you to deploy the same application across different environments without needing to redesign it
5. Container orchestration can be used to automate and manage tasks such as:

    - Provisioning and deployment
    - Configuration and scheduling 
    - Resource allocation
    - Container availability 
    - Scaling or removing containers based on balancing workloads across your infrastructure
    - Load balancing and traffic routing 
    - Monitoring container health
    - Configuring applications based on the container in which they will run
    - Keeping interactions between containers secure

## Kubernetes Architecture
- **Node (minion)** - A machine (Physical or Virtual) on which kubernetes is installed. It is a worker machine where Kubernetes launches its containers.

- **Cluster** - A set of nodes grouped together (for fault tolerant and sharing load).

- **Master** - It's another node which has kubernetes installed on it and is configured as the master. The master watches over the nodes on the cluster and is responsible for the orchestration of the work on the nodes.

- **Installing Kubernetes installed the following components:**

	* API Server
 	* Etcd service
 	* Kubelet service
 	* Container Runtime
 	* Controller
 	* Scheduler

**API Server** - Acts as the front-end for the kubernetes service. Users, management devices, CLI all talk to the API server to communicate with the Kubernetes Cluster.

**Etcd service** - It is a distributed key-value store which stores information that is required by Kubernetes to manage the cluster.

**Scheduler** - It is responsible for distributing work on the containers across multiple nodes. It looks for new containers and assigns them to nodes.

**Controller** - It is the brain of the kubernetes technology which is responsible for noticing and responding when a node, container or an endpoint goes down. The controller makes decisions to bring up new containers in such cases.

**Container Runtime** - It is the underlying software that is used to run containers (e.g. Docker) 

**Kubelet** - The agent that runs on each node in the cluster. The kubelet is responsible for making sure that the containers are running on the nodes as expected.

## Master vs Node Architecture: 

![K8s Architecture](https://platform9.com/wp-content/uploads/2019/05/kubernetes-constructs-concepts-architecture.jpg)

- Kubernetes follows a Client-Server Architecture and it is possible to have a multi-master setup, but by default there is only a single master setup.
- The master node consists of the following Kubernetes components: 
	- kube-apiserver
	- etcd storage
	- kube-controller-manager
	- cloud-controller-manger (Cloud Architecture)
	- kube-scheduler
	- DNS server
- The worker nodes consists of the following Kubernetes components: 
	- kubelet
	- kube-proxy

> K8s Master-Worker Architecture &rightarrow; [Click Here](https://www.aquasec.com/cloud-native-academy/kubernetes-101/kubernetes-architecture/)

> K8s Architecture explained in Detail &rightarrow; [Click Here](https://platform9.com/blog/kubernetes-enterprise-chapter-2-kubernetes-architecture-concepts/)

### ETCD Service:

**What is ETCD?**
- It is a distributed reliable key-value store that is Simple, Secure and Fast.
- ETCD is fully replicated, which means all the nodes in the ETCD cluster has access to the full data store.
- ETCD is fully consistent, which means that all the data reads is going to return the most recent data write.
- ETCD is highly available, which means there is no single point of failure.

> ETCD Explained &rightarrow; [Click Here](https://www.youtube.com/watch?v=OmphHSaO1sE)

> ETCD Backup &rightarrow; [Click Here](https://www.youtube.com/watch?v=fnfLGOHNlWs)

### Kube-api Server: 

- The kube-api server validates and configures data for the apiobject
- When an end-user uses the `kubectl` tool, they are actually making an API request to the kube-api for the requested information.
- It is not mandatory to have the `kubectl` tool installed to communicate with the `api-server`. You can also communicate using `curl` request to the API server directly.
- The `kube-scheduler` monitors the API server if any object has been created

> kube api-server Explained &rightarrow; [Click Here](https://www.youtube.com/watch?v=EJGwWP_qFVw)

### kube-controller manager:

- A controller manager is a process that continuously monitors the state of various objects within the cluster and works towards bringing them to the desired state.
- Some of the different types of controllers that are availble are:
	- Node Controller
	- Replication Controller
	- Deployment Controller
	- Endpoint Controller
	- Namespace Controller
	- Job Controller
- All of the above mentioned controllers are binded together into a single pod within the cluster as the `kube-controller-manger` pod.

> The video for `kube-controller` is the same link as the one for `kube-scheduler` shared below.

### Kube-scheduler: 

- The `kube-scheduler` is responsible for scheduling the pods/nodes onto the cluster.
- The `scheduler` only decides which pod goes on which node. But, it is the duty of the `kubelet` to create the pod on the decided node.
- The pods are scheduled on the nodes based on different criterias such as the resource requirements and limits, taints and tolerations, Node selectors and Node Affinity.

> kube-controller and kube-scheduler explained --> [Click Here](https://www.youtube.com/watch?v=0YZdKdQUupA)

### Kubelet:

- The `kubelet` is responsible provisioning and deleting pods from the node as described by the scheduler.
- The kubelet constantly sends notifications to the `kube-api` about the current status of the pods and the health of the nodes.
- Only the `kubelet` cannot be installed as a pod on the cluster. It has to be manually installed on all the nodes using the kubernetes releases binary.

### Kube Proxy:

- Inside a K8s cluster, each pod can communicate with every other pod through the `Pod Network`
- The `Pod Network` is a virtual network which spans across all the nodes in the cluster to which all the pods connect to.
- The `kube-proxy` is responsible for looking out for new services, and every time a new service has been created it creates the appropriate rules to forward the traffic to these services and then to the backend pods.

### Namespaces:

- Namespaces are way to organize clusters into virtual sub-clusters. They can be helpful when different teams or projects share the same Kubernetes cluster.
- Namespaces cannot be nested within each other
- Kubernetes comes with three namespaces out of the box
	- `Default` - This is where all the k8s objects are created by default for every kubernetes command executed.
	- `kube-system` - This is used by the Kubernetes components and you should avoid creating any objects inside this namespace
	- `kube-public` -  Used by public resources and it is not recommended to to be used by the users
- Each namespace can be assigned a resource limit so that it can be guaranteed that the namespace doesn't use more than this limit specified.
- A service in one namespace can communicate with a service in another namespace simply by providing their namespace name `db-service.dev.svc.cluster.local`
	- `cluster.local` --> Domain
	- `svc` --> sub-domain
	- `dev` --> namespace
	- `db-service` --> service
- The `kubectl config set-context --current --namespace=dev` command can be used to set the current namespace to `dev` permanently.

```
kubectl get namespaces --> get the list of all namespaces in the cluster.
kubectl config set-context --curent --namespace=dev --> Set the current namespace to dev
kubectl get pods --all-namespaces --> get list of pods from all namespaces.
```

## Kubernetes Concepts:

### Pods:

 - A Pod is a single instance of an application. And it is also the smallest object that you can create in Kubernetes.
 - To scale up/down your application you add new pods (instances) to your worker nodes and not add new containers on an existing pod.
 - A pod can have multiple containers inside them, but usually they are not containers of the same kind (e.g. Node.js, nginx, redis)
 - Containers within the same pod share the same network and communicate with each other over `localhost` and the same volume.
 - Every object defintion YAML file in kubernetes will/must contain these 4 field:
 	- `apiVersion` --> depends on the `kind` of the object definition file.
 	- `kind` --> It is most commonly Pod, ReplicaSet, Service or Deployment
 	- `metadata` --> Contains data about the objects like name and labels
 	- `spec` --> This is where additional information pertaining to the object is defined.
 - 
 
 ```kubectl run <pod_name> --image <image_name> → deploys the instance of the image specified  
    kubectl get pods → gets the list of pods running in the current namespace  
    kubectl describe pod <pod_name> → gives a detailed description about the pods.
    kubectl apply -f <file_name> --> Creates the object in the cluster with the object defintion from the file
 ```

> Pod Overview &rightarrow; [Click Here](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)

### Replication Controller:

- The replication controller helps by running multiple instances of the application in a cluster, thus providing `High Availability`
- The replication controller makes sure that the specified number of pods are always running in the cluster.
- Another advantage of replication controllers is that it helps in `Load Balancing` and `Scaling`.
- The replication controller can span across multiple nodes in a cluster.
- `Replication Controller` and `Replica Set` both provide the same functionalities, but both are not the same
- If the entire node fails, the Replication Controller re-spawns all the pods of that node on some different node.
- The scope of the replication controller is decided by the `label-selector`
- Whichever pod matches this label will be managed by the replication controller.
- The difference between `Replication Controller` and `Replica Set` is that the `Replica Set` can manage pods that were not created as part of the `Replica Set` and this is managed by the `matchLabels` field under the `spec` section 

```kubectl create -f <file_name> --> Creates the replication controller/ replica set with the specifications from the object defintion file
kubectl get rc/replicationcontroller --> Gets the list of rc running in the current namespace
kubectl describe rc <rc_name> --> gives a detailed description about the rc.
kubectl scale rc <rc_name> --replicas=5 --> To scale up the replicas.
kubectl delete rc <rc_name> --> Delete the replication Controller
```
> Difference between Replication Controller and Replica Set --> [Click Here](https://blog.knoldus.com/replicationcontroller-and-replicaset-in-kubernetes/)

### Deployments:

- Deployments are the objects that have the highest hierarchy amongst all K8s objects.
- Creating a deployment creates a replicaset which creates a replicaset automatically based on the spec which in turn creates the pods with the number of replicas specified in the definition file.
- Deployment ensures that only a certain number of pods are down while they are updated. This is decided by the `maxUnavailable` field, which defaults to 25%
- Deployment also ensures that only a certain number of pods are created above the desired number of pods. This is decided by the `maxSurge` field, which defaults to 25%
- All of the deployment's rollout history is kept in the system so that you can rollback anytime you want.
- Everytime a deployment happens, it creates a rollout and the rollout creates a deployment revision.
- There are two deployment strategies that are available with Kubernetes and they are `recreate` and `rolling-update`
- The problem with the `recreate` deployment strategy is that when the depolyment upgrades to a newer revision the application becomes in-accessible because the entire pods are brought down at the same time.
- In the `rolling-update` strategy the pods are brought down and upgraded in a rolling fashion, thus there are still few pods pods that are serving the application. And this is the default strategy followed by Kubernetes.


![Deployments](https://miro.medium.com/max/700/0*gqmjVsavMoxbmgId.gif)

```kubectl apply -f <file_name> --> Creates the Deployment object with the specifications from the definition file.
kubectl get deployments --> Get the list of all deployments running in the current namespace
kubectl rollout status deployment <deploy_name> --> Shows the rollout status of the deployment
kubectl rollout history deployment <deploy_name> --> Shows the history of the revision of deployments
kubectl rollout history deployment <deploy_name> --revision=2 --> See the details of each revision
kubectl rollout undo deployment <deploy_name> --> rollback to the previous revision
kubectl rollout undo deployment <deploy_name> --to-revision=2 --> rollback to a specific revision
kubectl scale deployment <deploy_name> --replicas 10 --> Scaling a Deployment
kubectl delete deployment <deploy_name> --> Delete the deployment
kubectl describe deployment <deploy_name> --> gives a detailed description about the deployment
kubectl edit deployment <deploy_name> --> Edit/Update the specifications of the deployment
```

> Deployments in Kubernetes --> [Click Here](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

> Article from medium.com on Deployments --> [Click Here](https://medium.com/avmconsulting-blog/deployment-types-in-kubernetes-14b70ca7ef93)

> Checkout advanced K8s Deployment strategies --> [Click Here](https://semaphoreci.com/blog/kubernetes-deployment)

### Networking

- In kubernetes, all the pods inside a node are assigned a unique IP address. Unlike Docker where the IP address is assigned to the container
- When kubernetes is installed, a internal private network is automatically created and all the pods get the IP addressed from the subnet of this private network.
- All the pods are attached to this private network and the pods receive their IP's within this series.
- There are five essential things to understand about networking in Kubernetes
	- Communication between containers in the same pod
	- Communication between pods on the same node
	- Communication between pods on different nodes
	- Communication between pods and services
	- How does DNS work? How do we discover IP addresses?


> Networking in K8s --> [Click Here](https://www.stackrox.com/post/2020/01/kubernetes-networking-demystified/)

> Networking explained simple --> [Click Here](https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-networking-guide-beginners.html)

### Services:

- Services allow communication within the objects in the cluster and also outside the cluster.
- In simple terms, a Service enables network access to a set of pods.
- Services select the pods based on their labels and when a request is made to the service, it selects all pods in the cluster matching the service selector label.
- They allow us to connect one application service with other application service or Users.
- There are 3 different types of Services that are available:
	- `NodePort` --> Allows the services to be accessible by the outside world by forwarding the internal IP and exposing it.
	- `ClusterIP` --> Creates a virtual internal IP for the pods to communicate with each other
	- `LoadBalancer` --> provisions a load balancer within the cluster.
- **NodePort:** 
	- A `NodePort` port can only be within a valid range of 30000 - 32767
	- `targetPort` -  Port on the Application itself where the app is published.
	- `Port` - Port on the Service object which is attached to the ClusterIP
	- `NodePort` -  Port on which the app is exposed to the outside world
- **ClusterIP:**
	- ClusterIP will create one common IP for all the related pods which are grouped together by the Service selector label.
	- All the pods that need to communicate with these different services can communicate with the ClusterIP instead of individual IP of the pods as the IP of pods can change after they are restarted or deleted.
- **LoadBalancer:**
	- Provides a Load Balancing service for all the hosted applications on the cluster, out of the box.
	- The endpoints from the pods are automatically configured to point to the load balancer based on the service selector label.

![Services](https://matthewpalmer.net/kubernetes-app-developer/articles/service-route.gif)

```kubectl apply -f <file_name> --> Create the Service with the specs specified in the definition file
kubectl get svc --> get the list of services running in the current namespace.
kubectl describe svc <svc_name> --> gives a detailed description about the service.
kubectl delete svc <svc_name> --> Delete the service with the name specified
```

> Services Explained --> [Click Here](https://matthewpalmer.net/kubernetes-app-developer/articles/service-kubernetes-example-tutorial.html)

## Scheduling:

### Manual Scheduling:

- If there is no `scheduler` in the cluster to schedule the pods, then the pods will be in a `pending` status. In this case, we can go ahead and manually schedule the pods.
- We can manually schedule the pods on a node by using the `nodeName` field in the pod definition file under the `spec` section.

> NodeName Explained --> [Click Here](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodename)

### Labels and Selectors:

- Labels are key-value pairs that are attached to the k8s objects such and pods, etc.
- Each key must be unique for a given object
- Labels can be used for querying and watching the objects
- Labels support maximum `63 Characters`
- Selectors are used by objects in k8s to identify other objects that needs to be connected/monitored 

```kubectl get pods --selector env=dev
```
> Selectors and Labels Explained --> [Click Here](https://medium.com/@zwhitchcox/matchlabels-labels-and-selectors-explained-in-detail-for-beginners-d421bdd05362)

### Taints and Tolerations:

- Taints and Tolerations are available in K8s to decide what pods can be scheduled on a node.
- `Taints` are set on `nodes`.
- `Tolerations` are set on `pods`.
- Command to apply taint to a node
	- `kubectl taint nodes node-name key=value:taint-effect`
	- `taint-effect` decides what happens to the pods that do not tolerate this taint. And there are three taint-effects available
		- `NoSchedule` --> No new pods will be scheduled on this node
		- `PreferNoSchedule` --> The scheulder will try not to schedule pods on this node, but is not guaranteed.
		- `NoExecute` --> No new pods will scheduled on this node and all the existing pods on it will be evicted if it doesn't tolerate the taint.
- `Tolerations` need to be applied in the pod definition file under the `spec` section.
- Taints and Tolerations do no guarantee that a pod will be placed on the node, it only guarantees that it accepts the pods that has the toleration for it. (Pods that have toleration may very well be placed on other nodes that has no taints)
```
tolerations:
	- key: "app"
	  operator: "Equal"
	  value: "blue"
	  effect: "NoSchedule"
```


## Important K8s Commands:

	kubectl get pods &rightarrow; get the list of pods running in the current namespace
	kubectl cluster-info &rightarrow; get the details about the current cluster
	kubectl run nginx --image nginx &rightarrow; deploys a nginx application on the cluster by pulling the nginx image from docker hub
	kubectl describe pod <pod_name> &rightarrow; gives a detailed description about the pod


## Important K8s Articles:

- https://www.aquasec.com/cloud-native-academy/kubernetes-101/kubernetes-architecture/
- https://platform9.com/blog/kubernetes-enterprise-chapter-2-kubernetes-architecture-concepts/