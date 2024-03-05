# Configuration management

Image this: You just got a new job as a system engineer to develop a new software product. As you begin to write code for the product, you change and update it continuously to correct any issues found. You use configuration management to optimize your IT responsibilities, creating a more efficient workflow. 

Configuration management is an automated process that ensures your new software project and its assets perform as they should as you update and change your code.

In this reading, you will learn more about configuration management, its role in maintaining consistency and stability, and how to use configuration files to describe desired system states.

## Consistency and stability

Configuration management helps you manage your code and all of its components. In addition, it ensures that each component of your code is automatically and properly built, monitored, and updated as needed. It’s common to have multiple copies of an application running at the same time to guarantee a highly available, properly functioning system.

If configuration management is not used, a developer will have to manually update and correct any issues or errors on each individual server. Something as simple as a typo could create misconfigured servers, causing errors and unexpected behaviors. The developer would have to correct each typo on each server. This process would be frustrating and unsustainable. That’s where configuration management plays a role in maintaining consistency and stability in software systems. It enables you to duplicate server instances, resulting in consistent behavior across all servers.

## Configuration files

Configuration files are commonly referred to as a manifest or playbook—depending on the DevOps tool you use. You can think of these as statements on how you want the system to look and perform. Let’s take a look at an example. A playbook might say, “I need a server with 32GB of RAM running Debian Linux, with Python 3.9 and Nginx installed.” Notice that this playbook statement does not specify the steps to achieve the desired state—it only describes what the desired state should look like. To use configuration files, create a configuration file as the input to your configuration management tool describing the desired state. The configuration management tool works to determine a solution to have the server look and perform as you described in your manifest or playbook.

Pro tip: Store configuration management files alongside the application code in your revision control system, allowing changes to be tracked and audited.

## Key takeaways

Configuration management provides developers a solution to simplify and effectively manage changes and updates to codes. It streamlines the process of correcting any issues or errors found on multiple copies of the same application. It operates off of configuration files—manifests or playbooks—to understand what the desired state of the system should be and determine a solution to achieve the desired state.
