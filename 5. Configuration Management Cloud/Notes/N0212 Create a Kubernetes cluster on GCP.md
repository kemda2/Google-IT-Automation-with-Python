## Introduction
A Kubernetes cluster is a fundamental construct within Kubernetes. The cluster enables the deployment, coordination, and operation of containerised applications at scale. Instead of one incredibly huge, ridiculously fast server positioned in one place to process requests from all around the world, clusters are lots of smaller servers spread out and coordinated to serve everyone close to where they are. 

A cluster is a group of machines grouped to work together, but not necessarily all doing the same tasks. In a Kubernetes cluster, virtual machines (VMs) are coordinated to execute all of the functions needed to process requests, such as serving a web application, running a database, or solving big-data problems. Each cluster consists of at least one cluster control plane machine, a server that manages multiple nodes. You submit all of your work to the control plane, and the control plane distributes the work to the node or nodes where it will run. These worker nodes are virtual machine (VM) instances running the Kubernetes processes necessary to make them part of the cluster. They can be in a single zone or spread out all over the world. Depending on the use case, one node might be used for data processing and another for hosting a web server. Each of these nodes is made up of pods, which are assigned by the control plane. Each pod is made up of one or more containers that work together to execute necessary functions. 

Have you ever been to a restaurant where there is a rolling tray of desserts? Well, the tray is like a cluster, holding all the little plates. The plates are like nodes, each working to hold a different dessert. The desserts are like the pods, each performing a different flavor, or function. 

