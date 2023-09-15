# SQL Workflows

Dataform can be used to develop, test and version control SQL Workflows that can be used to transform the data in BigQuery.

A SQL workflow can consist of the following objects:

* Data source declarations: Declarations of BigQuery data sources that can be  referenced in Dataform table definitions and SQL operations.
* Tables: Tables that can be created in Dataform based on the declared data sources or other tables in the SQL workflow. Dataform supports the following table types: table, incremental table, view, and materialized view.
* Assertions: Data quality test that can be used to validate table data. Dataform runs assertions every time it updates your SQL workflow and it alerts you if any assertions fail.
* Custom SQL operations: SQL statements that Dataform runs in BigQuery as they are, without modification.
* Includes: JavaScript files with definitions of variables and functions that can be reused across SQL workflows.

## Execution configuration options

Dataform also provides Dataform execution tag, these tags which can be added in individual sql workflows and can be used to club and trigger different workflows.

By default Dataform executes the sql workflow based on the configuration available in the dataform.json file. The same can also be overwritten using Release configuration and Workflow configuration.

Workspace configuration: Workflow configuration can be used to convert workspaces into isolated development environments. This means that when you manually trigger execution in a workspace, Dataform executes the output in an isolated location in BigQuery.

Release configuration: Release configuration can be used to configure compilation override for the entire repository as well as the frequency of creating compilation results with the applied settings.

## Declare a Data source

Any BigQuery Table types (Standard BigQuery table, External Tables, Views) can be declared as a data source in Dataform.  Declaring BigQuery data sources that are external to Dataform allows data sources to be treated as first-class Dataform objects. Once declared as a data source, the same can be referenced or resolved in the same way as any other table in Dataform.
