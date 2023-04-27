# Partitioning & Clustering

## Partitioning

Partitioning is a strategy to store very big dataset into smaller segments to optimize the I/O and overall query performance.

Partitioning provides below benefits:

* Parallelism: By introducing good partitioning criteria the data is split into different files, that can be processed in parallel to produce the desired results.
* Different partitioned blocks can live on different disk sub-systems, making it more cost-effective. For example: less used partitions can sit in low cost storage.
* Upserts can be improved by targeting only the required data.
* Allowed data types for partitions:

  * INT
  * DATETIME
* Partition can be done using only one column.
* Metadata table which holds all the partition related information in BQ is __PARTITION_SUMMARY

* Ingestion time of the data can also be used for partition other then the custom columns. While using the ingestion time, BQ can automatically partition the data  either based on the date or the hour of ingestion time, making the partition daley/hourly partitioned.
* Ingestion time partitions adds additional column in the table.

  * For Hourly: __PARTITIONTIME
  * For daily: __PARTITIONTIME as well as__PARTITIONDATE

* In case of custom date column being used for partitioning, additional partitions of __NULL and__UNPARTITIONED gets added, and these partitions are used for data missing the data and having invalid date values consecutively.
* For integer range partition tables similar partitions will get added for null and rows having out of range partition values for the partition column.
* Limitations:

  * Maximum number of partitions allows is 4000.
  * Maximum number of partitions modified per day:
    * For ingestion time - 5000
    * Column Partitioned - 30,000

## Clustering

Clustering is further organizing the data such that the data of similar type can be stored together. Clustering improves the i/o performance by storing ranges of a datatype, storing the data in the sorted order by the clustered columns.

* Limitations:

  * A maximum of 4 columns can be used for clustering. The data stored on the disk follows the order of clustered columns.
  * Datatypes allowed are: Date, Boolean, Geography, Int64, Numeric, Timestamp, String.

### Note for Partition & Cluster

* Avoid using complex calculation son the partitioned/clustered columns, present in query filters. Calculations on filters like casting or comparing with other columns can cause the partition/cluster pruning to not work and result in full table scans.
* Cluster/Partition columns should be the top-level non-repeated columns.
