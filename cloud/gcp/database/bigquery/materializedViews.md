# Materialized Views(MV)

MV periodically caches the results of a query for increased performance and efficiency. It can significantly improves the performance of workloads that have the characteristics of common and repeated queries.

Materialized view can optimize queries with high computation cost and small dataset result.

Key characteristics of MV:

* Zero maintenance: MVs are recomputed in the background when the base table changes. Any incremental data change from the base tables are automatically added to the MV with no user action required.

* Fresh data: For incremental MV, if base table changes invalidate the MV the data is read from the base table, otherwise in other cases only the delta changes are read from the base tables, making MV providing always fresh data.

* Smart Tunning: For incremental MV, BQ automatically tries to read the data from MV whenever possible, even if the query did not directly queried the MV.

### MV Usage

Querying a MV is exactly similar to querying regular table or standard view. Queries against materialized views are always consistent with queries against the view's base tables, even if those tables have changed since the last time the materialized view was refreshed. Querying does not automatically trigger a materialized refresh.

* Incremental updates

  * BigQuery combines the cached view data with new data to provide consistent query results while still using the materialized view. For single-table materialized views, this is possible when the base table has not changed since the last refresh, or only new data has been added. For multi-table views, no more than one table may have appends. All others cannot have changes.

  * If there were any updates or deletes in the base tables since the last refresh, or if more than one of a multi-table materialized view's base tables have changed, BigQuery automatically reverts to the original query.

* Partition alignment

    If a materialized view is partitioned, BigQuery ensures that its partitions are aligned with the partitions of the base table's partitioning column.

    Materialized views with inner joins can only be aligned with one of their base tables. If one of the non-aligned base tables changes, it affects the entire view.

* Smart tuning

    BigQuery automatically rewrites queries to use materialized views whenever possible. Automatic rewriting improves query performance and cost, and does not change query results.

    For a query to be rewritten, the materialized view must meet the following conditions:
  * Belong to the same dataset as one of its base tables.
  * Use the same set of base tables as the query.
  * Include all columns being read.
  * Include all rows being read.

A broader functionalities can be see in the below image.

![MaterializedView](/asset/images/gcp/MaterialzedViewComparision.png)

### Important Limitations of Materialized View

* The data of a materialized view cannot be updated or manipulated directly using operations such as copy, export, load, write, or data manipulation language (DML) statements.
* The view SQL cannot be updated after the materialized view is created.
* A materialized view must reside in the same organization as its base tables, or in the same project if the project does not belong to an organization.
* Each base table can be referenced by a limited number of materialized views.
* Only materialized views from the same dataset are considered for smart tuning.
* Materialized views cannot be nested on other materialized views.
* Materialized views cannot query external or wildcard tables.
* If you delete a base table without first deleting the materialized view, queries and refreshes of the materialized view fail. If you recreate the base table, you must also recreate the materialized view.

## Incremental Materialized view

* Each table is limited to 20 MV with the same dataset, 100 MVs within the same organization.
* MV uses restricted sql syntax.
* Below are the MV query limitations:

  * Aggregates in the MV must be in the outputs. Computing or filtering based on aggregate values are not supported.
  * Joins other then inner joins are not supported. i.e. Left/Right/full joins as well as self joins are not supported.
  * Windows functions not supported.
  * ARRAY sub-queries not supported.
  * Non-Deterministic functions not supported.
  * UDFs not supported.

### Partitioning in Materialized view

* MV build on top of partitioned tables can be partitioned.
* Only partitioned columns of the base table is allowed to be partitioned.
* By default MV is un-partitioned.
* **Recommendation**: If the base table is partitioned consider partitioning the MV, to reduce refresh job maintenance cost and query cost.

### Clustering in Materialized view

* Any column other then aggregate column from the output column list cab be used for clustering, subject to BQ clustering limitations.

### Joins in MV Query

While having inner joins in the materialized view, usually keeping the biggest fact table as the first table works perfectly for incremental update, in case of data change in the first table. Though, changes in any other table invalidates the MV and will gets automatically refreshed.

### MAX_STALENESS in MV

MV comes with an option to use stale data for the given staleness interval. This can be very cost effective if the requirement allows stale responses on a very frequent changing dataset. In case of MAX_STALENESS the query runs with the following condition.

1. If the last refresh is within the MAX_STALENESS interval, then BQ returns data directly from MV.
2. If the last refresh is outside of the MAX_STALENESS interval, then the query reads data from the base tables to return results within the staleness interval.

### Data streaming and max_staleness results

While streaming data into the base tables of a materialized view with the max_staleness option, then the query of the materialized view might exclude records that were streamed into its tables before the beginning of the staleness interval.

### Smart tuning and the max_staleness option

Smart tuning automatically rewrites queries to use materialized views whenever possible regardless of the max_staleness option, even if the query does not reference a materialized view. The max_staleness option on a materialized view does not affect the results of the rewritten query. The max_staleness option only affects queries that directly query the materialized view.

## Non-incremental MV

Allows most of the SQL operations, including all kind of joins, windows and analytical functions which are usually not available in Incremental MV.

### Limitations of No-Incremental MV

* Smart-tunning is not applied.
* Can configured to automatically/manually full refresh the MV by using allow_non_incremental_definition option.

---

Links

* <https://cloud.google.com/bigquery/docs/materialized-views-intro>
