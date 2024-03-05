# CI best practices

Continuous integration (CI) is a software development practice in which code changes occur automatically, frequently, and safely to integrate into a shared repository. With each integration, an automated build is triggered and tested to determine and resolve integration issues early.

## Principles and benefits

Key principles of CI include:
* Integration
* Builds
* Tests
* Feedback
* Version control

CI allows for frequent integration, as developers commit their changes to a shared repository daily. It also ensures the changes are tested and issues are resolved. CI relies on automation to build the application code and execute tests to manage integrated changes and to ensure consistent results. Because CI is able to detect integration issues early, this allows for CI to provide quick feedback to developers, alerting them of issues and providing time to allow them to correct any problems. Lastly, running the CI tests on every pull request will highlight which changes caused the tests to fail, guaranteeing a reliable history of the codebase for developers.

Let’s look at an example of where you’d see this in the real world: Imagine that a team working on a modern microservice-based application has been suffering and exhausted due to subtle errors showing up in production that should have been caught earlier. The team makes the decision to invest time and resources into building a strong set of integration tests.

After the unit tests run successfully, the team prepares the CI server to deploy all the microservices into a Kubernetes cluster and run the automated integrated test suite. Each microservice developer writes tests to check the interactions between their service and the other services it depends on. If any of those tests fail, the pull request is not merged and the code is not deployed to production.

## Core practices

CI is a way to develop software to make it easier, faster, and more reliable. CI is composed of three core practices, which include:
* Automated building
* Automated testing
* Version control system integration

Automated builds involve utilizing tools and scripts to automatically compile the source code into executable binaries or artifacts. Automated testing involves running different types of tests automatically to verify the stability of code changes made by developers, providing fast feedback to developers on any issues. Version control system integration allows a way to manage and track code changes efficiently and effectively.

## Key takeaways

Continuous integration enables faster feedback, higher quality software, and a lower risk of bugs and conflicts in your code. CI is a way for developers to ensure that their code is always up to date and ready to deploy. CI ensures that reliable software is getting into the hands of users
