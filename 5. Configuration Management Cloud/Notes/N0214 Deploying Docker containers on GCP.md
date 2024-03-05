#  Deploying Docker containers on GCP

Docker containers make it simple to deploy applications across different systems and platforms, allowing them to run the same way no matter what environment they are deployed to. This makes it easy to share, test, manage, and deploy applications quickly and reliably. 

There are several platforms that allow you to deploy Docker containers, and each has its own set of advantages. Let’s look at some of these, and some considerations when choosing where to deploy containers. 
## Docker containers on Google Cloud Run
If you don’t need a lot of flexibility in your configuration, you might find  Google Cloud Run to be a good option. Cloud Run is a fully-managed platform that allows you to run containerised applications without having to manage the underlying infrastructure. The platform offers easy deployment, and automatically manages scaling and routing traffic based on incoming requests. It can scale down to zero, which means it will not use any unnecessary resources if there are no requests. The platform is based on containers, so you can write your code in any language and then deploy it through Docker images. 

Cloud Run may be the best choice of platform for projects that do not need a high level of monitoring or configuration, providing that these applications are stateless. A stateless application is one which does not read or store information about their states from one run to the next. Kubernetes Deployment is most commonly used for stateless applications, so Cloud Run is often a great option . 

Cloud Run Deploying Docker containers on Cloud Run 

To deploy Docker containers on Cloud Run:
	
  1.	Build your Docker image and push it to any supported  container registry.
  2.	Deploy the container to Cloud Run using the **gcloud run deploy** command or through the Cloud Run Console.

For more about deploying an app to Cloud Run, see ~[Deploy to Cloud Run](https://cloud.google.com/run/docs/quickstarts/deploy-container)~. 
## Docker containers on Google Kubernetes Engine (GKE)
Google Kubernetes Engine (GKE) is a container orchestration platform provided by Google Cloud that allows you to automate the process of deploying, managing, and scaling containerised applications. Its streamlined cluster setup process makes deploying Kubernetes clusters fast and straightforward. Many functions are automated as well, including version upgrades and management of SSL certificates. 

Although GKE gives you control of all of your configurations, you can choose GKE Autopilot as a fully-managed option. Autopilot uses the Google Cloud Platform (GCP) to automate cluster configuration and to scale the underlying infrastructure based on your parameters and your application's resource requirements. This eliminates the need for manual intervention on your part, and optimizes resources. 

GKE is also particularly resilient, continuously monitoring the cluster and its components. Built-in monitoring and logging features provide real-time insights into your application's performance and health. But you don’t have to watch constantly, because GKE features self-healing clusters which  automatically detect and replace unhealthy nodes or containers, maintaining the desired state and application availability. 

GKE is also convenient for integration with all of the Google Cloud ecosystem, making it easy to leverage other services like Cloud Storage and Google Cloud Identity and Access Management (IAM) to enhance security and governance. GCP itself ensures regular security updates and follows industry best practices to protect the underlying infrastructure and containers.

You may not be ready for the following consideration, but GKE also supports running “stateful” applications. A stateful application is one for which a server saves status and session information. Kubernetes Deployment is commonly used for stateless applications, but you can make an application stateful by attaching a persistent volume to it.  If you find yourself needing to run a stateful application, GKE is a great option. 
## Deploying Docker containers on GKE
Now that you’ve heard about GKE’s features, here's how you can deploy Docker containers on GKE:
	
1. Build your Docker image and push it to any supported  container registry, such as Google Container Registry (GCR).
2. Create a Kubernetes Deployment manifest that specifies your configuration settings, including the container image you want to run and the desired number of replicas.
3. Use the GKE Console, or the Kubernetes command line tool kubectl, to deploy the application to your GKE cluster. GKE will handle the orchestration and scaling of the containers for you.

For more about deploying an app to a GKE cluster, see ~[Deploy an app to a GKE cluster](https://cloud.google.com/kubernetes-engine/docs/deploy-app-cluster)~.

For more on choosing between GKE and Cloud Run, see~[Google Kubernetes Engine vs Cloud Run: Which should you use?](https://cloud.google.com/blog/products/containers-kubernetes/when-to-use-google-kubernetes-engine-vs-cloud-run-for-containers)~
## Docker containers on Google Compute Engine
Finally, Google Compute Engine is a virtual machine (VM) service that allows you to run your containerized applications on Google's infrastructure. It has lower access time, which tends to translate to faster performance, and offers easy integration with other GCP services. 

Perhaps most attractive to its users, Google Compute Engine lets you run code on Google’s infrastructure, but grants you more control over the underlying infrastructure of your VM instances than GKE, and far more than Cloud Run. It is particularly suitable for custom environments and applications requiring specific configurations. But with more control comes more responsibility: when using Google Compute Engine, you are responsible for managing the VM instances and scaling. The platform itself is not as simplified as GKE or Cloud Run, and you cannot use all programming languages. 
## Deploying Docker containers on Google Compute Engine
To deploy Docker containers on Google Compute Engine:

1. Build your Docker image and push it to any supported  container registry.
2. Provision a VM instance on Google Compute Engine.
3. Install Docker on the VM.
4. Build your Docker image and copy it to the virtual machine (or pull the image from a container registry).
5. Run the Docker container on the virtual machine using the **docker run** command.

For more about containers on Compute Engine, see ~[Containers on Compute Engine](https://cloud.google.com/compute/docs/containers/)~.
## Key takeaways
GCP offers several choices for deploying Docker containers, all of which allow you to integrate with other Google services. Cloud Run is the simplest to use, offering a fully managed platform, but with little customization. GKE is a powerful platform that offers more flexibility in configuration coupled with plenty of options for automation. Google Compute Engine lets you control your environments and applications while they run on Google’s infrastructure, but requires significantly more technical knowledge than Cloud Run or GKE. The best option for you will be based on your needs.  
