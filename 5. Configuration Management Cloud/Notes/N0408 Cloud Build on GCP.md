# Cloud Build on GCP

Cloud Build is a fully managed continuous integration and continuous delivery (CI/CD) service provided by GCP. It allows developers to automate the process of building, testing, and deploying applications or code changes to various environments.

In this reading, you will learn more about the components that make up Cloud Build, the benefits of using Cloud Build, and integration capabilities of Cloud Build with GCP and Github repositories.

## Components

The core components of Cloud Build include:

* Build triggers
* Build configurations
* Build steps

Build triggers are the events that initiate the Cloud Build process. They define when and under what conditions a build should be triggered. Cloud Build supports various types of build triggers, including:

* Push trigger: This initiates a build when code changes are pushed to a specific branch of a version control repository like Github.
* Tag trigger: This triggers a build when a new tag is applied to the repository.
* Pull request trigger: This automatically starts a build when a pull request is opened, allowing you to run tests and checks before merging code changes.
* Scheduled trigger: This defines a specific time or schedule when the build should be triggered, enabling regular builds.

Build configurations are YAML files that define the build steps, environment variables, and other settings for a build. The build configuration file is typically named cloudbuild.yaml and is placed in the root of the repository. It includes information on steps, substitutions, timeouts, and artifacts.

Build steps are individual actions that Cloud Build executes in sequence according to the build configuration. Each step can run commands or scripts and the steps are executed in the order they are listed. Let’s look at an example. A typical build configuration might include the following build steps:

1. Fetching dependencies: The first step pulls in the required libraries and dependencies for the application.
2. Building the application: This step compiles the code and creates the application binaries.
3. Running tests: This step executes unit tests or other types of tests to ensure code quality.
4. Deploying: The last step deploys the application to a specified environment like staging or production.

## Benefits

Using Cloud Build for CI/CD workflows offers a number of benefits, including: speed, scalability, and seamless integrations with other GCP services. 

Cloud Build is a fully managed service, meaning you do not need to worry about infrastructure setup and maintenance. It automatically scales resources based on your build requirements, allowing you to run multiple builds in parallel, reducing build times and increasing overall development velocity, speed, and efficiency.

Cloud Build's ability to scale automatically means it can handle builds of any size, from small projects to large-scale applications. As your development needs grow, Cloud Build can accommodate the increased workload without manual intervention, ensuring that your CI/CD process remains smooth and efficient.

As part of the GCP ecosystem, Cloud Build seamlessly integrates with other GCP services, making it easy to incorporate different stages of the CI/CD workflow into your projects. Integrations include:

* [Source repository Opens in a new tab](https://cloud.google.com/source-repositories/docs)
* [Artifact registry Opens in a new tab](https://cloud.google.com/artifact-registry/docs/configure-cloud-build)
* [Cloud deployment manager Opens in a new tab](https://cloud.google.com/deployment-manager/docs)
* [Kubernetes Engine \(GKE\) Opens in a new tab](https://cloud.google.com/build/docs/deploying-builds/deploy-gke)

## Integration capabilities

Cloud Build offers integration capabilities with both GitHub and Google Cloud Source Repositories, making it easy to set up CI/CD workflows for projects hosted in either of these version control systems. While the overall integration approach is similar, there are some differences based on the version control system being used.

Cloud Build integrates seamlessly with GitHub repositories, allowing you to trigger builds automatically whenever code changes are pushed to specific branches or when pull requests are created. The integration steps for Github include:

1. Install the GitHub app.
   1. Open the Repositories page in the Google Cloud console. You will see the Repositories page.
   2. In the project selector in the top bar, select your Google Cloud project.
   3. Select Create host connection to connect a new host to Cloud Build.
   4. On the left panel, select GitHub as your source provider.
   5. In the Configure Connection section, enter the following information:
      1. Region: Select a region for your connection. A region must be specified. Your connection cannot exist globally.
      2. Name: Enter a name for your connection.
   6. Select Connect. After you select the Connect button, you will be asked to authorize the Cloud Build GitHub App to access your GitHub account. You may revoke access to the app by uninstalling or deleting the App from your host at any time.
2. Provide repository authentication.
3. Determine Cloud Build configuration.
4. Observe automatic triggering.

Since Google Cloud Build is a part of GCP, it naturally integrates with Google Cloud Source Repositories (GCSR). GCSR is a fully featured, private Git repository hosting service provided by Google Cloud. The integration process is more streamlined compared to GitHub. There is no need for additional authentication or setup. Cloud Build automatically has access to your GCSR repositories since both are part of GCP. The integration between Cloud Build and Google Cloud Source Repositories allows you to set up build triggers and use cloudbuild.yamlconfiguration files in your GCSR-hosted repositories, just like you would with GitHub. Since both services are part of GCP, you get enhanced visibility and monitoring capabilities when using Cloud Build with Google Cloud Source Repositories. You can view build logs, track build history, and access other GCP-specific features easily.

## Key takeaways

Cloud Build’s core components streamline the software development process, enabling teams to achieve faster, automated, and more reliable application deployments. Cloud Build provides a robust and efficient CI/CD solution with automatic scaling, seamless GCP integrations, and cost-effectiveness. The integration capabilities of Cloud Build with GitHub and Google Cloud Source Repositories share the same core functionalities, allowing you to define build triggers, configure build steps, and leverage the power of Cloud Build's CI/CD service.
