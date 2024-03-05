# Continuous integration, delivery, and deployment

Continuous integration, delivery, and deployment, or CI/CD, refers to the automation of an entire pipeline of tools that build, test, package, and deploy an application whenever a developer commits a code change to the source control repository. 

Continuous integration (CI) automatically builds, tests, and integrates code changes within a shared repository. Then, continuous delivery (CD) automatically delivers code changes to production-ready environments for approval, and continuous deployment (CD) automatically deploys those code changes directly to production. 

## Continuous integration

CI is a key best practice in DevOps. As the first stage of the automation process in the development lifecycle, developers integrate their code changes early and often to a shared source code repository. This shared repository is the solution to having too many separate iterations of a software or app in development at the same time. It can also: 
* Reduce the risk of having multiple pieces—which may be created independently—conflicting with each other 
* Save time throughout the development lifecycle by allowing you to identify and address any issues or conflicts as they arise rather than at the end of a phase
* Reduce the amount of time spent on fixing bugs and regression

![IMG_9916](https://github.com/kemda2/Google-Courses/assets/19648132/d5986653-5e01-46a2-b7fc-caf5c33f61c8)

![IMG_9917](https://github.com/kemda2/Google-Courses/assets/19648132/67eb7387-c557-4bb6-a29c-5ce74ee0e960)

![IMG_9918](https://github.com/kemda2/Google-Courses/assets/19648132/0cce39f3-2635-49da-943a-9de35aacd37b)

![IMG_9919](https://github.com/kemda2/Google-Courses/assets/19648132/9f108a37-d9d0-426c-892c-f768466f598f)

## Continuous delivery and deployment

An important note: Continuous delivery and continuous deployment are related concepts that are sometimes used interchangeably. While they’re both about automating later stages of a DevOps pipeline, you can use either to show what is happening during automation. For example, continuous delivery means that any changes a developer makes to an application are automatically released to a repository like GitHub and then deployed by the operations team. This ensures that minimal effort is required to deploy new code. It also includes test and code release automation at every stage, beginning with code changes and ending with the delivery of production-ready builds.

Continuous deployment is an extension of continuous delivery and refers to the automatic deployment of an app or any developer changes from the repository to production. This helps to prevent overloading the operations teams and automates the next stage in the pipeline. However, continuous deployment relies heavily on the success of test automation, so it’s important that your testing is written to accommodate the various testing and release stages in the DevOps lifecycle. 

![IMG_9920](https://github.com/kemda2/Google-Courses/assets/19648132/3fb2a7e9-da64-4978-abee-482e0cf7e681)

steps begin with build, test, and merge, in continuous integration, then move to “automatically release to repository” in continuous delivery, and then end with, “automatically deploy to production” in continuous deployment.
