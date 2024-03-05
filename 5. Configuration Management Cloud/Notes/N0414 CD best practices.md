# CD best practices

At this point, we have covered that Continuous Delivery and Continuous Deployment are at the heart of iterative development. The core principles of Continuous Deployment (CD) are:
* Automation: The entire process must be automated so that results are repeatable and consistent.
* Version control: CD configuration and scripts must be stored in your version control system and treated just like code.
* Monitoring: Monitoring the deployed application is essential so that you can confirm the app is working properly after deployment.
* Pairing: CD must be paired with CI and automated testing. Deployment should proceed automatically once tests have completed successfully.

The key of CD is automation. Automation not only reduces errors but also saves you time. As much as you can, automate everything from testing to releasing.

## Feature flags

Feature flags are also called feature toggles, release toggles, or feature flippers. The idea behind feature flags is that new features or application behaviors can be hidden and turned on when you’re ready to introduce them to users. Feature flags can often be set on a per-user or per-role basis. As you might already know, “ready to be deployed” isn’t always the same as “ready for users to see.”
For example, when you’re deploying a major new feature in an application. You may create a feature flag and turn it off for everyone. In your code, you check the flag before allowing the new feature to be used. Now, you can do the following:
* Allow the new code to be built, tested, and deployed to production. Because the flag is turned off, no one sees the new feature.
* Turn the flag on for a specific group of internal testers. 
* If all goes well, you can turn the flag on for a larger group of early adopters or beta testers to gather their feedback.
* Once all the bugs are fixed and feedback has been incorporated, you can turn the flag on for everyone.

## Incremental rollout

Incremental rollout means to slowly deploy changes throughout your infrastructure so that you can monitor for trouble and quickly roll back the deployment if there’s a problem. The practices that are associated with the incremental rollout are canary releases and blue-green deployments.

Canary releases and blue-green deployments
Both of these are extensions of the concept of incremental rollout. You deploy changes to a portion of your infrastructure or user base. You can then use a variety of monitoring tools to observe any changes in key metrics such as error rate, user engagement, feedback scores, etc. and compare those against the rest of the population.

The difference between the two is that a canary release is often targeted at a specific population of testers or early adopters, whereas a blue-green deployment will send X% of randomly selected users to the blue or green servers.

A canary release can be used to closely observe and gather feedback from a small group of users before unleashing a new release on everyone. If the feedback is negative, or the canary group experiences issues with the new release, you can halt further deployment and fix the issues before deploying everywhere.

With a blue-green deployment, you can use automated monitoring to observe any differences between the blue and green populations. If there is a problem, you can instantly shut off traffic to the blue or green side and direct all user traffic to the other side until the problem is fixed.

## Key takeaways

CD must be paired with CI and automated testing. The CD practices of using feature flags, incremental rollout, canary releases, and blue-green deployments will minimize problems that often are caused by human errors.

## Resources for more information

* ~[8 Key Continuous Delivery Principles | Atlassian Opens in a new tab](https://www.atlassian.com/continuous-delivery/principles)~
* ~[The Fundamentals of Continuous Deployment in DevOps - GitHub Resources Opens in a new tab](https://resources.github.com/devops/fundamentals/ci-cd/deployment/)~
* ~[Continuous Deployment - Scaled Agile Framework Opens in a new tab](https://scaledagileframework.com/continuous-deployment/)~
* ~[Feature Flags—What Are Those? Uses, Benefits & Best Practices | LaunchDarkly Opens in a new tab](https://launchdarkly.com/blog/what-are-feature-flags/)~
* ~[Incremental rollouts with GitLab CI/CD | GitLab Opens in a new tab](https://docs.gitlab.com/ee/ci/environments/incremental_rollouts.html)~
* ~[A Comprehensive Guide to Canary Releases | by Daniel Bryant | Ambassador Labs \(getambassador.io\) Opens in a new tab](https://blog.getambassador.io/cloud-native-patterns-canary-release-1cb8f82d371a)~
* ~[What is the Canary Deployment & Release Process? – BMC Software | Blogs Opens in a new tab](https://www.bmc.com/blogs/canary-deployment-release/)~
* ~[A Comprehensive Guide to Canary Releases | by Daniel Bryant | Ambassador Labs \(getambassador.io\) Opens in a new tab](https://blog.getambassador.io/cloud-native-patterns-canary-release-1cb8f82d371a)~
* ~[Using blue-green deployment to reduce downtime | Cloud Foundry Docs](https://docs.cloudfoundry.org/devguide/deploy-apps/blue-green.html)~
