# WhiteBoard
![K8s](https://github.com/kesajad/learndevops/assets/99335234/2d6dd795-b15c-4650-8b95-e3553af39446)

# What is Kubernetes?
- Kubernetes is a rapidly evolving platform that manages container-based applications and their associated networking and storage components. 
- Kubernetes focuses on the application workloads and not the underlying infrastructure components. 
- Kubernetes provides a declarative approach to deployments, backed by a robust set of APIs for management operations.
- You can build and run modern, portable, microservices-based applications using Kubernetes to orchestrate and manage the availability of the application components.
- Kubernetes supports both stateless and stateful applications.
- As an open platform, Kubernetes allows you to build your applications with your preferred programming language, OS, libraries, or messaging bus. 
- Existing continuous integration and continuous delivery (CI/CD) tools can integrate with Kubernetes to schedule and deploy releases.
- AKS provides a managed Kubernetes service that reduces the complexity of deployment and core management tasks.
- The Azure platform manages the AKS control plane, and you only pay for the AKS nodes that run your applications.
## Kubernetes cluster architecture
A Kubernetes cluster is divided into two components:
- The control plane, which provides the core Kubernetes services and orchestration of application workloads, and
- Nodes, which run your application workloads.
  
 ![image](https://github.com/kesajad/learndevops/assets/99335234/e97e7615-95a7-4471-acd9-2f7fdd2e3b51)

## Control plane
- When you create an AKS cluster, the Azure platform automatically creates and configures its associated control plane. 
- This single-tenant control plane is provided at no cost as a managed Azure resource abstracted from the user. 
- You only pay for the nodes attached to the AKS cluster. The control plane and its resources reside only in the region where you created the cluster.

The control plane includes the following core Kubernetes components:

>### kube-apiserver
The API server exposes the underlying Kubernetes APIs and provides the interaction for management tools, such as kubectl or the Kubernetes dashboard.

>### etcd
etcd is a highly available key-value store within Kubernetes that helps maintain the state of your Kubernetes cluster and configuration.

>### kube-scheduler
When you create or scale applications, the scheduler determines what nodes can run the workload and starts the identified nodes.

>### kube-controller-manager
The controller manager oversees a number of smaller controllers that perform actions such as replicating pods and handling node operations.

Keep in mind that you can't directly access the control plane. Kubernetes control plane and node upgrades are orchestrated through the Azure CLI or Azure portal. To troubleshoot possible issues, you can review the control plane logs using Azure Monitor.

## Nodes
- To run your applications and supporting services, you need a Kubernetes node.
- Each AKS cluster has at least one node, an Azure virtual machine (VM) that runs the Kubernetes node components, and container runtime.
Nodes include the following core Kubernetes components:

>### kubelet
The Kubernetes agent that processes the orchestration requests from the control plane along with scheduling and running the requested containers.

>### kube-proxy
The proxy handles virtual networking on each node, routing network traffic and managing IP addressing for services and pods.

>### container runtime
The container runtime allows containerized applications to run and interact with other resources, such as the virtual network or storage. For more information, see Container runtime configuration.

![image](https://github.com/kesajad/learndevops/assets/99335234/591841f0-1b2b-4091-80e8-609438f007f9)

- The Azure VM size for your nodes defines CPUs, memory, size, and the storage type available, such as high-performance SSD or regular HDD.
- Plan the node size around whether your applications might require large amounts of CPU and memory or high-performance storage.
- Scale out the number of nodes in your AKS cluster to meet demand.
- In AKS, the VM image for your cluster's nodes is based on Ubuntu Linux, Azure Linux, or Windows Server 2022. 
- When you create an AKS cluster or scale out the number of nodes, the Azure platform automatically creates and configures the requested number of VMs. 
- Agent nodes are billed as standard VMs, so any VM size discounts, including Azure reservations, are automatically applied.
- For managed disks, default disk size and performance are assigned according to the selected VM SKU and vCPU count.

## OS configuration
- AKS supports Ubuntu 22.04 and Azure Linux 2.0 as the node operating system (OS) for clusters with Kubernetes 1.25 and higher.
- Ubuntu 18.04 can also be specified at node pool creation for Kubernetes versions 1.24 and below.
- AKS supports Windows Server 2022 as the default OS for Windows node pools in clusters with Kubernetes 1.25 and higher. 
- Windows Server 2019 can also be specified at node pool creation for Kubernetes versions 1.32 and below. 
- Windows Server 2019 is being retired after Kubernetes version 1.32 reaches end of life and isn't supported in future releases.

## Container runtime configuration
- A container runtime is software that executes containers and manages container images on a node. 
- The runtime helps abstract away sys-calls or OS-specific functionality to run containers on Linux or Windows. 
- For Linux node pools, containerd is used on Kubernetes version 1.19 and higher. 
- For Windows Server 2019 and 2022 node pools, containerd is generally available and is the only runtime option on Kubernetes version 1.23 and higher
