# Example pipeline

You’ve learned about CI/CD: continuous integration and continuous delivery or continuous deployment, which is the automation of an entire pipeline of tools that build, test, package, and deploy an application whenever a developer commits, or saves, a code change to the source control repository. You’ve also learned about DevOps, the stages of the software development lifecycle, and the DevOps tools that can help you automate the processes in CI/CD.  In this reading, you’ll learn about pipelines, which are the steps necessary to build, test, and (optionally) deploy software. 

## Pipelines

Pipelines are automated processes and sets of tools that developers use during the software development lifecycle. In a pipeline, the steps of a process are carried out in sequential order. This way, if any step fails, the pipeline stops without deploying the changes.

Consider the following example: A pipeline for a Python application is triggered when a pull request is ready to be merged. That pipeline can perform the following steps:

1.	Check out the complete branch represented by the pull request.
	
2.	Attempt to build the project by running python **setup.py build**.

3.	Run unit tests with **pytest**.

4.	Run integration tests against other parts of the application with a framework like **playwright**.

5.	Build the documentation and upload it to an internal wiki.

6.	Upload the build artifacts to a container registry.

7.	Message your team in Slack to let them know the build was successful.

The advantage to automating the CI/CD process is there’s much less manual work and coordination required to deploy software, and this saves a tremendous amount of time and effort for your development and operations teams. 

Pro tip: The more teams you have working independently, the greater the advantage.

## Example pipeline

Now imagine you’re part of an organization with many development teams that are working independently but still contributing to the larger application or project. In order to deploy an application successfully, your organization has to:

1.	Choose a “release day” when all the code will be merged together.

2.	Restrict  new code commits until the release is complete, to avoid conflicts.

3.	Run integration tests (and maybe performance tests). 

4.	Prepare the deployment.

5.	Notify customers of an upcoming maintenance window. 

6.	Manually deploy the application and any other updates.

Without automating any (or all) of these steps, the entire process is painful and subject to human error. As a result, many organizations release updates infrequently, e.g., once every few weeks or even months. Imagine the disruption and chaos of “release day” or even “release week” within those organizations! The developers cannot commit any new code, and the operations teams scramble to package and deploy dozens of microservices and other components to meet a deadline. 

This is when having a pipeline to automate some or all of the processes during CI/CD comes in handy. By creating a CI pipeline, the process looks very different:
	
1.	Developers commit code to the repository as soon as they’re done.

2.	The CI server observes the commit and automatically triggers a build pipeline.

3.	If the build completes successfully, the CI server runs all the unit tests. If any tests fail, the build stops.

4.	The CI server runs integration tests and/or smoke tests, if any.

5.	Assuming the previous steps all complete successfully, the CI server signals success. Then, the application is ready to be deployed.

6.	If the CD process has also been automated, the code is deployed to production servers. 

You can have multiple pipelines run at once, which enables teams across your organization to commit code whenever they’re ready. If you’ve also automated the deployment process (CD), code can be deployed to production without waiting for every other team to prepare for “release day.” Some CD pipelines even continue to monitor production for errors, rolling back the deployment if it detects an increase.

Organizations that have high-quality CI/CD pipelines often deploy to production every day, sometimes dozens of times a day, as individual teams release code. The automation of these processes is more efficient, saves you time, and reduces human error. It also provides a better end-product for consumers. 

It’s important to note that none of this works with any confidence unless your code has high-quality automated tests. If your project is part of a largely distributed application, it’s also important to have good integration tests. Otherwise, your changes that aren’t caught during the pipeline can cause problems for other components that are then deployed to production unchecked, causing an outage.

## Key takeaways

Pipelines are the sets of tools and automated processes that development and operations teams use to build, test, and (optionally) deploy software. The automation of the CI/CD pipeline can reduce the amount of manual work and coordination required to deploy software, save time and effort for your development and operations teams, and allow you and your organization to release any updates more efficiently. In order for your CI/CD pipelines to be successful, make sure you have included high-quality tests for automation, integration, and deployment. Finally, pipelines allow your organization to have multiple teams working independently, accelerate software development and deployment cycles, enhance the quality and stability of your software releases, and create a faster, more efficient review and resolution process, which also reduces the number of errors.
