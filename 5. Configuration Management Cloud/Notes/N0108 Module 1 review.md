# Module 1 review

This has been a big module! We’ve covered a lot of ground related to cloud computing. We started by learning about clouds — not the ones that float through the sky, but computer services that run in a data center or remote servers that we access over the Internet. These clouds have different service types, from a bare bones environment that gives you the computing power to run your own software with your own configuration settings, to those that deliver a whole application or program to a user, such as easy to use email solutions like Gmail, storage solutions like Google Cloud, or productivity suites like Google Workspace. 

Next we learned how to deploy a virtual machine (VM), made sure the VM was set up to serve our web app, and that it would stay updated via Puppet. A single VM can be useful for small operations with lower technical requirements, but as technical requirements increase, an organization will need to deploy more and larger cloud solutions. Luckily, it’s easy to scale in the cloud. So we turned that single VM into a customized VM template that could be used to clone that VM as many times as we want, so scaling our cloud deployments would be easy. 

When we had a VM template, we looked at different ways to interact with the platform. We saw how both the web interface and the command line tool can be used to create VMs in the cloud, modify their configuration, and control other things, using tools which are very effective at a small or medium scale. 

At a large scale, you’ll need to automate cloud deployments even further using orchestration. We looked at how tools like Terraform allow us to define our cloud infrastructure as code, which can give us a lot of control over things like how the infrastructure is managed, and how changes are applied. Orchestration lets us combine the power of infrastructure as code with the flexibility of cloud resources. 

Then it was time to look at some of the options for building software for the cloud. FIrst, we looked into the different types of storage available, and what to consider when deciding which storage solution to use. These considerations include how we want to request data from storage, and how fast we want to be able to access the requested data.

Maybe the number one reason for using cloud computing is how much computing power is available across many servers. But in order to distribute our service evenly across however many instances we have available, we use load balancing. We talked about the different methods load balancers use to distribute the workload, and how they can monitor server health to avoid sending requests to unhealthy servers. 

There is no doubt that computing methods are constantly changing, and this happens pretty fast. We talked about how change management allows us to make changes in a safe and controlled way. We looked at how continuous integration (CI) can build and test code every time there is a change, and how continuous deployment (CD) can automatically control the deployment of new code to a specified set of rules. And we talked about different environments where new code could be tested before being pushed to production. 

And we talked about limitations. Limitations you may come across when running services in the cloud are not the same as limitations when running services on physical machines, and you should take time to understand the limitations of any cloud solution you may choose. 

Basically, you just learned a lot about cloud computing in a short period of time. And there’s more to come. First, you’ve got a graded assessment that covers the material from this past module. Then it’s time to start learning about deploying applications to the cloud.
