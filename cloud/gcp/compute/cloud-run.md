### Cloud Run 
Cloud run is the serverless compute service in GCP, used to run any kind of workload that can be containerized. This gives the flexibility to deploy applications written in any programming language on top of cloud-run.


There are basically two ways to run any workload in Cloud Run  
1. Cloud Run Services : A Cloud Run service provides the infrastructure required to run a reliable HTTPS endpoint. Developer's responsibility is to make sure that the code listens on a TCP port and handles HTTP requests.
Some features of request type cloud run:
    * Unique HTTPS endpoint for every service
    * Fast request-based auto scaling ()
    * Built-in traffic management
    * Private and public services
Pricing model:
    1. Request-based : Pay on per-requests level, making it very economic if no requests are being processed. 
    2. Instance-based: Charged for the entire lifetime of a container instance and the CPU is always allocated. There's no per-request fee.

2. Cloud Run as a job:  If the workload is to performs a work and then stops (a script is a good example), use a Cloud Run job to run the code. The job can be executed from the command line using the gcloud CLI, schedule a recurring job, or run it as part of a workflow.
    * Array jobs are a faster way to run cloud jobs. An array job is running multiple identical, independent container instances in parallel. Array jobs are a faster way to process jobs that can be split into multiple independent tasks.


#### Services or jobs must be packaged in a container image
A container image is a package with everything a service needs to run. That includes build artifacts, assets, system packages, and (optionally) a runtime. This makes a containerized application inherently portable – it runs anywhere a container can run. 
![container_overview](/images/gcp/container_overview.png)




---
Reference:
1. https://cloud.google.com/run/docs/overview/what-is-cloud-run