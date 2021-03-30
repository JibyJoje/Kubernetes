# Kubernetes
This repository contains information about basics of Kubernetes and the resources definition files of the most common Kubernetes resources.

## Containers
1. Containers are completely isolated environments that can have their own processes, services, Network Interfaces and mounts just like VM's except that they share the same OS kernel
2. Containers are an executable unit of software in which application code is packaged, along with its libraries and dependencies, in common ways so that it can be run anywhere, whether it be on desktop, traditional IT, or the cloud.
3. To do this, containers take advantage of a form of operating system (OS) virtualization in which features of the OS (in the case of the Linux kernel, namely the namespaces and cgroups primitives) are leveraged to both isolate processes and control the amount of CPU, memory, and disk that those processes have access to.

Containerzation Explained --> [Click Here](https://youtu.be/0qotVMX-J5s)

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
    