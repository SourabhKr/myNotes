### What is resource hierarchy?
Every cloud provider has a specific way of organizing the provided services/resources into an umbrellas, in a unique structure, the same can be called as resource hierarchy. Resource-hierarchy basically has two tasks:
    1. Binds the resource lifecycle with the immediate parent.
    2. Provide access points for access control.

### What is the resource hierarchy in GCP?
In GCP, the resource hierarchy looks like as below.     
- Organization <br>
&emsp;&emsp; - Folder / Subfolder <br>
&emsp;&emsp;&emsp; - Project
The same can be seen in the below image:

![GCP-ResourceHierarchy](/images/gcp/cloud-hierarchy.jpg) <br><br>

Organization being the root node, contains all the resources for a company. An organization can have none or multiple folders. Each folder then contain a project. Project is basically the most important node in the hierarchy, the actual billing is done at this level. All the resources and services are connected to a Project.

Important points:
    The IAM roles can be assigned at different levels, i.e. the access can be controlled at any level mentioned above.<br><br>


### Organization:
The Organization is a mandatory resource, though it's not available in free tier, where the Organization is "NO_ORGANIZATION". Anyway, the organization resources are the route of all the resources. Policies maintained at this level are available to all the resources of the organization. Having an organization resource means that the owner of the project created is the organization and not the account created the project. <br><br>

### Folder / Subfolder:
The folder/subfolder is an optional resource and usually used to have better organizational control. Folders can be the individual department/domain/team of a company. Similar to Organizational resources, folder resources allow administrative access delegation, i.e. access provided at folder level delegated to each resource of the folder. At the same time access to resources can also be restricted to folder, restricting the access of an account to a particular folder. <br><br>

### Projects: 
The project resource is the base level organizational resource. Organization and folder resources may contain multiple projects. A project resource is mandatory to use gcp resources. <br>
All project resources consist of the following:

> Two identifiers:
> * Project resource ID, which is a unique identifier for the project resource.
> * Project resource number, which is automatically assigned when you create the project. It is read-only.
>
> One mutable display name. <br>
> The lifecycle state of the project resource; for example, ACTIVE or DELETE_REQUESTED.<br>
> A collection of labels that can be used for filtering projects. <br>
> The time when the project resource was created.
 
 In-order to interact with google resources each request must have the project-id or the auto generated unique project number.
