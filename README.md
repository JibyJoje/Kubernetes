# Kubernetes
This repository contains information about basics of Kubernetes and the resources definition files of the most common Kubernetes resources.

## Containers
1. Containers are completely isolated environments that can have their own processes, services, Network Interfaces and mounts just like VM's except that they share the same OS kernel
2. Containers are an executable unit of software in which application code is packaged, along with its libraries and dependencies, in common ways so that it can be run anywhere, whether it be on desktop, traditional IT, or the cloud.
3. To do this, containers take advantage of a form of operating system (OS) virtualization in which features of the OS (in the case of the Linux kernel, namely the namespaces and cgroups primitives) are leveraged to both isolate processes and control the amount of CPU, memory, and disk that those processes have access to.

> Containerzation Explained --> [Click Here](https://youtu.be/0qotVMX-J5s)

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

> K8s Master-Worker Architecture --> [Click Here](https://www.aquasec.com/cloud-native-academy/kubernetes-101/kubernetes-architecture/)

> K8s Architecture explained in Detail --> [Click Here](https://platform9.com/blog/kubernetes-enterprise-chapter-2-kubernetes-architecture-concepts/)

## Important K8s Commands:

	kubectl get pods --> get the list of pods running in the current namespace
	kubectl cluster-info --> get the details about the current cluster
	kubectl run nginx --image nginx --> deploys a nginx application on the cluster by pulling the nginx image from docker hub
	kubectl describe pod <pod_name> --> gives a detailed description about the pod
	

## Important K8s Articles:

https://www.aquasec.com/cloud-native-academy/kubernetes-101/kubernetes-architecture/
https://platform9.com/blog/kubernetes-enterprise-chapter-2-kubernetes-architecture-concepts/