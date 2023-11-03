# Overview

GitHub Actions is a continuous integration and continuous delivery platform that allows to automate build, test and deploy pipelines. 

Github Actions goes beyond just DevOps and allows workflows to be triggered when other events happens in the repository. For example, adding a tag to a PR based on some comments.


## GitHub Action Component

#### 1. Workflows

A workflow is a configurable automated process which runs one or more jobs. Workflows are defined in YAML, checked in the repository and wil be triggered on a event, can be scheduled or triggered manually. 

Workflows are defined in the `.github/workflows` folder in a repository and can contains different types of tasks.

A workflow can refer different workflows.

#### 2. Events

An event is a specific activity in the repository, like a creation of a pull request, pushing a commit to the repository or creating an issue. Events can be used to trigger a workflow. 


#### 3. Jobs

A job is a set of steps in a workflow that is executed on the same runner. Each step is either a shell script that will be executed, or an action that will be run. Steps are executed in order and are dependent on each other. Since each step is executed on the same runner, data can be shared from one step to another. 

Jobs can also have dependency between each other; by default, jobs have no dependencies and run in parallel with each other. When a job takes a dependency on another job, it will wait for the dependent job to complete before it can run. For example, multiple build jobs for different architectures that have no dependencies, and a packaging job that is dependent on those jobs. The build jobs will run in parallel, and when they have all completed successfully, the packaging job will run.

#### 4. Actions

An action is a custom application for the GitHub Actions platform that performs a complex but frequently repeated task. For example: Pulling the repository from GitHub, setup the correct tool chain for the build environment. 


#### 5. Runners

A runner is the server that runs the workflow when triggered. Each runner can run single job at a time. Each workflow run executes in a fresh, newly-provisioned virtual machine. 


