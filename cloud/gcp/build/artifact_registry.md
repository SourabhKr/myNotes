# What is artifact registry?

Artifact registry provides a single location for storing and managing packages and Docker container images.

Artifact registry provides below features:

1. Integrate Artifact Registry with Google Cloud CI/CD services or on existing CI/CD tools.
    * Store artifacts from Cloud Build.
    * Deploy artifacts to Google Cloud runtime, including Google Kubernetes Engine, Cloud Run, Compute Engine, and App Engine flexible environment.
    * Identity and Access Management provides consistent credentials and access control.
2. Protect software supply chain.
    * Manage container metadata and scan for container vulnerabilities with Container Analysis.
    * Enforce deployment policies with Binary Authorization.
3. Protect repositories in a VPC Service Controls security perimeter.
4. Create multiple regional repositories within a single Google Cloud project. Group images by team or development stage and control access at the repository level.
5. All repository content is encrypted using either Google-managed or customer-managed encryption keys. Artifact Registry uses Google-managed encryption keys by default and no configuration is required for this option.

Artifact Registry integrates with Cloud Build and other continuous delivery and continuous integration systems to store packages from builds. It can also store trusted dependencies that is used for builds and deployments.

## Artifact Registry supports the following container image formats

1. Docker Image Manifest V2, Schema 1
2. Docker Image Manifest V2, Schema 2
3. Open Container Initiative (OCI) Image Format Specifications

## Pricing

* Storage: Storage costs apply to the at-rest storage of all artifacts in Artifact Registry repositories. The pricing is the same for both regional and multi-regional repositories.
Usage : over 0.5GB $0.10 per GB / month

* Network
    1. Egress: Network egress pricing is per GB delivered from Artifact Registry repositories. When network traffic leaves a repository, the pricing depends on both the repository location and the destination of the traffic.
        * Internet egress pricing is based on Premium tier pricing. Internet egress is network traffic leaving a repository to a client that is not a Google product, such as using a local server that is downloading artifacts.
        * For egress to destinations within Google Cloud: within same region it's free.
    2. Ingress: Network ingress is free.

* Vulnerability scanning: (If the Container Scanning API is enabled)

### Repositories

Artifact Registry enables storing different artifact types, create multiple repositories in a single project, and associate a specific region or multi-region with each repository.

#### Repository format

Each repository is associated with a specific artifact format. For example, a Python repository stores Python packages. Multiple repositories for each format can be created in the same Google Cloud project.

#### Access control

For each repository, consider the level of access final users need. For example:

* You have a development repository for applications that are in development and production repository for applications that are released. Developers have read and write access to the development repository and read-only access to the production repository.
* You have a demo repository with sample applications. Your Sales team has read-only access to download the demos.

#### Repository locations

Multiple repositories can be created in the same region or multi-region. A good repository location balances latency, availability, and bandwidth costs for data consumers.

#### While creating repository below settings have to be provided

1. The artifact format the repository will store.
2. The regional or multi-regional location.
3. A Cloud Key Management Service key, while using customer-managed encryption keys.

*These settings cannot be changes after the repository is created.*

---
Reference:

1. <https://cloud.google.com/artifact-registry/docs/overview>
2. <https://cloud.google.com/artifact-registry/pricing>
3. <https://cloud.google.com/artifact-registry/docs/repositories>
