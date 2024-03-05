# Kubernetes principles

Kubernetes is an open-sourced container orchestration platform that automates the deployment, scaling, and management of containerized applications. Kubernetes provides developers with a framework to easily run distributed systems. Kubernetes also provides developers choice and flexibility when building platforms.

In this reading, you will learn more about the principles and design philosophy behind Kubernetes, and you’ll learn how declarative configuration enables the desired state reconciliation model. In addition, you’ll learn about the key components of the control plane.



## Kubernetes principles

Kubernetes—a cloud-native application—follows principles to ensure the containerized application runs properly. These principles take into consideration build time and run time. A container is self-contained, relying only on the Linux kernel. Once the container is built, then additional libraries can be added. In addition, containerized applications are not meant to change to different environments after they are built.

In terms of run time, each container needs to implement APIs to help the platform manage the application in the most efficient way possible. All APIs must be public, as there should be no hidden or private APIs. In addition, APIs should be declarative, meaning the programmer should be able to communicate their desired end result, allowing Kubernetes to find and implement a solution. Support is available to developers, if needed, to run applications in Kubernetes. Workloads are portable, and the control plane is able to transfer a workload to another node without disrupting the overall program.



## Declarative configuration

Declarative configuration is an approach that is commonly used in Kubernetes to achieve a desired state of an application. In this approach, developers specify the desired state, but they do not explicitly define how to achieve or reach the desired state. The approach is more focused on what the desired state should be. The system will determine the most efficient and reliable way to achieve the desired state. These configuration assets are stored in a revision control system and track changes over time.

To use declarative configuration in Kubernetes, create a manifest that describes the desired state of an application. Then, the control plane will determine how to direct nodes in the cluster to achieve the desired state.



## The control plane

The Kubernetes control plane is responsible for making decisions about the entire cluster and desired state and for ensuring the cluster’s components work together. Components of the control plane include: 

* etcd
* API server
* Scheduler
* Controller manager
* Cloud controller manager

**etcd** is used as Kubernetes backing store for all cluster data as a distributed database. This key-value store is highly available and designed to run on multiple nodes.

The Kubernetes **API server** acts as the front-end for developers and other components interacting with the cluster. It is responsible for ensuring requests to the API are properly authenticated and authorized.

The **scheduler** is a component of the control plane where pods are assigned to run on particular nodes in the cluster.

The **control manager** hosts multiple Kubernetes controllers. Each controller continuously monitors the current state of the cluster and works towards achieving the desired state.

The **cloud controller manager** is a control plane component that embeds cloud-specific control logic. It acts as the interface between Kubernetes and a specific cloud provider, managing the cloud’s resources.



## Key takeaways

Kubernetes is a portable and extensible platform to assist developers with containerized applications. Kubernetes core principles and key components support developers with starting, stopping, storing, building, and managing containers.
