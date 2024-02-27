# What is resource hierarchy?

Every cloud provider has a specific way of organizing the provided services/resources into an umbrellas, in a unique structure, the same can be called as resource hierarchy. Resource-hierarchy basically has two tasks:
1. Binds the resource lifecycle with the immediate parent.
2. Provide access points for access control.

## What is the resource hierarchy in GCP?

In GCP the resources are divided into two different groups:  

1. account-level resources
2. service-level resources  

The account-level resources, maintain the hierarchy required to manage the company, examples are Organization, Folder and Project. Whereas the service-level resources are the actual services, like VM, DBs etc...
In GCP, the resource hierarchy looks like as below.

- Organization  
&emsp;&emsp; - Folder / Subfolder  
&emsp;&emsp;&emsp; - Project

The same can be seen in the below image:

![GCP-ResourceHierarchy](/asset/images/gcp/cloud-hierarchy.jpg)

Organization being the root node, contains all the resources for a company. An organization can have none or multiple folders. Each folder then contain a project. Project is basically the most important node in the hierarchy, the actual billing is done at this level. All the resources and services are connected to a Project.

Important points:
    The IAM roles can be assigned at different levels, i.e. the access can be controlled at any level mentioned above.

### Organization

The Organization is a mandatory resource, though it's not available in free tier, where the Organization is "NO_ORGANIZATION". Anyway, the organization resources are the route of all the resources. Policies maintained at this level are available to all the resources of the organization. Having an organization resource means that the owner of the project created is the organization and not the account created the project.

Google Cloud users are not required to have an organization resource, but some features of Resource Manager will not be usable without one. The organization resource is closely associated with a Google Workspace or Cloud Identity account. When a user with a Google Workspace or Cloud Identity account creates a Google Cloud project resource, an organization resource is automatically provisioned for them.

### Folder / Subfolder

The folder/subfolder is an optional resource and usually used to have better organizational control. Folders can be the individual department/domain/team of a company. Similar to Organizational resources, folder resources allow administrative access delegation, i.e. access provided at folder level delegated to each resource of the folder. At the same time access to resources can also be restricted to folder, restricting the access of an account to a particular folder.

### Projects

The project resource is the base level organizational resource. Organization and folder resources may contain multiple projects. A project resource is mandatory to use gcp service-level resources.
All project resources consist of the following:

> Two identifiers:
>
> - Project resource ID, which is a unique identifier for the project resource.
> - Project resource number, which is automatically assigned when the project is created. It is read-only.
>
> One mutable display name.
> The lifecycle state of the project resource; for example, ACTIVE or DELETE_REQUESTED.
> A collection of labels that can be used for filtering projects.
> The time when the project resource was created.

 In-order to interact with google resources each request must have the project-id or the auto generated unique project number.


### IAM Policy Inheritance

IAM can control who (users) has what access (roles) to which resources by setting IAM policies on the resources.

The IAM policies can be applied at Organization,  Folder, Project level or in some cases at the resource level.  If a policy is ste at the organization level, it is inherited by all its child folder and project resources, and if you policy is set at the project level, it is inherited by all its child resources.

The effective policy for a resource is the union of the policy set on the resource and the policy inherited from its ancestors. This inheritance is transitive. In other words, resources inherit policies from the project, which inherit policies from the organization resource. Therefore, the organization-resource-level policies also apply at the resource level.

Roles are always inherited, and there is no way to explicitly remove a permission for a lower-level resource that is granted at a higher level in the resource hierarchy.

The IAM policy hierarchy follows the same path as the Google Cloud resource hierarchy. If the resource hierarchy is changed, the policy hierarchy changes as well. For example, moving a project into an organization resource will update the project's IAM policy to inherit from the organization resource's IAM policy. Similarly, moving a project resource from one folder resource to another will change the inherited permissions.