In this reading, you’ll learn about the steps to creating a Kubernetes cluster on Google Cloud Platform (GCP), and you’ll get some pro tips on the process. 
## Setup
You have already gone through a lot of the prerequisites to creating a Kubernetes cluster on GCP. As a review, and for when you do this work outside of the course, you’ll need to do the following:
* Create a valid GCP account and access to the Google Cloud Console. To open a new GCP account, start at the ~[Google Cloud console start page](https://cloud.google.com/cloud-console?utm_source=google&utm_medium=cpc&utm_campaign=na-US-all-en-dr-bkws-all-all-trial-b-dr-1605212&utm_content=text-ad-none-any-DEV_c-CRE_665735422256-ADGP_Hybrid%20%7C%20BKWS%20-%20MIX%20%7C%20Txt_Cloud%20Console-KWID_43700077225654723-kwd-296393718382&utm_term=KW_google%20cloud%20console-ST_google%20cloud%20console&gclid=EAIaIQobChMIh97S_7fLgAMV8qBaBR0w_QaQEAAYASAAEgLqT_D_BwE&gclsrc=aw.ds)~. 
* Create a GCP project where you will deploy your Kubernetes cluster.
* Enable billing for your GCP project to use Google Kubernetes Engine (GKE), as this may involve charges for the resources you use.
* Create a service account for GKE with the necessary permissions to manage resources in your GCP project.
* Install the Google Cloud SDK on your local machine. It provides the necessary tools and commands to interact with GCP resources.
* Install kubectl on your local machine. kubectl is a command-line tool used to interact with Kubernetes clusters.
* (Optional) If you're creating a private Kubernetes cluster, set up a Virtual Private Cloud (VPC) network or use an existing one to define the network boundaries for your cluster.
* Configure firewall rules to allow necessary network traffic to and from your cluster.

**Note:** If you plan to use private container images, set up a container registry like ~[Google Artifact Registry](https://cloud.google.com/artifact-registry/docs)~ to store your Docker images. This is entirely optional. 

Once you have met these prerequisites, you can proceed to create your Kubernetes cluster using Google Kubernetes Engine through the Google Cloud Console or use the gcloud command-line tool.

Let’s get started! 
## Creating a GKE Cluster using Google Cloud Console
As you get started working with Kubernetes clusters on Google Cloud Platform (GCP), the first thing to do is create a cluster to work with. Here are the steps to creating a standard cluster: 

1.  Log in to Google Cloud Console: Go to https://console.cloud.google.com/ and log in with your Google Cloud account.

2.  Open Google Kubernetes Engine (GKE). In the left-hand navigation menu, select **Kubernetes Engine**, and then **Clusters**.

3.  Click **Create Cluster** to create a new Kubernetes cluster. By default, this will take you to Autopilot cluster. For these instructions, we are setting up a standard cluster, so click **Switch to Standard Cluster**. For more information on the difference between Standard and Autopilot, see ~[Compare GKE Autopilot and Standard](https://cloud.google.com/kubernetes-engine/docs/resources/autopilot-standard-feature-comparison)~.

4.  Configure cluster basics. Enter a unique cluster name for your GKE cluster.

5.  Choose a Location type. Zonal is for creating a cluster within a single zone. When selecting this, you will also need to select the zone where your cluster's control plane will run. 

Regional is for multi-zone deployment. Deployment across a larger area means higher availability to users. When selecting a regional cluster, you’ll also need to choose the region. By default, three zones will be selected within the chosen region, or you can manually select the zones if you wish.

6.  Configure the node pool. In the Node pool section, specify the desired node count for the initial number of nodes in the default node pool depending on the needs of your application on your Kubernetes cluster. For production clusters, the recommended minimum is usually three nodes. 

The maximum number of nodes will depend on the type of application, the expected amount of traffic, and your budget. A maximum of five to ten nodes is a good start while you get a feel for what's needed. As you configure the node pool, there's a cost estimator on the right side of the screen that estimates how much you will pay per month. You can also look over the ~[GKE pricing for Standard mode](https://cloud.google.com/kubernetes-engine/pricing#standard_mode)~. If you don’t set a maximum that suits your budget, and demand for your application rises sharply, you could get an expensive wake-up call. 

Once you have configured the node pool, you can enable Autoscaling by checking the box for Enable cluster autoscaler. Once enabled, Autoscaler will automatically adjust the number of nodes based on resource utilization up to the maximum number of nodes you set for the Node pool. 

Finally, choose the machine type for your nodes. There are four machine families: 

* General purpose machines are suitable for most workloads. These machines balance performance with price.
* Compute-optimized machines provide high performance for intensive workloads like artificial intelligence and machine learning, entertainment streaming, and game servers
* Memory-optimized machines offer the highest memory configurations. These machines process large data sets in memory in use cases like Big Data analytics.
* Accelerator-optimized machines are for very demanding workloads like machine learning (ML) training and inference, in which a neural network makes deductions about new data based on what it has already learned. 

For more details on choosing machine families or specific types, see ~[Choosing the right machine family and type](https://cloud.google.com/blog/products/compute/choose-the-right-google-compute-engine-machine-type-for-you)~.

7.  Choose any optional configurations needed. Based on your projects’ specific requirements, you can expand the Node pool section to configure advanced settings including boot disk size, preemptible nodes, node labels, and node locations.

You can also enable networking and security features based on the data governance laws and the level of security you need to maintain for your data. In the Networking section, you can choose the VPC network and subnetwork where your cluster's nodes will be placed. You can also enable Private cluster mode to hide the cluster's master endpoint from the public internet. For pod-level firewall rules, you can define network tags and network policies.

8.  Click the **Create** button to start creating the GKE cluster.

9.  Wait for cluster creation. GKE will begin creating your cluster based on your specified configuration. The process may take a few minutes.

10.  Access and use your cluster. Once the cluster is successfully created, you can click on the cluster name in the GKE dashboard to view its details and manage the cluster.

## Congratulations!
That's it! You have now created a Kubernetes cluster on GCP using GKE with the desired configurations, including the specified node count and other settings. You can now start deploying and managing your applications on the GKE cluster.

**Pro tip**: Using kubectl

To access and manage your cluster from your local machine using kubectl, click the "Connect" button in the cluster details view. This will provide you with the necessary kubectl command to authenticate and connect to your GKE cluster. 

kubectl is the Kubernetes command-line tool for interacting with the cluster. Command line is a bit daunting but it allows you to document the steps you take and reuse the commands in the future. Once you get used to working with kubectl, it can streamline your process, allowing you to keep notes and commands all in one place. 

## Key takeaways
It’s easy to create a Kubernetes cluster on GCP that meets your exact requirements. Kubernetes clusters allow multiple nodes to work together in concert no matter their physical distance.  
