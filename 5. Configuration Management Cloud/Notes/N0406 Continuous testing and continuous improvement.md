# Continuous testing and continuous improvement

You’ve learned about CI/CD, the tools you can use to automate your DevOps processes, and the stages of a CI/CD pipeline. In this reading, you’ll learn about continuous testing and continuous improvement, why they’re important in the CI/CD pipeline, how to measure the effectiveness and efficiency of your CI/CD pipeline, and some tools you can use to detect issues and ensure the quality of your software. 

## Continuous testing

Continuous testing means running automated test suites every time a change is committed to the source code repository. In practice, this usually means running the tests as part of a CI/CD pipeline, in between the build and deploy stages. Continuous testing is an important part of the CI/CD process. It ensures that all of your code changes are tested early in the development process, preventing them from becoming larger, more difficult, time-intensive, and/or more expensive to fix later on.
There are three types of testing that you’ll typically see in the CI/CD pipeline. These include:

* Unit testing
* Integration testing
* System testing 

You use unit testing to test an individual unit within your code—a unit can be a function, module, or set of processes. Unit testing checks that everything is working as expected. 

Integration testing is part of both continuous delivery and continuous deployment. It allows you to automatically test each change to your code when you commit or merge them to your source code repository. The testing  checks for errors and security issues as they arise, again preventing you from having to deal with larger, more difficult, and/or expensive issues later in the process. 

System testing does exactly what it sounds like: It simulates active users and runs on the entire system to test for performance. When testing the entire system, testing for performance can include testing how your program, software, or application handles high loads or stress, changes in the configuration; and system  security. You can also utilize end-to-end testing, which tests the functionality and performance of your entire application from start to finish by simulating a real user scenario.

Testing frameworks and tools

There are many testing frameworks and tools you can use for automated testing, such as [JUnit Opens in a new tab](https://junit.org/junit5/), [Selenium Opens in a new tab](https://www.selenium.dev/), [Cypress Opens in a new tab](https://www.cypress.io/), and [Postman Opens in a new tab](https://www.postman.com/). 

* JUnit is an open-source unit testing framework for the Java programming language and can help you with your unit testing. With JUnit, you can write and execute automated tests and develop reliable, bug-free code. There are similar libraries for other languages such as PyUnit for Python and NUnit for C#.
* Selenium is an open-source, automated testing suite of tools for web application developers. Each tool can be used for different testing needs.
* Cypress is a JavaScript-based testing tool that can automate end-to-end tests. It simulates how users would interact with your web applications. Often used for front-end development of web-based applications, these kinds of tests will help to ensure that your tests and the users’ experiences are the same. 
* Postman can be used to automate unit tests, function tests, integration tests, end-to-end tests, regression tests, and more in your CI/CD pipeline.  

## Continuous improvement

Continuous improvement is a crucial part of the DevOps mindset. It’s the idea that every team should constantly be on the lookout for ways to improve their efficiency and reduce errors and bottlenecks. Think of continuous improvement like compounding interest—it starts out small, but slowly increases over time, resulting in a better product for consumers. 

Continuous improvement requires investing the time and resources necessary to improve the entire process of developing and deploying software. It also requires commitment from your organization’s leadership to allow that investment when they may be considering other priorities.

Key benefits of continuous improvement include:

* Increased productivity and efficiency
* Improved quality of products and services
* Reduced waste
* Competitive products and services
* Increased innovation
* Increased employee engagement 
* Reduced employee turnover

The benefits don’t stop there! The benefits of continuous improvement can accumulate and improve your organization’s processes, efficiency, and profitability overall. It’s in your, and your organization's, best interest to invest in continuous improvement.

## Key performance indicators (KPIs)

Key performance indicators, or KPIs, are quantifiable measurements of performance. These metrics are data points that can tell you how your DevOps CI/CD pipeline is performing and help you identify if there are any errors or bottlenecks in the process. Metrics can track and measure workflows and the progress of your projects and goals, which can lead to improved software or application quality and performance. There are many metrics you can use in DevOps, so it’s important to choose the ones that work best for your project and workflows—just like the tools you use for CI/CD. Popular metrics in DevOps that you can use to measure performance include:

* Lead time for changes: This is the length of time it takes for a code change to be committed to a branch and be in a deployable state.
* Change failure rate: This is the percentage of code changes that lead to failures and require fixing after they reach production or are released to end-users.
* Deployment frequency: This measures the frequency of how often new code is deployed into production.
* Mean time to recovery: This measures how long it takes to recover from a partial service interruption or total failure of your product or system. 

## Key takeaways

Making high-quality tests part of your CI/CD pipeline is critical to your DevOps success. The more complete your test suite is, the earlier you will be able to catch bugs and squash them. If you’re going to deploy your code as soon as it’s committed, you want to have the utmost confidence that everything will work together in production. The more tests you are able to run before deployment—unit tests, integration and smoke tests, load tests—the more confident you can be. 

Pro tip #1: Take the time to learn how to write good tests. There are tools available that will analyze your code and estimate how complete your test coverage is. You should aim for 100% coverage. 

Pro tip #2: Test engineering is a highly skilled and sought-after discipline. Becoming a passionate advocate for DevOps and continuous improvement can make you highly visible and valuable in many organizations. For more information, visit IT automation job opportunities and SRE job opportunities.  
