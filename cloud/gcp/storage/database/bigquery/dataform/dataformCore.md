# Dataform Core

Dataform core is an open source meta-language to create SQL tables and workflows. Dataform core extends SQL by providing a dependency management system, automated data quality testing, and data documentation.

Dataform core can be used for following purposes:

* Defining tables, views, materialized views, or incremental tables.
* Defining data transformation logic.
* Declaring source data and managing table dependencies.
* Documenting table and column descriptions inside code.
* Reusing functions and variables across different queries.
* Writing data assertions to ensure data consistency.

Dataform uses Dataform core to develop SQL workflows and deploy assets to BigQuery.

To use Dataform core, we write SQLX files. Each SQLX file contains a query that defines a database relation that Dataform creates and updates inside the data warehouse.

## SQLX file config block

A SQLX file consists of a config block and a body. All config properties, and the config block itself, are optional. Given this, any plain SQL file is a valid SQLX file that Dataform executes as-is.

In the config block, you can perform the following actions:

* Specify query metadata
  * This can be used to configure how Dataform materializes queries into a warehouse, for example the output table type, the target database, or labels using the config metadata.
* Document data
  * The tables and their fields can directly be documented in the config block. Documentation of the tables are pushed directly to BigQuery.
* Define data quality tests
  * Define data quality tests, called assertions, to check for uniqueness, null values, or a custom condition. Dataform adds assertions defined in the config block to the workflow dependency tree after table creation. Assertions can also be defined outside the config block, in a separate SQLX file.

## SQLX file body

In the body of a SQLX file we can perform the following actions:

* Define a table and its dependencies
  * To define a new table you can use SQL SELECT statements and the ref function. The ref function is a SQLX built-in function that is critical to dependency management in Dataform.Dataform uses the ref function to build a dependency tree of all the tables to be created or updated.
* Define additional SQL operations to run in your data warehouse
  * To configure Dataform to execute one or more SQL statements before or after creating a dataset, you can specify pre-query and post-query operations.
* Generate SQL code with JavaScript.
  * To define reusable functions to generate repetitive parts of SQL code, you can use JavaScript blocks. You can reuse code defined in a JavaScript block only inside the SLQX file where the block is defined. To reuse code across your entire repository, you can create includes.

---
Reference

* <https://cloud.google.com/dataform/docs/dataform-core>