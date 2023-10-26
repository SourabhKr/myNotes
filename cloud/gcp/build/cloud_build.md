# Cloud Build

Cloud build is a service that executes builds on google cloud. Cloud build can import source code from different variety of repositories or cloud storage spaces, execute a build and produce artifacts such as Docker containers or Java archives.

A build config can provide instructions to Cloud Build on what tasks to perform. The configures builds can be used to fetch dependencies, run unit tests, static analyses, and integration tests, and create artifacts with build tools such as docker, gradle, maven, bazel, and gulp.

Cloud Build executes build as a series of build steps, where each build step is run in a Docker container. Executing build steps is analogous to executing commands in a script.

There are some already available build steps mentioned below that can be handy to use:

* Google provided common build steps are available here [supported open-source build steps](https://github.com/GoogleCloudPlatform/cloud-builders).
* Community-contributed build steps: The Cloud Build user community has provided open-source [build steps](https://github.com/GoogleCloudPlatform/cloud-builders-community).

Each build step is run with its container attached to a local Docker network named cloudbuild. This allows build steps to communicate with each other and share data

## How builds work

The following steps describe, in general, the lifecycle of a Cloud Build build:

* Prepare the application code and any needed assets.
* Create a build config file in YAML or JSON format, which contains instructions for Cloud Build.
* Submit the build to Cloud Build.
* Cloud Build executes the build based on the build config provided.
* If applicable, any built artifacts are pushed to Artifact Registry.

## Default pools and private pools

By default, the cloud build runs the build in a secure, hosted environment with access to public internet. Each build runs on its own worker and is isolated from other workloads. This can be customized, even changing the default machine configuration, i.e. increasing the cpu, memory. Though the default pool has a limitation on the customization, particularly around the private network access.

**Private Pools** are private, dedicated pools of workers that offer greater customization over the build environment, including the ability to access resources in a private network

## Automate builds by using Cloud Build

Cloud build uses build triggers to enable CI/CD automation. Triggers can be configured to listen for incoming events, such as when a new commit is pushed to a repository or when a pull request is initiated, and then automatically invoke a build when new events come in.

## IAM roles and permissions

Access control in Cloud Build is controlled using Identity and Access Management (IAM). IAM enables you to create and manage permissions for Google Cloud resources. Cloud Build provides a specific set of predefined IAM roles where each role contains a set of permissions. You can use these roles to give more granular access to specific Google Cloud resources and prevent unwanted access to other resources. IAM lets you adopt the security principle of least privilege, so you grant only the necessary access to your resources.

---
Reference:
<https://cloud.google.com/build/docs/overview>
<https://cloud.google.com/build/docs/automate-builds>
<https://cloud.google.com/build/docs/iam-roles-permissions>
