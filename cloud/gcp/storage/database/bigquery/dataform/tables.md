# Mange Tables in Dataform

In Dataform, a table is one of the types of objects that make up a SQL workflow. Tables can be created from data sources declared in the SQL workflow or other tables in the SQL workflow. Dataform compiles your table definitions into SQL in real time.

Below types of tables can be created using dataform in a type:"table" SQLX file:

* table: a regular table
* incremental: an incremental table
* view: a table view
  * materialized: materialized table view.

## Creating Tables

Defining table is simple in Dataform, the type used is as of type: "table" and add the SQL script that will be used to generate the table in the SQLX file. Dataform then compiles the Dataform core code into SQL, executes the SQL code, and creates the defined tables in BigQuery.

In the SQLX file called the Dataform core the SELECT statement contains the table structure and reference other objects.

In addition to defining tables in a type: "table" SQLX file, the empty table can be created by defining a custom SQL query in a type: "operations" SQLX file.

To add table dependencies that are not referenced in the SELECT statement, but need to be executed before the current table, dependencies attribute can be added in the config block. 

Example:

``` json
    config { dependencies: [ "some_table", "some_other_table" ] }
```

## Maintaining partition and clusters

   1. To create a table partition, add a BigQuery partition_expression to the bigquery block in a table definition SQLX file.The syntax to add the partition as below:

        ``` json
        config {
        type: "table",
        bigquery: {
            partitionBy: "DATETIME_TRUNC(<timestamp_column>, HOUR)"
            }
        }
        ```

   2. Partition filter: Queries that reference this table must use a filter on the partitioning column, or else BigQuery returns an error. Setting this option to true can help prevent mistakes in querying more data than intended. Below attribute can be set to add this filter.

        ``` json
         requirePartitionFilter : true
        ```

   3. To control retention of all partitions in a partitioned table

        ``` json
        partitionExpirationDays: NUMBER_OF_DAYS
        ```

   4. To create table clusters below syntax can be used:

        ``` json
            config {
                type: "table",
                bigquery: {
                    partitionBy: "DATE(ts)",
                    clusterBy: ["name", "revenue"]
                }
            }
            SELECT CURRENT_TIMESTAMP() as ts, name, revenue
        ```

## Adding Documentation in table

Table, column, and record descriptions can be added to all table types in Dataform: table, incremental table and views.

To add descriptions of individual columns and records to a SQLX file. Example:

``` json
record_name: {
      description: "Description of the record",
      columns: {
        record_column_name: "Description of the record column"
      }
}
```

### Reuse column documentation in Dataform with includes

The column descriptions can be reused across the SQL workflow with JavaScript includes. 

* To create a reusable a column description, define a JavaScript include constant with the name of the column and its description.

The following code sample shows multiple constants with descriptions of individual columns defined in the includes/docs.js JavaScript file:

``` json

// filename is includes/docs.js

const user_id = `A unique identifier for a user`;
const age = `The age of a user`;
const creation_date = `The date this user signed up`;
const user_tenure = `The number of years since the user's creation date`;
const badge_count = `The all-time number of badges the user has received`;
const questions_and_answer_count = `The all-time number of questions and answers the user has created`;
const question_count = `The all-time number of questions the user has created`;
const answer_count = `The all-time number of answers the user has created`;
const last_badge_received_at = `The time the user received their most recent badge`;
const last_posted_at = `The time the user last posted a question or answer`;
const last_question_posted_at = `The time the user last posted an answer`;
const last_answer_posted_at = `The time the user last posted a question`;

module.exports = {
   user_id,
   age,
   creation_date,
   user_tenure,
   badge_count,
   questions_and_answer_count,
   question_count,
   answer_count,
   last_badge_received_at,
   last_posted_at,
   last_question_posted_at,
   last_answer_posted_at,
};
```

The following code sample shows the user_id and age constants, defined in includes/docs.js, used in the definitions/my_table.sqlx SQLX table definition file to generate documentation for selected columns in the table:

```json
config {
  type: "table",
  description: "Table description.",
  columns: {
    user_id: docs.user_id,
    column2_name: "Description of the second column",
    column3_name: "Description of the third column",
    age: docs.age,
  }
}

SELECT ...
```

## Configure additional table settings

With Dataform core,  pre_operations and post_operations can be defined to execute a SQL statement before or after table creation. This can also be used for overriding table settings, such as database or schema, and disabling table creation.

1. Override table settings
   By default, a table follows the schema and database configuration set in dataform.json. The name of a table is the same as the name of the table definition SQLX file. To override the defaults add the below configuration in the config block of each sqlx file:

    ```json
     {
    schema: "OVERRIDDEN_SCHEMA",
    database: "OVERRIDDEN_DATABASE",
    name: "OVERRIDDEN_NAME"
    }
    ```


---
Reference

* <https://cloud.google.com/dataform/docs/tables>
* <https://cloud.google.com/dataform/docs/define-table>
* <https://cloud.google.com/dataform/docs/partitions-clusters>
* <https://cloud.google.com/dataform/docs/document-tables>