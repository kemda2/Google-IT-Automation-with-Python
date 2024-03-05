# Deployment


## What are deployments?

Let’s continue the example of the Python-based web application running in a Kubernetes cluster, specifically the web server component of the application. As traffic to your application grows, you'll need to scale the number of web server instances to keep up with demand. Also, to ensure high availability, you want to maintain multiple replicas of the web server so that if one instance fails, others can take over. This is where Kubernetes Deployments come in.

**In Kubernetes, a Deployment is like your application's manager.** It's responsible for keeping your application up and running smoothly, even under heavy load or during updates. It ensures your application, encapsulated in Pods, always has the desired number of instances—or “replicas”—running.

Think of a Deployment as a blueprint for your application's Pods. It contains a **Pod Template Spec**, defining what each Pod of your application should look like, including the container specifications, labels, and other parameters. The Deployment uses this template to create and update Pods.

A Kubernetes Deployment also manages a **ReplicaSet**, a lower-level resource that makes sure the specified number of identical Pods are always running. The Deployment sets the desired state, such as the number of replicas, and the ReplicaSet ensures that the current state matches the desired state. If a Pod fails or is deleted, the ReplicaSet automatically creates new ones.  In other words, Deployments configure ReplicaSets, and thus, they are the recommended way to set up replication.

And by default, deployments support **rolling updates and rollbacks**. If you update your web server's code, for example, you can push the new version with a rolling update, gradually replacing old Pods with new ones without downtime. If something goes wrong, you can use the Deployment to rollback to a previous version.

So, in summary, a Kubernetes Deployment consists of several key components:

* **Desired Pod template:** This is the specification that defines the desired state of the Pods managed by the Deployment. It includes details such as container images, container ports, environment variables, labels, and other configurations.
* **Replicas:** This field specifies the desired number of identical copies of the Pod template that should be running. Kubernetes ensures this number of replicas is maintained, automatically scaling up or down as needed.
* **Update strategy:** This defines how the Deployment handles updates. The default is a rolling update strategy, where Kubernetes performs updates by gradually replacing Pods, keeping the application available throughout the process. This strategy can be further customized with additional parameters.



## Powerful features

Deployments not only help maintain high availability and scalability, but they also provide several powerful features:

* **Declarative updates:** With a declarative update, you just specify the desired state of your application and the Deployment ensures that this state is achieved. If there are any differences between the current and desired state, Kubernetes automatically reconciles them. 
* **Scaling:** You can easily adjust the number of replicas in your Deployment to handle increased or decreased loads. For example, you might want to scale up during peak traffic times and scale down during off-peak hours.
* **History and revision control:** Deployments keep track of changes made to the desired state, providing you with a revision history. This can be useful for debugging, auditing, and rolling back to specific versions.

A Kubernetes Deployment is typically defined using a YAML file that specifies these components. Here is an example YAML manifest.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
    app: example-app
  template:
    metadata:
    labels:
        app: example-app
    spec:
    containers:
    - name: example-container
        image: example-image:latest
        ports:
        - containerPort: 80
```

This Deployment specifies that it should maintain three replicas of the **example-container** Pod template. The Pods are labeled with **app: example-app**, and the container runs an image tagged as **example-image:latest** on port 80. The default rolling update strategy will be used for any updates to this Deployment. 

By utilizing Deployments, you can manage your Python web server's life cycle more efficiently, ensuring its high availability, scalability, and smooth updates. 



## Deployments and Python

The following Python script uses the Kubernetes Python client to create, list, and delete Kubernetes Services in a given namespace.

```
from kubernetes import client, config

def create_deployment(api_instance, namespace, deployment_name, image, replicas):
    # Define the Deployment manifest with the desired number of replicas and container image.
    deployment_manifest = {
        "apiVersion": "apps/v1",
        "kind": "Deployment",
        "metadata": {"name": deployment_name},
        "spec": {
            "replicas": replicas,
            "selector": {"matchLabels": {"app": deployment_name}},
            "template": {
                "metadata": {"labels": {"app": deployment_name}},
                "spec": {
                    "containers": [
                        {"name": deployment_name, "image": image, "ports": [{"containerPort": 80}]}
                    ]
                },
            },
        },
    }

    # Create the Deployment using the Kubernetes API.
    api_response = api_instance.create_namespaced_deployment(
        body=deployment_manifest,
        namespace=namespace,
    )
    print(f"Deployment '{deployment_name}' created. Status: {api_response.status}")

