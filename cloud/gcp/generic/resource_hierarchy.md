### What is resource hierarchy?
    Every cloud provider has a specific way of organizing the services into different umbrellas. In a unique structure, the same can be called as resource hierarchy.

### What is the resource hierarchy in GCP?
    In GCP, the resource hierarchy looks like as below.     
        - Organization
            - Folder / Subfolder
                - Project

    Organization being the root node, contains all the resources for a company. An organization can have none or multiple folders. Each folder then contain a project. Project is basically the most important node in the hierarchy, the actual billing is done at this level. All the resources and services are connected to a Project.
    Important points:
     The IAM roles can be assigned at different levels, i.e. the access can be controlled at any level mentioned above.
