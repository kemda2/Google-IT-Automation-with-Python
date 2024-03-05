# CI testing

You’ve learned that continuous testing means running automated test suites every time a change is committed to the source code repository. In practice, this usually means running the tests as part of a CI/CD pipeline, in between the build and deploy stages. 

In this reading, you’ll learn about continuous integration (CI) testing: why it’s important, what tools you can use, and how to test different types of applications, like the web, a database, or a microservice. 

## Integration testing

Continuous integration is when developers integrate code into a shared repository frequently. Benefits of continuous integration include revision control, build automation, and automated testing which allows you to detect errors quickly and locate them more easily. Integration tests are tests you conduct to make sure different parts of the application work together, like modules or services, as opposed to individual units of code. They’re one type of test that is typically run during the CI pipeline. The purpose of integration testing is to make sure that any recent changes you or your team has made haven’t broken other parts of the system and to verify that everything is working together as expected. A few benefits of CI testing include repeatability of your testing, continuous integration and testing, the ability to run builds or tests in parallel with other team members, and rapid feedback. 

There are different types of CI tests that you can perform in the CI pipeline:
* Code quality tests are used to check the quality and complexity of your code(s) and identify if there are any code defects. 
* Unit tests which are used to test an individual unit within your code, like a function, module, or set of processes. Unit testing checks that everything is working as expected.
* Integration tests are used to verify that the different modules or parts of your application are working together.
* Security or license tests are used to make sure that your software or application is free from threats, vulnerabilities, and risks. This allows developers to identify if and where there are security risks so they can be fixed earlier rather than later. 

You’ve learned the different kinds of CI tests you can perform, but what about the tools you can use to run the tests? 
* If you want to test the integrations between web services, you can use a programming framework like PyTest or its equivalent (if the app you’re using is Python). 
* If you want to test a browser-based app or site, you can use a framework like Selenium or Playwright to load the web pages and test functionality.

Refer to Continuous testing and continuous improvement for more information on the tools you can use to run integration tests. 

After you’ve chosen the CI tool that fits your needs, it can run the designated tests and halt the deployment of your software or application if some or any of the tests fail. There are also “code coverage” tools that will scan your code for you and tell you if it appears you’ve missed anything in your test suite.

## End-to-end testing

Integration testing verifies that the components of your application are working together as intended and usually occurs in the CI pipeline. End-to-end (E2E) testing is similar. Although it occurs in the CD pipeline, it is used to test the functionality and performance of your entire application from start to finish by simulating a real user scenario. The objective of E2E testing is to identify any errors or bugs that appear when all of your components have been integrated, so you know if the entire application operates as it should. You can gain insights into how end users are experiencing your application, giving you a better understanding of the quality of your product before it’s deployed. 

## Key takeaways

Continuous integration testing is used to test different components of your application throughout the CI pipeline. It allows you to verify that any code changes made by developers working independently haven’t created errors or broken other parts of the system. Continuous integration testing can also lead to continuous testing, allowing you to automate different processes along the CI/CD pipeline.

It’s important to note that if you’re going to automate the entire process of deploying your code to production, you’ll want to significantly reduce the risk that the changes you make will break the production system. It will be up to you and your team to weigh the risk/reward ratio of whether you want to perform less testing and quickly make changes to the production system or perform more testing and delay changes to the production system. There is no “one-size-fits-all” solution for all systems, so choose the tests and the tools that make the most sense for your project.
