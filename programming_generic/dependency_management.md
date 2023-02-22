# What is dependency management?

Dependency management refers to managing all software components, a piece of software/script requires to function. Resolving dependencies can happen while  compiling code, building, running, downloading, or installing a software.

Dependencies can be of two types.

1. Direct Dependency: Software components which the code directly references, for example importing a specific library to the code.
2. Indirect/Transit Dependency: The software components which are referred by the direct dependencies. For example, the dependencies which the importing library has.

## Approaches to including dependencies

Below steps can be taken:

1. Install directly from public sources:
Install the open-source dependencies directly from the internet. This is convenient to use, though error pron as the source is manged somewhere else.

2. Store copies of dependencies in source repository:  
This approach is also known as *vendoring*. Instead of installing an external dependency from a public repository during builds, download it and copy it into project source tree. It provides more control over the vendored dependencies that is used, but there are several disadvantages:
    * Vendored dependencies increase the size of source repository and introduce more churn.
    * Must vendor the same dependencies into each separate application. If the source repository or build process does not support reusable source modules, we might need to maintain multiple copies of the dependencies.
    * Upgrading vendored dependencies can be more difficult.

3. Store dependencies in a private registry:  
A private registry, such as Artifact Registry, provides the convenience of installation from a public repository as well as control over your dependencies. With Artifact Registry, you can:
    * Centralize your build artifacts and dependencies for all your applications.
    * Configure your Docker and language package clients to interact with private repositories in Artifact Registry the same way that they do with public repositories.
    * Have greater control over your dependencies in private repositories:
    * Restrict access to each repository with Identity and Access Management.
    * Use remote repositories to cache dependencies from upstream public sources and scan them for vulnerabilities (private preview).
    * Use virtual repositories to group remote and private repositories behind a single end point. Set a priority on each repository to control search order when downloading or installing an artifact (private preview).
    * Easily use Artifact Registry with other Google Cloud services in Software Delivery Shield, including Cloud Build, Cloud Run, and Google Kubernetes Engine. Use automatic vulnerability scanning across the software development lifecycle, generate build provenance, control deployments, and view insights about your security posture.

When possible, use a private registry for your dependencies. In situations where you cannot use a private registry, consider vendoring your dependencies so that you have control over the content in your software supply chain.

## Version pinning

Version pinning means restricting an application dependency to a specific version or version range.  Ideally, pin a single version of a dependency.

Pinning the version of a dependency helps to ensure that your application builds are reproducible. However, it also means that your builds do not include updates to the dependency, including security fixes, bug fixes, or improvements.

You can mitigate this issue using automated dependency management tools that monitor dependencies in your source repositories for new releases. These tools make updates to your requirements files to upgrade dependencies as necessary, often including changelog information or additional details.

Version pinning only applies to direct dependencies, not transitive dependencies.

## Signature and hash verification

There are a number of methods that can be used to verify the authenticity of an artifact that is used as a dependency.

1. Hash verification
2. Signature verification

## Lock files and compiled dependencies

Lock files are fully resolved requirements files, specifying exactly what version of every dependency should be installed for an application. Usually produced automatically by installation tools, lock files combine version pinning and signature or hash verification with a full dependency tree for your application.

Installation tools create dependency trees by fully resolving all downstream transitive dependencies of your top-level dependencies, and then include the dependency tree in your lock file. As a result, only these dependencies can be installed, making builds more reproducible and consistent.  
Example: pip in python, npm in javascript.

## Mixing private and public dependencies

Modern cloud-native applications often depend on both open source, third-party code, as well as closed-source, internal libraries.

However, when mixing private and public dependencies, your software supply chain is more vulnerable to a dependency confusion attack. By publishing projects with the same name as your internal project to open-source repositories, attackers might be able to take advantage of misconfigured installers to install their malicious code instead of your internal dependency.

## Removing unused dependencies

Removing unused dependencies and keeping the software healthy and light.

## Vulnerability scanning

Scanning for any known vulnerabilities, using different code scanning tools.

---
References:

* <https://cloud.google.com/software-supply-chain-security/docs/dependencies>