def update_deployment_image(api_instance, namespace, deployment_name, new_image):
    # Get the existing Deployment.
    deployment = api_instance.read_namespaced_deployment(deployment_name, namespace)

    # Update the container image in the Deployment.
    deployment.spec.template.spec.containers[0].image = new_image

    # Patch the Deployment with the updated image.
    api_response = api_instance.patch_namespaced_deployment(
        name=deployment_name,
        namespace=namespace,
        body=deployment
    )
    print(f"Deployment '{deployment_name}' updated. Status: {api_response.status}")

def delete_deployment(api_instance, namespace, deployment_name):
    # Delete the Deployment using the Kubernetes API.
    api_response = api_instance.delete_namespaced_deployment(
        name=deployment_name,
        namespace=namespace,
        body=client.V1DeleteOptions(
            propagation_policy="Foreground",
            grace_period_seconds=5,
        )
    )
    print(f"Deployment '{deployment_name}' deleted. Status: {api_response.status}")


if __name__ == "__main__":
    # Load Kubernetes configuration (if running in-cluster, this might not be necessary)
    config.load_kube_config()

    # Create an instance of the Kubernetes API client for Deployments
    v1 = client.AppsV1Api()
​
    # Define the namespace where the Deployment will be created
    namespace = "default"
​
    # Example: Create a new Deployment
    create_deployment(v1, namespace, "example-deployment", image="nginx:latest", replicas=3)
​
    # Example: Update the image of the Deployment
    update_deployment_image(v1, namespace, "example-deployment", new_image="nginx:1.19.10")
​
    # Example: Delete the Deployment
    delete_deployment(v1, namespace, "example-deployment")
```



## Additional learning points

Beyond the fundamental concepts, you should be aware of a few additional features and best practices related to Kubernetes Deployments.

* **A fresh start:** While the default update strategy is rolling updates, Kubernetes also supports a "Recreate" strategy. In the "Recreate" strategy, all existing Pods are terminated before new Pods are created. This strategy may lead to brief periods of downtime during updates but can be useful in specific scenarios where a clean restart is necessary.
* **Don’t get stuck:** Deployments have a progressDeadlineSeconds field, which sets the maximum time (in seconds) allowed for a rolling update to make progress. If progress stalls beyond this duration, the update is considered failed. This field helps prevent deployments from getting stuck in a partially updated state. Likewise, the minReadySeconds field specifies the minimum time Kubernetes should wait after a Pod becomes ready before proceeding with the next update. This can help ensure the new Pods are fully functional and ready to handle traffic before more updates are made.
* **Press pause:** Deployments can be paused and resumed to temporarily halt the progress of rolling updates. This feature is helpful when investigating issues or performing maintenance tasks. Pausing a Deployment prevents further updates until it is explicitly resumed.
* **It’s alive!:** Deployments can utilize liveness and readiness probes to enhance the health management of Pods. Liveness probes determine if a Pod is still alive and running correctly, while readiness probes determine if a Pod is ready to accept traffic. These probes help Kubernetes decide whether to consider a Pod as healthy or not during rolling updates and scaling operations.

If you want to learn more about Kubernetes Deployments and their components, you can explore the provided resources below.



## Key takeaways

From maintaining the desired state of your applications, managing updates and rollbacks, to ensuring high availability, Deployments provide a set of key features that streamline the deployment and management of containerized applications. 

* Deployments are crucial resources that manage and scale containerised applications. They automate the deployment and management of Pods and ReplicaSets.
* Deployments use a declarative approach, ensuring that the application's desired state is maintained across the cluster, providing high availability. In case of Pod or node failures, the Deployment replaces the affected Pods automatically.
* Deployments support rolling updates, allowing for smooth transitions during application updates with no downtime. They also offer the capability to roll back to a previous stable version in case of issues with a new update.
* Deployments have several key components, including the desired Pod template (which defines the desired state of the Pods), the number of replicas (indicating the desired level of availability and scalability), and the update strategy (which defines how updates to the Pod template are handled).



## Resources for more information

[Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) :Comprehensive documentation on Kubernetes Deployments, their use cases, and operations.

[Managing Resources](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/): A guide on managing Deployments in Kubernetes including rolling updates, scaling and rollback.

[Kubernetes ReplicaSets](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/): Detailed explanation on ReplicaSets in Kubernetes, their role in maintaining the desired number of Pods.

[Declarative Application Management in Kubernetes](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/declarative-config/): Understanding declarative approach in Kubernetes with configuration files.

[Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/): An in-depth guide on liveness and readiness probes, which enhance the health management of Pods.

[Rolling Back a Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment): Documentation on how to perform rollbacks on a Deployment.  
