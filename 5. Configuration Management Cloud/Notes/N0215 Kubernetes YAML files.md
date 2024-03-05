# Kubernetes YAML files

Suppose you're a Python developer working on a web application that's experiencing a surge in user traffic. You've containerized your application using Docker, but manually scaling the application to keep up with demand is becoming cumbersome. Kubernetes to the rescue! Kubernetes can manage and scale your containerized application automatically…if you can tell it what to do! This is where Kubernetes YAML files come in.

**Kubernetes YAML files** define and configure Kubernetes resources. They serve as a declarative blueprint for your application infrastructure, describing what resources should be created, what images to use, how many replicas of your service should be running, and more.
## Structure of Kubernetes YAML files
Every Kubernetes YAML file follows a specific structure with key components: **API version, kind, metadata**, and **spec**. These components provide Kubernetes with everything it needs to manage your resources as desired. 
	
* **apiVersion**: This field indicates the version of the Kubernetes API you're using to create this particular resource.
* **kind**: This field specifies the type of resource you want to create, such as a Pod, Deployment, or Service.
* **metadata**: This section provides data that helps identify the resource, including the name, namespace, and labels.
* **spec**: This is where you define the desired state for the resource, such as which container image to use, what ports to expose, and so on.

Let's illustrate this with a simple Kubernetes YAML file for creating a Deployment of your Python web application:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: python-web-app
  labels:
    app: python-web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: python-web-app
  template:
    metadata:
      labels:
        app: python-web-app
    spec:
      containers:
      - name: python-web-app
        image: your-docker-repo/python-web-app:latest
        ports:
        - containerPort: 5000
```


In the YAML file above, we're defining a "Deployment" resource for a Kubernetes cluster. A Deployment is a way to tell Kubernetes how to run our application. This YAML file tells Kubernetes to create a Deployment named "python-web-app", which will ensure that three instances of our Python web application are always running.
## Key components and fields in Kubernetes YAML files
YAML files can include many other fields, depending on the type of object and your specific needs. 

### Pods
As you’ve learned, a Pod is the smallest and simplest unit in the Kubernetes object model. It represents a single instance of a running process in a cluster and can contain one or more containers. Because it is the simplest unit, a Pod’s YAML file typically contains the basic key components highlighted above:
	
* **apiVersion**: This is the version of the Kubernetes API you're using to create this object.
* **kind**: This is the type of object you want to create. In this case, it's a Pod.
* **metadata**: This includes data about the Pod, like its name and namespace.
* **spec**: This is where you specify the desired state of the Pod, including the containers that should be running. Specifications include:
	* Containers: An array of container specifications, including "name", "image", "ports", and "env".
  * Volumes: Array of volume mounts to be attached to containers
  * restartPolicy: Defines the Pod's restart policy (e.g., "Always," "OnFailure," "Never")

### Deployments
A Deployment is a higher-level concept that manages Pods and ReplicaSets. It allows you to describe the desired state of your application, and the Deployment controller changes the actual state to the desired state at a controlled rate. In addition to the fields mentioned above, a Deployment's YAML file includes:

* **spec.replicas**: This is the number of Pods you want to run.
* **spec.selector**: This is how the Deployment identifies the Pods it should manage.
* **spec.template**: This is the template for the Pods the Deployment creates.

### Services
A Service in Kubernetes is an abstraction which defines a logical set of Pods and a policy by which to access them. Key components in a Service's YAML file include:
	
* **spec.type**: This defines the type of Service. Common types include ClusterIP, NodePort, and LoadBalancer.
* **spec.ports**: This is where you define the ports the Service should expose.
* **spec.selector**: This is how the Service identifies the Pods it should manage.

### ConfigMaps
A ConfigMap is an API object used to store non-confidential data in key-value pairs. In addition to the common fields, a ConfigMap's YAML file includes the data field, which is where you define the key-value pairs.

### Secrets
A Secret is similar to a ConfigMap, but is used to store sensitive information, like passwords or API keys. A Secret's YAML file includes:

* **type**: The type of Secret. Common types include Opaque (for arbitrary user-defined data), kubernetes.io/service-account-token (for service account tokens), and others.
* **data**: This is where you define the key-value pairs. The values must be base64-encoded.

Each of these resources can be defined and managed using Kubernetes YAML files. For example, a YAML file for a Secret resource might look like this:

```
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  db_username: dXNlcm5hbWU=  # base64 encoded username
  db_password: cGFzc3dvcmQ=  # base64 encoded password
```


## Parameterizing YAML files with Python
As you’ve seen, YAML files are the backbone of defining and managing resources. However, static YAML files can be limiting, especially when you need to manage different configurations for different environments or deployment scenarios. This is where Python comes in, offering a dynamic and flexible approach to parameterize your YAML files.
For instance, you can customize your rolling update strategy using Python with the following example code.
 
```
from kubernetes import client, config

def update_deployment_strategy(deployment_name, namespace, max_unavailable):
    config.load_kube_config()
    apps_v1 = client.AppsV1Api()
​
    deployment = apps_v1.read_namespaced_deployment(deployment_name, namespace)
    deployment.spec.strategy.rolling_update.max_unavailable = max_unavailable
    apps_v1.patch_namespaced_deployment(deployment_name, namespace, deployment)
​
if __name__ == "__main__":
    update_deployment_strategy('my-deployment', 'my-namespace', '25%')
```


This is just one example of how Python provides a powerful and flexible way to parameterize your YAML files in Kubernetes. 
## Key takeaways
Kubernetes YAML files play a crucial role in defining and managing Kubernetes resources, enabling Python developers to manage their applications' infrastructure in a consistent, version-controlled, and automated manner. By understanding the structure of these files and their key components, developers can leverage Kubernetes to its full potential and focus more on writing the application logic rather than managing infrastructure.
## Resources for more information
~[Objects in Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/)~
~[Get Started with Kubernetes \(using Python\)](https://kubernetes.io/blog/2019/07/23/get-started-with-kubernetes-using-python/)~
