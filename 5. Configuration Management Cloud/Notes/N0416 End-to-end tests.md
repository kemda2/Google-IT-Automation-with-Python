# End-to-end tests

End-to-end testing or E2E testing involves testing of a complete application environment in a scenario that mimics real-world use, such as interacting with a database, using network communications, or interacting with other hardware, applications, or systems. Unlike unit testing or integration testing, E2E testing is a comprehensive evaluation.

## Scope and objectives

E2E testing covers:
* User experience: Ensuring the system behaves as expected and delivers the right user experience from front-end UI interactions to back-end database operations
* Integration and communication: Validating the interaction between different system components, such as databases, network protocols, and other interfacing systems
* Data flow: Checking the data integrity between different system components. It ensures that data is correctly sent, received, and processed.

For example, imagine your team develops a coffee-and-music app with social media features. A typical user journey involves creating an account, logging in, choosing a coffee, selecting music, interacting with other users, and logging out. To conduct an E2E test, your team would identify all the main user journeys (from account creation to logging out) and create a detailed test case for each journey that includes the expected outcomes.

One of the key objectives of E2E testing is the opportunity to simulate critical user journeys or the real-world user scenarios. The journeys usually cover essential user flows like account creation, log-in, placing an order, or making a payment. In addition, the E2E testing allows you to verify if business processes are working as expected. For example, if a user places an order, it should trigger a series of events like payment processing, order confirmation, and dispatch details. 

## Tools for end-to-end tests

You can use testing frameworks such as Selenium and Puppeteer to conduct an E2E testing. Most of these UI testing frameworks target web applications and they tend to be JavaScript-based as web apps almost always use HTML+JavaScript (react.js, angular, vue.js) for their user interface components. For Python developers, when you utilize these frameworks, you will need to use Flask or Django. Flask is commonly used to build web apps and it can handle microservices. Django is used for larger or more complex applications. 

Here are some of the testing tools you can use with Flask and Django:
* [Selenium  Opens in a new tab](https://www.selenium.dev/documentation/test_practices/overview/) is a popular open-source tool that allows for automated testing across various platforms and browsers. It supports multiple programming languages like Java, C#, and Python.
* [Puppeteer  Opens in a new tab](https://pptr.dev/guides/query-selectors) is a Node library that provides a high-level API to control Chrome or Chromium over the DevTools Protocol. It can be used for testing Chrome extensions and for generating screenshots and PDFs of pages.
* [Cypress  Opens in a new tab](https://docs.cypress.io/guides/end-to-end-testing/writing-your-first-end-to-end-test) is a JavaScript-based testing framework that doesn't use Selenium. It allows you to write all types of tests: E2E tests, integration tests, and unit tests. However, Cypress doesn’t support Python.
* [Appium  Opens in a new tab](https://appium.io/docs/en/2.0/quickstart/) is an open-source tool for automating native, mobile web, and hybrid applications on iOS mobile, Android mobile, and Windows desktop platforms. It's widely used for end-to-end testing of mobile applications.
* [Protractor  Opens in a new tab](https://www.protractortest.org/#/tutorial) is an end-to-end test framework for Angular and AngularJS applications. It runs tests against your application running in a real browser, interacting with it as a user would.

## Key takeaways

End-to-end testing is a comprehensive evaluation that includes testing of a complete application environment using real-world user scenarios. Its scope includes the testing of user experience, integration and communication, and data flow. Python users can use testing tools and frameworks such as Selenium. But keep in mind that these tools require Flask or Django.
