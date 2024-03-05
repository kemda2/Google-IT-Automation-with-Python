# IT skills in action

Congratulations! You have gained so much knowledge on continuous integration and continuous deployment (CI/CD). There are many technical pieces that are included within CI/CD, but how would you apply the skills you learned in a professional setting?

In this reading, you will review an example of how Docker containers are used in the real world.

## The background

Disclaimer: The following scenario is based on a fictitious company.

The Quick Tech Solution Company decided that it is time to rebuild their outdated application into a modern microservice-based architecture with a web frontend. The different development teams knew this was a brilliant—and much needed—idea, so they began to decompose their specific parts of the application into simple microservices in different languages, including Python, Go, and Java. There was very little communication across teams, and each team was unaware of what languages the other teams were using. In addition to using different languages, each team had their own unique process of building and deploying their code to a server. No team worked in the same way.

## The nightmare

Soon enough, this became the DevOps team’s worst nightmare. There was no consistency in the build process, whatsoever. Because of this, when errors were caught, they had to be sent back to the development team to be corrected. Due to a lack of automation, integration tests would take weeks to complete and releases to production were error prone and infrequent. Nothing was running smoothly. They needed a solution, and they needed it fast.

## The solution

The engineering leaders determined that a modern microservice application requires a modern CI/CD solution. Here’s what the solution looked like:

First, The DevOps team evaluated various CI/CD tools and chose the ones that best fit their workflow. Then, each development team was required to add a Dockerfile to their repository. This was used to build their component as a container and provided unit tests and integration tests. DevOps made the decision to leverage Kubernetes for orchestrating all the containers and worked with each development team to write deployment manifests in YAML for each component. After the deployment manifests were written, the DevOps team designed a CI/CD pipeline whose purpose was to build containers, deploy them to a fresh—but temporary—Kubernetes cluster using the manifests, and run all of the unit and integration tests.

## The aftermath

This gave the DevOps team more confidence in what they built. When these tasks were completed, the DevOps team extended the pipeline so every successful pull request would deploy the containers to the production Kubernetes cluster.
