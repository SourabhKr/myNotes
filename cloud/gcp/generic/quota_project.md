# Quota project overview

Every request to a Google Cloud API is counted against a quota. Because quotas are enforced on each project, that means
that every request needs a project to provide quota. That project is called the quota project. It's also sometimes
referred to as the billing project. The billing project and the quota project are the same project.

## How the quota project is determined

How the quota project is determined depends on the type of API you use: resource-based API or client-based API.

### Resource-based APIs

For resource-based Google Cloud APIs, the project that provides quota for an API call is also the project that contains
the resource that is being accessed. For example, when you create a Compute Engine instance, you must specify the
project for that new instance. The project then contains the newly created instance. Later, if you perform operations on
the Compute Engine instance, the project that contains the instance provides the quota for the request.

You cannot change the quota project used by a request to a resource-based API. The request always uses the project that
contains the resource that the request is operating on.

### Client-based APIs

If an API is not a resource-based API, it's a client-based API. For example, the Cloud Translation API is a commonly
used client-based API.

When you make a request to a client-based API, if a quota project cannot be identified, the request fails.

### Determine if an API is resource-based or client-based

It can be difficult to determine which type of API you're using. However, activation and quota are enforced in the same
way. If a service account from project A calls a read method in project B, and neither project has the API enabled, the
API not enabled error message indicates which project is checked for activation. The project checked for activation is
the same project checked for rate quota.

--- 
Link

* <https://cloud.google.com/docs/quota/quota-project>
