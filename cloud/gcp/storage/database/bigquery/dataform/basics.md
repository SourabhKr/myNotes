# DataForm

Dataform is a service for data analysts to develop, test, version control, and schedule complex SQL workflows for data transformation in BigQuery.

Once the data is loaded from the source systems to the BigQuery, Dataform can be used to further transform,using SQL.

**NOTE** Dataform does not support customer-managed encryption keys (CMEK) and VPC Service Controls at this time.

## Important points

### Repositories

Each Dataform project is stored in a repository. A Dataform repository houses a collection of JSON configuration files, SQLX files, and JavaScript files.

Dataform repositories contain the following types of files:

* Config files: Config JSON or SQLX files that configure the SQL workflows. They contain general configuration, execution schedules, or schema for creating new tables and views.
* Definitions: Definitions are SQLX and JavaScript files that define new tables, views, and additional SQL operations to run in BigQuery.
* Includes: Includes are JavaScript files that can be used to define variables and functions to use in a project.

Each Dataform repository is connected to a service account. You can select a service account while creating a repository, or the service account can be edited later.

By default, Dataform uses a service account derived from your project number in the following format:
> *<service-YOUR_PROJECT_NUMBER@gcp-sa-dataform.iam.gserviceaccount.com>*

### Version control

Dataform uses the Git version control system to maintain a record of each change made to project files and to manage file versions. Each Dataform repository can manage its own Git repository, or be connected to a remote third-party Git repository

### Workflow development

In Dataform, all the changes to files and directories are made inside a development workspace. A development workspace is a virtual, editable copy of the contents of a Git repository. Dataform preserves the state of files in the development workspace between sessions.

In a development workspace, you can develop SQL workflow actions by using Dataform core with SQLX and JavaScript, or exclusively with JavaScript.
Each element of a Dataform SQL workflow, such as a table or assertion, corresponds to an action that Dataform performs in BigQuery. For example, a table definition file is an action of creating or updating the table in BigQuery.

In a Dataform workspace, following SQL workflow actions can be created:

* Source data declarations
* Tables and views
* Incremental tables
* Table partitions and clusters
* Dependencies between actions
* Documentation of tables
* Custom SQL operations
* BigQuery labels
* BigQuery policy tags
* Dataform tags
* Data quality tests, called assertions

The JavaScript can be used to reuse the Dataform SQL workflow code in the following ways:

1. Across a file with code encapsulation
2. Across a repository with includes
3. Across repositories with packages

Dataform compiles the SQL workflow code in your workspace in real-time.

### Workflow compilation

Dataform uses default compilation settings, configured in dataform.json, to compile the SQL workflow code in your workspace to SQL in real-time, creating a compilation result of the workspace.

You can override compilation settings to customize how Dataform compiles your SQL workflow into a compilation result.

1. With workspace compilation overrides, we can configure compilation overrides for all workspaces in a repository.The dynamic workspace overrides can be used to create compilation results custom for each workspace, turning workspaces into isolated development environments
2. With release configurations, we can configure templates of compilation settings for creating compilation results of a Dataform repository.


### Workflow execution

During workflow execution, Dataform executes compilation results of SQL workflows to create or update assets in BigQuery.


---
Reference

* <https://cloud.google.com/dataform/docs/features>