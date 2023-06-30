# IaC (What is IaC?)

Infrastructure as Code means using code to define, deploy, update and destroy infrastructure.
Software practices enabled by IaC:

* Self Service: Automated workflows allow self service deployment without being dependent on anyone.
* Speed and Safety:  Automated process would be much faster and safe having the features of consistent, more repeatable and not prone to manual error.
* Documentation: Code can explain why instead of people knowing what was developed.
* Version Control
* Validation: Code review and automated testing can reduce defects.
* Reuse

### Why do we use IaC?

IaC is an essential tool in the DevOps area. It brings software best practices to infrastructure management, by thinking infrastructure as a set of configurations. It solves the problem of deployment and Snowflake servers (Snowflake servers: All the different environments (prod, stage, dev) being bit different in the configuration then each other (the problem being called configuration drift) exactly like snowflake which looks almost the same but none are exactly same).

### Configuration Management Tools

Chef, Puppet, and Ansible are all configuration management tools, which means that they are designed to install and manage software on existing servers.

Advantages:

1. Coding conventions
2. Idempotence (Code that works correctly no matter how many times you run it is called idempotent code.)
3. Distribution (Managing multiple servers with single configuration)

### Server Templating Tools

Instead of launching a bunch of servers and configuring them by running the same code on each one, the idea behind server templating tools is to create an image of a server that captures a fully self-contained “snapshot” of the operating system (OS), the software, the files, and all other relevant details. Then this image is used by a different IaC tool to be installed on the servers.

### Orchestration Tools

Orchestration tools manages VMs. Following are the tasks taken care by the Orchestration Tools:

* Deploy VMs and containers, making efficient use of hardware.
* Roll out updates to an existing fleet of VMs and containers using strategies such as rolling deployment, blue-green deployment, and canary deployment.
* Monitor the health of your VMs and containers and automatically replace unhealthy ones (auto healing).
* Scale the number of VMs and containers up or down in response to load (auto scaling). Distribute traffic across your VMs and containers (load balancing).
* Allow your VMs and containers to find and talk to one another over the network (service discovery).

### Provisioning Tools

Whereas configuration management, server templating, and orchestration tools define the code that runs on each server, provisioning tools such as Terraform, CloudFormation, OpenStack Heat, and Pulumi are responsible for creating the servers themselves.
