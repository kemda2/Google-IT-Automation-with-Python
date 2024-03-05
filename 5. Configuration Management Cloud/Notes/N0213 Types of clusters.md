# Types of clusters

## Kubernetes clusters
A Kubernetes cluster comprises multiple servers (which Kubernetes calls “nodes”) that work together as a group. These nodes are virtual or physical machines that form the underlying infrastructure of the Kubernetes cluster. 

Each node is capable of running containers and hosting workloads. Kubernetes clusters are designed for scalability and high availability. Nodes can be added or removed as needed as workloads vary, so applications can scale up or down seamlessly. 

Nodes are interconnected and communicate with each other through the Kubernetes control plane to ensure seamless coordination and collaboration. The control plane is the brain of the Kubernetes cluster. It consists of several components that manage and monitor the cluster's overall state, including:

* An API server
* A controller manager
* A scheduler
* An etcd: This is a reliable data storage that can be accessed by the cluster of machines. 

Every Kubernetes cluster has one control plane and at least one control plane node. However, multiple nodes can be tasked with running the control plane components, and these component nodes can be spread out across zones for redundancy. 

The standard unit for deployment to a Kubernetes cluster is a container. Containerized applications are software applications packaged along with their dependencies, libraries, and configurations into isolated containers. Containers can be easily duplicated, ensuring easy, consistent deployment across different environments. 

Kubernetes is a powerful orchestration platform designed to manage and scale containerised applications. Kubernetes automates the deployment, scaling, and management of containerised applications across the cluster's nodes. Kubernetes also manages resources across the cluster by optimally allocating CPU, memory, and storage based on application requirements. This ensures that resources are used efficiently, and it minimizes conflicts between applications. And Kubernetes also maintains the health of the cluster by employing features that automatically replace failed or unhealthy containers. 

To manage a Kubernetes cluster, users specify the desired state of their applications, and then the cluster handles the actual execution and maintenance of the applications to match that desired state. This is called a “declarative approach.” The declarative approach simplifies management and reduces the need for manual intervention once the initial parameters are set. 

## Different types of Kubernetes clusters

Selecting the right type of cluster ensures a well-aligned Kubernetes deployment that will meet your specific business needs and objectives. Here are some of the major cluster architectures:
## On-premises cluster
An on-premises Kubernetes cluster is deployed within an organization's own data center or on a private infrastructure. Deploying an on-premises cluster involves setting up the control plane and worker nodes on the organization's own hardware, and the organization is responsible for cluster maintenance. This provides complete control over the hardware, networking, and security. This is particularly suitable for situations with specific compliance or data governance requirements. 

On-premises clusters are one of the primary types of Kubernetes clusters.  Tools like Kubernetes kubeadm and Kubernetes Operations (kOps) are designed for deploying this type of cluster, and there are multiple custom configurations that can be used to create and manage on-premises clusters

## Public cloud managed cluster
Another primary type of Kubernetes cluster is a public cloud managed cluster. Public cloud providers offer managed Kubernetes services, handling the underlying infrastructure management so it is easier for users to deploy and manage Kubernetes clusters on the cloud. This is a useful option for teams that prefer to offload cluster management tasks, but who still require the scalability and flexibility of cloud-based deployments.  This type of cluster allows the organization to focus on deploying and managing applications without dealing with the complexities of cluster maintenance in the way you would with an on-premise cluster. When you run Kubernetes in the cloud, cluster maintenance is automatically handled by the cloud provider. You don't need to worry about it. 

Another advantage of public cloud managed clusters is that they can be spread over zones or even regions. Just by checking a box in your configurations, you can spread your clusters geographically in case a cloud data center goes down or there are network problems. Some examples of managed services by public cloud providers are Amazon Elastic Kubernetes Service (EKS) on AWS, Google Kubernetes Engine (GKE) on Google Cloud, and Azure Kubernetes Service (AKS) on Microsoft Azure. 
## Private cloud managed cluster
These clusters function similarly to public cloud managed clusters, but private cloud providers manage Kubernetes services for deploying clusters within a private cloud environment. This combines the ease and flexibility of managed services with control over the private infrastructure. 

Some examples of managed private cloud providers are Nutanix, OpenStack, and Hewlett Packard Enterprises (HPE). 
## Local development clusters
The third primary type of Kubernetes clusters are local development clusters. These are lightweight and easy-to-set-up Kubernetes environments which facilitate a fast development workflow for individual developers. These are most often set up as local development and testing clusters, and they’re primarily used for application development and testing on a developer's local machine. They are often employed during the development phase to enable rapid iteration and debugging of applications before deploying them to production clusters. 

Tools commonly used to create local development clusters include Minikube, Docker Desktop (with Kubernetes enabled), and Kubernetes kind (Kubernetes in Docker). Each of these tools allows developers to spin up a single-node Kubernetes cluster locally to develop and validate applications without the need for a full-scale production cluster.
## Hybrid cluster
A hybrid Kubernetes cluster coordinates on-premises and cloud environments, allowing workloads to run seamlessly across both locations. This type of cluster is suitable for scenarios in which some applications need to reside on-premises, for instance for security requirements, while others benefit from cloud scalability and services. 
## Edge cluster
An edge Kubernetes cluster is deployed at the edge of the network, closer to the locations of end-users or Internet of Things (IoT) devices. Edge clusters are designed to support low latency, particularly in regions or zones where power and network connectivity are scarce and expensive.
## High-performance computing (HPC) cluster
HPC Kubernetes clusters are tailored for running computationally intensive workloads, such as scientific simulations or large data processing tasks. These clusters optimize performance by leveraging specialized hardware and configurations. 
## Multi-cluster federation
Multi-cluster federation involves managing multiple Kubernetes clusters as a single logical cluster. This allows centralized management of workloads, which are deployed across clusters similarly to the way a single Kubernetes cluster distributes workloads to multiple nodes. Multi-cluster federation facilitates global-scale deployments like disaster recovery scenarios. 
## Key takeaways
Kubernetes clusters are nodes which are coordinated to act as singular, cohesive units to provide a flexible and reliable platform. Clusters offer high availability, efficient scaling, and robust security. Depending on the computational purpose and requirements, you can configure a cluster to suit any organization.
