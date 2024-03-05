# Scaling containers on GCP

One of the most important factors in cloud computing is scalability. For a moment, let’s imagine cloud computing as if it were an actual cloud in the sky. Clouds are made up of water vapor; the more vapor that joins the cloud, the larger it gets. As the cloud releases this water as snow or rain, the cloud gets smaller. That’s scalability; the process of expanding or shrinking as necessary.

The conditions in the atmosphere determine the shape of a cloud throughout this scaling process. There is a lot more we could say about sky-clouds, but let’s return to computing clouds. Your application's requirements are the conditions that determine the direction and method of scaling in cloud computing. 

## Horizontal and vertical scaling

Generally, we can talk about scaling on two axes, horizontal, meaning sideways, and vertical, meaning up and down. In horizontal scaling, more containers are added as needed. Horizontal scaling is useful for adding dedicated resources as the number of users increase, and creating fallback containers in case of failure. In vertical scaling, more resources are allocated to each container. Vertical scaling increases performance. 

## Multidimensional scaling

Multidimensional scaling is a combination of horizontal and vertical scaling. This is sometimes called diagonal scaling, because you are doing some horizontal scaling, adding more containers to add to the number of resources, and some vertical scaling, increasing the performance of existing or added resources. 

Imagine it’s autumn and someone is burning a pile of leaves, but the fire is a little bigger than they planned. That’s pretty dangerous, so they call the fire department. Meanwhile, they fill a bucket and use it to throw water on the fire. Neighbors come over, each with their own bucket, and start throwing more buckets of water. That’s horizontal scaling, the addition of more small resources. 

The fire truck rolls up and hooks up the big hose, but the pressure isn’t very good. In fact it isn’t any better than the pressure from the hoses that other neighbors have stretched from their own homes. All these hoses are moving more water than the buckets, though. That’s diagonal scaling; more resources with a bit more performance in each. 

But then the fire department cranks open the valve on the fire hydrant, and a huge jet of water flies out of the big hose. That’s vertical scaling; increasing resources to a single response unit to increase its performance. 

## Elastic scaling

In cloud computing, you can employ elastic scaling to automatically increase or decrease the number of servers (horizontal) or the resources allocated to existing servers (vertical) or both (multidimensional) based on the current demand. 

Containers can scale down to a fraction of a computer, or scale up to use all the resources of multiple computers. It’s important to decide on the type or types of scaling your application will require in advance so you can make sure to have the right service-level agreement (SLA). Your SLA is the contract with your platform provider; this dictates what will be furnished to you, and at what cost. 

For more details about horizontal and vertical scaling, see ~[Horizontal Vs. Vertical Scaling: How Do They Compare?](https://www.cloudzero.com/blog/horizontal-vs-vertical-scaling)~

For more on the how-to of scaling, see ~[Scaling an application](https://cloud.google.com/kubernetes-engine/docs/how-to/scaling-apps)~. 

For more about horizontal autoscaling, see ~[Horizontal Pod autoscaling](https://cloud.google.com/kubernetes-engine/docs/concepts/horizontalpodautoscaler)~ and ~[Configuring horizontal Pod autoscaling](https://cloud.google.com/kubernetes-engine/docs/how-to/horizontal-pod-autoscaling)~. 

For more on diagonal scaling, see ~[Configure multidimensional Pod autoscaling](https://cloud.google.com/kubernetes-engine/docs/how-to/multidimensional-pod-autoscaling)~.

For a primer on using autoscaling in Google Kubernetes Engine (GKE), see~[Understanding and Combining GKE Autoscaling Strategies](https://www.cloudskillsboost.google/focuses/15636?parent=catalog)~.

## Scaling containers on GCP
Google Cloud Platform (GCP) has massive amounts of computers and components at the ready, so the platform lets you avoid a delayed response to scaling needs. These resources are shared between GCP users, which means you pay less during off hours when your app requires fewer resources. By comparison, if you were running a Kubernetes cluster on-premises, you would pay for electricity for a device that might always be on, regardless of whether it was idle or busy. 

Scaling is also easy to automate using the dashboards in any of GCP’s platforms. These dashboards allow you to set policies and limits. When setting your scaling parameters, be sure to pay attention to the pricing involved with scaling. The base price for a Kubernetes cluster may be a lot lower than the price when it operates at scale. If traffic suddenly takes off for your application, you may be thrilled, but the thrill might be gone when you get the bill. 

Before you choose settings for your scaling,  learn more about the details. 

For more about adjusting capacity for demand and resilience, see ~[Patterns for scalable and resilient apps](https://cloud.google.com/architecture/scalable-and-resilient-apps)~.

For more on instance autoscaling, see~[About instance autoscaling](https://cloud.google.com/run/docs/about-instance-autoscaling)~.

For more about basing your autoscaling needs on metrics, see ~[Autoscale workloads based on metrics](https://cloud.google.com/kubernetes-engine/docs/concepts/custom-and-external-metrics)~.

Last but far from least, learn about pricing as you set limits for your scaling capabilities. For more on this, see ~[Google Kubernetes Engine pricing](https://cloud.google.com/kubernetes-engine/pricing)~. 

## Pro tip
Using **kubectl**, the Kubernetes command line tool, can be intimidating. But once you get used to working with kubectl, it can really streamline your process. It also lets you keep your notes and commands all in one place. 

For a tutorial on how to use the command line to scale containers, see the ~[Autoscaling Deployments](https://cloud.google.com/kubernetes-engine/docs/how-to/scaling-apps#autoscaling-deployments)~ section in this tutorial on ~[Scaling an application](https://cloud.google.com/kubernetes-engine/docs/how-to/scaling-apps)~.  
