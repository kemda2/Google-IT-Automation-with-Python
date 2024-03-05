#  Protect containers on GCP

As Python developers working with Kubernetes on Google Cloud Platform (GCP), understanding how to protect your containers is crucial. This involves a combination of tools and practices provided by GCP, as well as your own responsibilities in configuring and managing these resources.

## Security challenges and considerations

The first step in protecting your containers is understanding the security challenges and considerations involved. Containers, while providing a lightweight and portable solution for running your applications, also come with their own set of security challenges. These include the need to secure the container runtime, to protect the underlying host system, and to manage the application dependencies that are packaged within the container.

One approach to addressing this challenge is the Zero Trust model, which involves assuming no trust by default and only granting permissions as necessary. This means starting with a completely locked down system and only opening up what is necessary for your application to function. This approach can help to minimize the potential attack surface and reduce the risk of a security breach.

You can read more about the Zero Trust model ~[here](https://www.nist.gov/publications/zero-trust-architecture)~.

Also, building on the previous reading about GCP networking, using Virtual Private Clouds (VPCs) and properly firewalled subnets means you can guarantee at the network level—not the software level—that things do not come into contact with other things they shouldn’t. It is easier to build a moat than a drawbridge!

## Shared Responsibility Model

Another model you can implement for container security is the Shared Responsibility Model. This model outlines the responsibilities of both GCP and you in ensuring the security of the containers. In this model, GCP is responsible for:

* **Infrastructure security:** GCP is responsible for the physical security of data centers, the security of the hardware and software that underpin the service, and the networking infrastructure of the container orchestration service, Google Kubernetes Engine (GKE). 
* **Operational security:** GCP is responsible for ensuring that the GKE service is operational and available for customers to use. This includes protecting against threats that could impact the service's availability, such as Distributed Denial of Service (DDoS) attacks.
* **Software supply chain security:** GCP provides tools and features to help secure the software supply chain, such as Binary Authorization for Borg (BAB), which can enforce signature verification checks on container images before they are deployed.

Tools help provide security, but can be configured incorrectly. That’s where you come in! To make effective use of the container security tools offered by GCP, you are responsible for:

* **Workload security:** You are responsible for ensuring the security of the workloads (i.e., the applications and data) that you run on GKE. This includes implementing appropriate access controls, protecting sensitive data, and managing cryptographic keys.
* **Network security:** Although GCP provides the underlying network infrastructure, you are responsible for securing the network connections between your workloads. This includes configuring firewalls, managing network policies, and securing network endpoints.
* **Identity and access management:** You are responsible for managing access to your GKE resources. This includes managing user identities, assigning appropriate roles and permissions, and using strong authentication methods.
* **Software supply chain security:** Although GCP provides tools to help secure the software supply chain, you are responsible for using these tools effectively. This includes ensuring that container images are securely built, stored, and signed.

## Security Features and Best Practices

As mentioned above, a zero trust approach makes sense. Start with the least possible amount of permissions, open ports, and only change the bare minimum to what is needed to provide service. Security is usually reactive, so this lowers the attack surface for your cloud builds, giving less ways for attackers to get in.

Other security strategies you can implement include:

* **Use minimal base images:** The fewer components and services running in your container, the fewer potential vulnerabilities. Use minimal base images that only contain the essential components needed for your application. This means closing all IP addresses and ports except those that are necessary, closing data containers off to the outside internet so only parts of the application can reach them, and so on. This can also mean only opening up containers on VPCs to other VPCs or members of the same subnet, and having sound firewall rules in place.
* **Regularly update and patch:** This may seem obvious, but regularly update your containers and their dependencies to ensure you have the latest security patches. Outdated software is one way vulnerabilities get in. Sometimes new software is shipped that has new bugs that do not get discovered for a while. Just updating containers is not sufficient to guarantee safety, but it can reduce the risk. Google Cloud provides services like Container-Optimized OS which automatically updates and patches itself.
* **Implement vulnerability scanning:** Use tools like Google's Container Analysis and Container Threat Detection in the Google Cloud console to regularly scan your containers for known vulnerabilities.
* **Use runtime security:** Use a tool like gVisor to provide sandboxing for containers at runtime, isolating them from the host kernel and reducing the risk of a container escape vulnerability.
* **Implement access controls:** Use Identity and Access Management (IAM) to control who can do what with your containers and other resources.
* **Encrypt sensitive data:** Use Google's Key Management Service (KMS) to encrypt sensitive data in your containers.
* **Monitor and log activity:** Use Google's Cloud Audit Logs to keep track of who did what, when, in your Google Cloud environment. Logs are super important to have on from the start. If you wait for an incident to happen to necessitate turning on logs, it may be too late!
* **Use binary authorization:** This is a deploy-time security control that ensures only trusted images are deployed in your environment.

## Key takeaways

Container security is a vast topic that could easily be its own course. For right now, however, the key takeaways from this reading are:

* Containers pose some unique security challenges, including securing the container runtime, protecting the host system, and managing application dependencies.
* Adopting a Zero Trust model can help mitigate these challenges. This approach involves assuming no trust by default and only granting permissions as necessary, reducing the potential attack surface.
* Security on GCP is a shared responsibility. GCP is responsible for infrastructure security, operational security, and providing tools for software supply chain security. Developers are responsible for workload security, network security, identity and access management, and effective use of software supply chain security tools.
* GCP provides several security features and best practices for protecting containers, including using minimal base images, regularly updating and patching containers, implementing vulnerability scanning, using runtime security tools like gVisor, implementing access controls with IAM, encrypting sensitive data with KMS, monitoring and logging activity with Cloud Audit Logs, and using Binary Authorization to ensure only trusted images are deployed.

## Resources for more information

* ~[Exploring Container Security](https://cloud.google.com/blog/products/containers-kubernetes/exploring-container-security-let-google-do-the-patching-with-new-managed-base-images)~
* ~[Google Cloud Security Command Center](https://cloud.google.com/security-command-center/docs/concepts-security-command-center-overview)~
* ~[Shared Responsibilities and Shared Fate on Google Cloud](https://cloud.google.com/architecture/framework/security/shared-responsibility-shared-fate)~
* ~[GKE shared responsibility | Google Kubernetes Engine \(GKE\)](https://cloud.google.com/kubernetes-engine/docs/concepts/shared-responsibility)~
