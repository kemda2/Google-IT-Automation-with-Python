# Installing Kubernetes 

There are multiple ways to set up and run a Kubernetes cluster. Because Kubernetes acts as a set of containers that manages other containers, Kubenetes is not something you download. You decide on the installation type you need based on your programming requirements.

In this reading, you will learn more about a Kubernetes cluster, including how to set it up and run it using Docker Desktop, and you’ll receive step-by-step instructions along the way.



## Download Docker

You should already have Docker up and running on your computer or laptop. If you don’t, download and install Docker according to your operating system:

Windows: [Install Docker desktop on Windows | Docker documentation](https://docs.docker.com/desktop/install/windows-install/)

macOS: [Install Docker desktop on Mac | Docker documentation](https://docs.docker.com/desktop/install/mac-install/)

Linux: [Install Docker desktop on Linux | Docker documentation](https://docs.docker.com/desktop/install/linux-install/)

## Enable Kubernetes

After Docker is installed on your machine, follow the instructions below to run Kubernetes in Docker Desktop.

1. From the Docker Dashboard, select Settings.

2. Select Kubernetes from the left sidebar.

3. Select the checkbox next to Enable Kubernetes.

4. Select Apply & Restart to save the settings.

5. Select Install to complete the installation process.

The Kubernetes server runs as containers and installs the **/usr/local/bin/kubect1** command on your machine.

And that’s it! Setting up Kubernetes on Docker Desktop is typically the most common way that developers use Kubernetes since Docker Desktop has built-in support for it. Below are additional tools that you can use to start a Kubernetes cluster.

* [kind](https://kind.sigs.k8s.io/docs/user/quick-start/) 
* [k3s](https://docs.k3s.io/quick-start) 
* [microk8s](https://microk8s.io/docs/getting-started)
* [minikube](https://minikube.sigs.k8s.io/docs/start/) 



## Key takeaways

Kubernetes is not a replacement for Docker, but rather a tool that developers use while working in Docker. It can run and manage Docker containers, allowing developers to deploy, scale, and manage containerized applications across clusters.
