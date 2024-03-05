# Github and delivery

GitHub can facilitate your efforts in Continuous Integration and Continuous Delivery (CI/CD). Learning about how to utilize this repository will benefit you down the road.

## How GitHub supports CI/CD

GitHub supports external CI/CD tools by providing webhooks and APIs that allow those tools to become part of the pull request process. For example, GitHub can be set up to refuse to merge a pull request until several actions are completed:

* The PR is reviewed and signed off by one or more code reviewers.
* The CI build process completes successfully.
* The CI test suites run successfully.
* The PR submitter has acknowledged the project’s license, standards, and/or code of conduct.

The feature of GitHub that automates CI/CD is called GitHub Actions.

## GitHub Actions

GitHub Actions is a feature of GitHub that allows you to run tasks whenever certain events occur in your code repository. With GitHub Actions, you are able to trigger any part of a CI/CD pipeline off any webhook on GitHub. 

To get started with GitHub Actions, go to the Actions tab in the GitHub repository. When opening the tab for the first time, you’ll find a description of GitHub Actions and some suggested workflows for your repository. These workflows build the code in your repository and run your tests either on GitHub-hosted virtual machines or on your own machines. You’ll receive the results of the tests in the pull request.

GitHub Actions has more than 13,000 pre-written and tested CI/CD workflows. If you would like to write your own workflows or customize an existing one, you can do it using YAML files. 

Because GitHub Actions is a general-purpose engine that runs tasks in response to events in the repository, you can use it for more than just CI/CD pipelines. Some examples:

* Running a nightly build in the master branch for testing.
* Cleaning up old issues or bug reports.
* Creating a full-fledged bot that responds to comments or commands on a PR or issue. (“Issues” are like bug reports or support tickets.)

## Key takeaways

GitHub Actions supports your CI/CD. It offers workflows that you can use right away or customize for your own repository. 

## Resources for more information

* [GitHub Actions documentation - GitHub Docs Opens in a new tab](https://docs.github.com/en/actions)
* [A beginner’s guide to CI/CD and automation on GitHub - The GitHub Blog Opens in a new tab](https://github.blog/2022-06-03-a-beginners-guide-to-ci-cd-and-automation-on-github/)
* [GitHub Protips: Tips, tricks, hacks, and secrets from Jason Etcovitch - The GitHub Blog](https://github.blog/2020-04-16-github-protips-tips-tricks-hacks-and-secrets-from-jason-etcovitch/)
