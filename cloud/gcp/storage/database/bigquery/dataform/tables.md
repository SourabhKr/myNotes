# Mange Tables in Dataform

In Dataform, a table is one of the types of objects that make up a SQL workflow. Tables can be created from data sources declared in the SQL workflow or other tables in the SQL workflow. Dataform compiles your table definitions into SQL in real time.

Below types of tables can be created using dataform in a type:"table" SQLX file:

* table: a regular table
* incremental: an incremental table
* view: a table view
  * materialized: materialized table view.

Below additional features can be added:

1. Maintaining partition and clusters: To create a table partition, add a BigQuery partition_expression to the bigquery block in a table definition SQLX file. 
   1. The syntax to add the partition as below:

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

2. Adding Documentation
