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

```
Component	Description
kube-apiserver	The API server exposes the underlying Kubernetes APIs and provides the interaction for management tools, such as kubectl or the Kubernetes dashboard.
etcd	etcd is a highly available key-value store within Kubernetes that helps maintain the state of your Kubernetes cluster and configuration.
kube-scheduler	When you create or scale applications, the scheduler determines what nodes can run the workload and starts the identified nodes.
kube-controller-manager	The controller manager oversees a number of smaller controllers that perform actions such as replicating pods and handling node operations.
Keep in mind that you can't directly access the control plane. Kubernetes control plane and node upgrades are orchestrated through the Azure CLI or Azure portal. To troubleshoot possible issues, you can review the control plane logs using Azure Monitor.
```
Nodes
To run your applications and supporting services, you need a Kubernetes node.
Each AKS cluster has at least one node, an Azure virtual machine (VM) that runs the Kubernetes node components, and container runtime.
Nodes include the following core Kubernetes components:
Component	Description
kubelet	The Kubernetes agent that processes the orchestration requests from the control plane along with scheduling and running the requested containers.
kube-proxy	The proxy handles virtual networking on each node, routing network traffic and managing IP addressing for services and pods.
container runtime	The container runtime allows containerized applications to run and interact with other resources, such as the virtual network or storage. For more information, see Container runtime configuration.

![image](https://github.com/kesajad/learndevops/assets/99335234/591841f0-1b2b-4091-80e8-609438f007f9)

The Azure VM size for your nodes defines CPUs, memory, size, and the storage type available, such as high-performance SSD or regular HDD.
Plan the node size around whether your applications might require large amounts of CPU and memory or high-performance storage.
Scale out the number of nodes in your AKS cluster to meet demand.
In AKS, the VM image for your cluster's nodes is based on Ubuntu Linux, Azure Linux, or Windows Server 2022. 
When you create an AKS cluster or scale out the number of nodes, the Azure platform automatically creates and configures the requested number of VMs. 
Agent nodes are billed as standard VMs, so any VM size discounts, including Azure reservations, are automatically applied.
For managed disks, default disk size and performance are assigned according to the selected VM SKU and vCPU count. 
OS configuration
AKS supports Ubuntu 22.04 and Azure Linux 2.0 as the node operating system (OS) for clusters with Kubernetes 1.25 and higher.
Ubuntu 18.04 can also be specified at node pool creation for Kubernetes versions 1.24 and below.
AKS supports Windows Server 2022 as the default OS for Windows node pools in clusters with Kubernetes 1.25 and higher. 
Windows Server 2019 can also be specified at node pool creation for Kubernetes versions 1.32 and below. 
Windows Server 2019 is being retired after Kubernetes version 1.32 reaches end of life and isn't supported in future releases.
Container runtime configuration
A container runtime is software that executes containers and manages container images on a node. 
The runtime helps abstract away sys-calls or OS-specific functionality to run containers on Linux or Windows. 
For Linux node pools, containerd is used on Kubernetes version 1.19 and higher. 
For Windows Server 2019 and 2022 node pools, containerd is generally available and is the only runtime option on Kubernetes version 1.23 and higher


## Dockerfile commands/Instructions
1. FROM
Represents the base image(OS), which is the command that is executed first before any other commands.
```
Syntax: 
FROM <ImageName>
Example: The base image will be ubuntu:19.04 Operating System.
FROM ubuntu:19.04
```
2. COPY
The copy command is used to copy the file/folders to the image while building the image. 
```
Syntax:
COPY <Source> <Destination>
Example: Copying the .war file to the Tomcat webapps directory
COPY target/java-web-app.war  /usr/local/tomcat/webapps/java-web-app.war
```
3. ADD
While creating the image, we can download files from distant HTTP/HTTPS destinations using the ADD command.
```
Syntax:
ADD <URL>
Example: Try to download Jenkins using ADD command 
ADD https://get.jenkins.io/war/2.397/jenkins.war
```
4. RUN
Scripts and commands are run with the RUN instruction. The execution of RUN commands or instructions will take place while you create an image on top of the prior layers (Image).
```
Syntax: 
RUN < Command + ARGS>
Example: 
RUN touch file
```
5. CMD
The main purpose of the CMD command is to start the process inside the container and it can be overridden.
```
Syntax:
CMD [command + args]
Example: Starting Jenkins 
CMD ["java","-jar", "Jenkins.war"]
```
6. ENTRYPOINT
A container that will function as an executable is configured by ENTRYPOINT. When you start the Docker container, a command or script called ENTRYPOINT is executed. It can’t be overridden.The only difference between CMD and ENTRYPOINT is CMD can be overridden and ENTRYPOINT can’t.
```
Syntax:
ENTRYPOINT [command + args]
Example: Executing the echo command.
ENTRYPOINT ["echo","Welcome to GFG"]
```
7. MAINTAINER
By using the MAINTAINER command we can identify the author/owner of the Dockerfile and we can set our own author/owner for the image.
```
Syntax: 
MAINTAINER <NAME>
Example: Setting the author for the image as a KESaj.
MAINTAINER  KESaj 
```
## Create a Dockerfile
- Create a file named Dockerfile.
- Add instructions in Dockerfile.
- Build Dockerfile to create an image.
- Run the image to create a container.

## Example 1: Steps To Create Dockerfile With Example(Jenkins)
In this example, we will write the Dockerfile for Jenkins and build an image by using Dockerfile which has been written for Jenkins and we will run it as a container.
### Step 1: Create a directory and create a file with the name Dockerfile.
### Step 2: Open the Dockerfile by using the vim editor and start writing the command that is required to build the Jenkins image.
Dockerfile for Jenkins image
We used JDK as a base image because Jenkins’s pre-requisite is JDK after that we added a command called MAINTAINER which indicates the author or owner of the docker file and we added the ENV variable where we set the path for the Jenkins and by using RUN command we are creating the path and by using ADD we are downloading the Jenkins and starting the .war file with the help of CMD command.
```
FROM openjdk:11-jdk
MAINTAINER Guruschools
LABEL env=production
ENV apparea /data/app
RUN mkdir -p $apparea
ADD https://get.jenkins.io/war/2.397/jenkins.war $apparea
WORKDIR $apparea
EXPOSE 8080
CMD ["java","-jar","jenkins.war"]
```
### Step 3: Build the image by using the below command with the help of Dockerfile and give the necessary tags. and the dot(.) represents the current directory which is a path for Dockerfile.
docker build -t jenkins:1 .
### Step 4: Run the container with the help image ID or tag of the image by using the below command.
docker run -d -p 8080:8080 <Imagetag/ID>
### Step 5: Accesses the application (Jenkins) from the internet with the help of host port and hostIP (HostIP: Port)
![image](https://github.com/kesajad/learndevops/assets/99335234/1d2c8c06-3b9c-4996-95b4-998457291a4f)
