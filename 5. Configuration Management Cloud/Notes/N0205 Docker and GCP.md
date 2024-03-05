# Docker and GCP

Docker and Google Cloud Platform (GCP) are two types of technologies that complement each other, allowing programmers to build, deploy, and manage containerized applications in the cloud.

In this reading, you will learn more about GCP, how to run Docker containers in GCP, and how to use Cloud Run.



## Google Cloud Platform

GCP is a composition of all the cloud services provided by Google. These include:

* Virtual machines
* Containers
* Computing
* Hosting
* Storage
* Databases
* Tools
* Identity management

GCP is widely used by businesses, startup companies, developers, and organizations of all sizes across a variety of industries to help their users go digital.



## How to run Docker containers in GCP

You can run containers two ways in the cloud using GCP. The first way is to start a virtual machine with Docker installed on it. Use the docker run command to create a container and start it. This is the same process for running Docker on any other host machine.

The second way is to use a service called Cloud Run. This serverless platform is managed by Google and allows you to launch containers without worrying about managing the underlying infrastructure. Cloud Run is simple and automated, and it’s designed to allow programmers to be more productive and move quickly.

An advantage of Cloud Run is that it allows you to deploy code written in any programming language if you can put the code into a container.



## Use Cloud Run to deploy containers in GCP

Before you begin, sign into your Google account, or if you do not have one, create an account.

1. Open [Cloud Run](https://console.cloud.google.com/run?enableapi=true&_ga=2.103152064.1978640569.1689869801-335443466.1689535280).

2. Click **Create service** to display the form.

    In the form,

    1. Select **Deploy one revision from an existing container image**.
    
    2. Below the **Container image URL** text box, select **Test with a sample container**.
    
    3. From the **Region** drop-down menu, select the region in which you want the service located.
    
    4. Below **Authentication**, select **Allow unauthenticated invocations**.
    
    5. Click **Create** to deploy the sample container image to Cloud Run and wait for the deployment to finish.

3.  Select the displayed URL link to run the container.

**Pro tip:** Cloud Run helps keep costs down by only charging you for central processing unit (CPU) time while the container is running. It’s unlike running Docker on a virtual machine, for which you must keep the virtual machine on at all times—running up your bill.



## Key takeaways

GCP supports Docker containers and provides services to support containerized applications. Integrating GCP and Docker allows developers and programmers to build, deploy, and run containers easily while being able to focus on the application logic.
