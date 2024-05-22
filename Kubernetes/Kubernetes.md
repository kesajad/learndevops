# Kubernetes
## What is Kubernetes?
Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

![image](https://github.com/kesajad/learndevops/assets/99335234/a9ebf3fc-6052-4b02-a0b2-b23a05279d62)

### Traditional deployment era:
Early on, organizations ran applications on physical servers. There was no way to define resource boundaries for applications in a physical server, and this caused resource allocation issues. For example, if multiple applications run on a physical server, there can be instances where one application would take up most of the resources, and as a result, the other applications would underperform. A solution for this would be to run each application on a different physical server. But this did not scale as resources were underutilized, and it was expensive for organizations to maintain many physical servers.

### Virtualized deployment era:
As a solution, virtualization was introduced. It allows you to run multiple Virtual Machines (VMs) on a single physical server's CPU. Virtualization allows applications to be isolated between VMs and provides a level of security as the information of one application cannot be freely accessed by another application.
Virtualization allows better utilization of resources in a physical server and allows better scalability because an application can be added or updated easily, reduces hardware costs, and much more. With virtualization you can present a set of physical resources as a cluster of disposable virtual machines.
Each VM is a full machine running all the components, including its own operating system, on top of the virtualized hardware.

### Container deployment era:
Containers are similar to VMs, but they have relaxed isolation properties to share the Operating System (OS) among the applications. Therefore, containers are considered lightweight. Similar to a VM, a container has its own filesystem, share of CPU, memory, process space, and more. As they are decoupled from the underlying infrastructure, they are portable across clouds and OS distributions.
Containers have become popular because they provide extra benefits, such as:
- Agile application creation and deployment: increased ease and efficiency of container image creation compared to VM image use.
- Continuous development, integration, and deployment: provides for reliable and frequent container image build and deployment with quick and efficient rollbacks (due to image immutability).
- Dev and Ops separation of concerns: create application container images at build/release time rather than deployment time, thereby decoupling applications from infrastructure.
- Observability: not only surfaces OS-level information and metrics, but also application health and other signals.
- Environmental consistency across development, testing, and production: runs the same on a laptop as it does in the cloud.
- Cloud and OS distribution portability: runs on Ubuntu, RHEL, CoreOS, on-premises, on major public clouds, and anywhere else.
- Application-centric management: raises the level of abstraction from running an OS on virtual hardware to running an application on an OS using logical resources.
- Loosely coupled, distributed, elastic, liberated micro-services: applications are broken into smaller, independent pieces and can be deployed and managed dynamically – not a monolithic stack running on one big single-purpose machine.
- Resource isolation: predictable application performance.
- Resource utilization: high efficiency and density.

### Why you need Kubernetes and what it can do
Containers are a good way to bundle and run your applications. In a production environment, you need to manage the containers that run the applications and ensure that there is no downtime. For example, if a container goes down, another container needs to start. Wouldn't it be easier if this behavior was handled by a system?
That's how Kubernetes comes to the rescue! Kubernetes provides you with a framework to run distributed systems resiliently. It takes care of scaling and failover for your application, provides deployment patterns, and more. For example: Kubernetes can easily manage a canary deployment for your system.
Kubernetes provides you with:
- Service discovery and load balancing Kubernetes can expose a container using the DNS name or using their own IP address. If traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic so that the deployment is stable.
- Storage orchestration Kubernetes allows you to automatically mount a storage system of your choice, such as local storages, public cloud providers, and more.
- Automated rollouts and rollbacks You can describe the desired state for your deployed containers using Kubernetes, and it can change the actual state to the desired state at a controlled rate. For example, you can automate Kubernetes to create new containers for your deployment, remove existing containers and adopt all their resources to the new container.
- Automatic bin packing You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.
- Self-healing Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.
- Secret and configuration management Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys. You can deploy and update secrets and application configuration without rebuilding your container images, and without exposing secrets in your stack configuration.
- Batch execution In addition to services, Kubernetes can manage your batch and CI workloads, replacing containers that fail, if desired.
- Horizontal scaling Scale your application up and down with a simple command, with a UI, or automatically based on CPU usage.
- IPv4/IPv6 dual-stack Allocation of IPv4 and IPv6 addresses to Pods and Services
- Designed for extensibility Add features to your Kubernetes cluster without changing upstream source code.

### What Kubernetes is not
Kubernetes is not a traditional, all-inclusive PaaS (Platform as a Service) system. Since Kubernetes operates at the container level rather than at the hardware level, it provides some generally applicable features common to PaaS offerings, such as deployment, scaling, load balancing, and lets users integrate their logging, monitoring, and alerting solutions. However, Kubernetes is not monolithic, and these default solutions are optional and pluggable. Kubernetes provides the building blocks for building developer platforms, but preserves user choice and flexibility where it is important.
Kubernetes:
- Does not limit the types of applications supported. Kubernetes aims to support an extremely diverse variety of workloads, including stateless, stateful, and data-processing workloads. If an application can run in a container, it should run great on Kubernetes.
- Does not deploy source code and does not build your application. Continuous Integration, Delivery, and Deployment (CI/CD) workflows are determined by organization cultures and preferences as well as technical requirements.
- Does not provide application-level services, such as middleware (for example, message buses), data-processing frameworks (for example, Spark), databases (for example, MySQL), caches, nor cluster storage systems (for example, Ceph) as built-in services. Such components can run on Kubernetes, and/or can be accessed by applications running on Kubernetes through portable mechanisms, such as the Open Service Broker.
- Does not dictate logging, monitoring, or alerting solutions. It provides some integrations as proof of concept, and mechanisms to collect and export metrics.
- Does not provide nor mandate a configuration language/system (for example, Jsonnet). It provides a declarative API that may be targeted by arbitrary forms of declarative specifications.
- Does not provide nor adopt any comprehensive machine configuration, maintenance, management, or self-healing systems.
- Additionally, Kubernetes is not a mere orchestration system. In fact, it eliminates the need for orchestration. The technical definition of orchestration is execution of a defined workflow: first do A, then B, then C. In contrast, Kubernetes comprises a set of independent, composable control processes that continuously drive the current state towards the provided desired state. It shouldn't matter how you get from A to C. Centralized control is also not required. This results in a system that is easier to use and more powerful, robust, resilient, and extensible.

# Azure Kubernetes Service (AKS)
## Azure Kubernetes Service (AKS) 
It is a managed Kubernetes service that you can use to deploy and manage containerized applications. You need minimal container orchestration expertise to use AKS. AKS reduces the complexity and operational overhead of managing Kubernetes by offloading much of that responsibility to Azure.
AKS is an ideal platform for deploying and managing containerized applications that require high availability, scalability, and portability, and for deploying applications to multiple regions, using open-source tools, and integrating with existing DevOps tools.

![image](https://github.com/kesajad/learndevops/assets/99335234/124d4580-5fa6-4e43-a0d7-10a1d66d743f)

# The Evolution of Software Architecture:
Before diving into microservices, let's take a step back and understand how software architectures have evolved. In the past, monolithic architectures ruled the roost. These massive, all-in-one applications housed the entire functionality of an application in a single codebase. While they served their purpose, they came with their fair share of challenges.

### What is Monolithic Architecture?
A monolithic application, sometimes known as a "monolith," is comprised of a single enormous codebase that houses all of the program's components, including the backend, frontend, and configuration. Monoliths are commonly regarded as an older and more traditional technique of creating applications, however, many firms must still begin utilizing monolithic architecture. Monolithic programs are faster to design and deploy compared to microservices-based systems and may be easier to manage. 
![image](https://github.com/kesajad/learndevops/assets/99335234/03b71111-d8dc-4434-af5d-111a468bb08b)

### Pros of Monolithic Applications
- Easier to create and deploy: Because all components of a monolith are centralized, they may be relatively simple to build and deploy, resulting in a shorter time to market. The monolith architecture allows single developers or small teams to easily build, test, and launch programmes.
- Easier to test: Monolithic systems are easier to test than microservices-based programmes since they have a single code source to manage during testing and debugging.
- Fewer skills required: While most development teams nowadays are capable of designing a monolithic programme, developing a microservices-based application necessitates certain talents and training.
- Singular security management: While dividing an application into discrete microservices has some security benefits, using a monolith guarantees security is maintained in one spot.

### Cons of Monolithic Applications
- Complex maintenance: As a program expands and adds functionality, a monolithic codebase may become massive and complex. This makes the program harder to maintain, especially when the number of people working on the same codebase grows.
- Difficulty in implementing changes: Changes to one component of the program may inadvertently influence other portions of the codebase, necessitating more effort to discover problems.
- Difficult to scale: Scaling monolithic programs is challenging because new processing resources must be added all at once, a technique known as vertical scaling. This may be costly, and there are always constraints to how far an application may extend vertically.
- Technology constraints: Because of a monolith's interwoven dependencies, adding or upgrading functionality may be time-consuming. Depending on the program's needs, developers may be constrained in their ability to introduce extra functionality with a monolithic application.
- Single point of failure: Single point of failure: Because all program components are tightly linked, a fault anywhere in the code can bring the entire application down.

## What is Microservices Architecture?
Microservices design breaks down system components into distinct pieces that may be created, implemented, and scaled independently. Microservices, also known as microservices architecture, is a design method that builds an application as a collection of small, independent services based on a business domain. In a microservice architecture, each service is self-contained and provides a single business feature. Microservices have become the preferred method for designing applications in today's market.

![image](https://github.com/kesajad/learndevops/assets/99335234/3d097fbb-8e53-484c-aa58-cf9ea04d14f6)

## Pros of Microservices Applications:
- Microservices are self-contained: Because microservices are self-contained, they can be debugged, deployed, and managed independently of other modules. As an application grows, this might be advantageous since modifications to one component do not affect the others. Each microservice may be managed by a team focused on that capability.
- Simple to scale: An application may be horizontally scaled using microservices, which implies that each microservice can grow independently as needed. Horizontal scaling costs less than vertical scaling and allows an application to grow indefinitely.
- More adaptability: A microservices-based architecture enables teams to add new functionality and technologies as needed. The number of microservices needed to develop a system increases in proportion to its requirements.

## Cons of Microservices Applications:
- Complication: The individual modules may be simple, but a whole microservices-based system might be rather complex. The way microservices are coupled together provides a level of complexity not seen in monolithic programs.
- Specialised skills are required: Developing a microservices architecture demands specialized skills, which not all developers have. Developing microservices without proper training might lead to delays in delivery and increased costs for hiring external expertise.
- Security and testing will be distributed: Each module will include its own set of security vulnerabilities and concerns. While this helps to avoid assaults, it also means that there are more potential vulnerabilities to monitor, and debugging each part may be time-consuming.
- Extra expenses: While microservices may save money in certain cases, they will most likely necessitate more development resources to handle each microservice and its dependencies. While microservices may save money in certain cases, they will most likely necessitate more development resources to handle each microservice and its dependencies.

## Monolithic Vs Microservices Architecture:
Monolithic architecture is built as a single huge system with a common code base. As the application grows, it becomes increasingly intertwined, making it hard to separate services for scalability and maintenance. Because everything is so tightly linked and dependent on one another, changing technology, language, or structure is incredibly difficult. 

Microservices architecture is made up of tiny, self-contained modules based on business functions. A microservices application's projects and services are code independent of one another. As a result, it is simple to set up, deploy, and expand according to demand.

![image](https://github.com/kesajad/learndevops/assets/99335234/255e5c6c-e3cd-4b18-bcaa-9d00350a8120)

### Are Microservices Right for Your Business?
Whether microservices are the appropriate solution for your company relies on a number of criteria, including:
- Your organization's size
- Goals
- Technical expertise
Smaller companies may find it simpler to use microservices right once, but bigger enterprises may need to shift from monolithic systems over time.

### Challenges of Microservices:
While microservices offer many advantages, they also present unique challenges:
1.	Complexity: Managing a distributed system of microservices may be difficult, necessitating powerful tools for monitoring, logging, and deployment.
2.	Data Management: Managing data consistency and transactions across many services can be challenging.
3.	Service Coordination: Coordinating communication between services and preserving API contracts is critical, but it may be difficult.
4.	Testing: Comprehensive testing procedures must be implemented to guarantee that the whole system performs properly.

### Benefits of Microservices Architecture:
1.	Scalability: Microservices enable you to grow individual services according to demand. This results in more effective resource utilisation and cost savings.
2.	Faster Development: Smaller, focused teams can work on individual services, accelerating development cycles. This agility is crucial in today's fast-paced tech world.
3.	Resilience: If one service fails, it doesn't bring down the entire application. Other services can continue functioning, enhancing overall system resilience.
4.	Technology Flexibility: You're not locked into a single technology stack. Each service can use the best-suited technology, which promotes innovation and adaptability.
5.	Improved Maintenance: Smaller codebases are easier to maintain and update, reducing the risk of introducing bugs.

### Best Practices for Microservices:
1.	Service Isolation: Keep services independent, with well-defined APIs and minimal shared state.
2.	Containerization: Use container technologies like Docker for easy deployment and scaling.
3.	Automated Testing: Implement automated testing, including unit, integration, and end-to-end tests, to ensure reliability.
4.	Service Discovery: Use service discovery tools to locate and connect to services dynamically.
5.	Centralized Logging and Monitoring: Implement robust logging and monitoring solutions to gain visibility into your microservices ecosystem.
6.	Security: Apply security best practices at both the service and API levels to protect against potential threats.
7.	Continuous Integration/Continuous Deployment (CI/CD): Embrace CI/CD pipelines to automate the deployment process and ensure rapid and safe releases.
