# BigQuery

BigQuery is a managed petabyte scale OLAP(Online Analytical Processing) database provided by GCP.

## Caching

By default all queries fired on BigQuery are stored in temp tables for subsequent use, the temporary storage is called caching.

Points to Note:

* By default the size of each cache can't exceed 10 GB, i.e. the result set of a query should be less then 10 GB compressed. This can be changed.
* The subsequent query must be exactly the same in order to use the cache, changing anything in the query syntax will result in cache miss, even though the result set is exactly the same.

    For example: The second query in the below example will result in a cache miss.

    `select * from table1` and `select * from table1 where 1=1`
* The underline table must not be changed since the last cache.
* The results won't be cached if the query results are getting stored in a table.
* No caching for streaming ingestion.
* Not cached if the query uses non-deterministic functions like:

  * current_timestamp()
  * now()
  * current_user() etc...
* No caching for external tables.

## WildCard Queries

Important points:

* Wildcard allows multiple tables to be queried once, using wildcard in the query.
* Wildcard can also be achieved by TABLE_SUFFIX keyword in the query.
* Wildcard works best when the search criteria is small. Ex: If we have tables for each year and we want to query data between years 2020 - 2022, wildcard pattern of `202*` will perform better then `20*` simply because there are less tables to look for.
* The inference of the wildcard values in the filters should not refer to wildcard. Ex:
query like this will .

## ARRAY, STRUCT & RECORD DATA TYPE

Bigquery prefers de-normalized modeling over standard star or snowflake data models. This is due to the fact that on the fly joining in distributed systems are very expensive operation, hence minimizing joins can perform much better in bigquery.

Though query on de-normalized tables starts to slow down when the query needs to do group by on columns that has one to many relationships, to achieve this the data needs to be shuffled, which is one of the most data incentive operation.

This overhead is solved by BigQuery, by using the STRUCT and RECORDS type datatype. This enables BigQuery to store the relationship of the data without repeating/duplicating the data.

* ARRAY: An array is an ordered list of zero or more elements of non-array values. Elements in an array must share the same type. Arrays of arrays are not allowed. Queries that would produce an array of arrays will return an error. Instead, a struct must be inserted between the arrays using the SELECT AS STRUCT construct. To create a column with repeated data, set the mode of the column to REPEATED in the schema.
  * To convert an ARRAY into a set of rows, also known as "flattening," use the UNNEST operator. UNNEST takes an ARRAY and returns a table with a single row for each element in the ARRAY.
* STRUCT: A struct is a data type that has attributes in key-value pairs, just like a dictionary in Python.A STRUCT is a container of ordered fields. To create a column with nested data, set the data type of the column to RECORD in the schema.
* A RECORD column can have REPEATED mode, which is represented as an array of STRUCT types. Also, a field within a record can be repeated, which is represented as a STRUCT that contains an ARRAY. An array cannot contain another array directly.
* Nested and repeated schemas are subject to the following limitations:
  * A schema cannot contain more than 15 levels of nested RECORD types.

    Columns of type RECORD can contain nested RECORD types, also called child records. The maximum nested depth limit is 15 levels. This limit is independent of whether the RECORDs are scalar or array-based (repeated).

