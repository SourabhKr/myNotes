# Delta Lake: High-Performance ACID Table Storage over

Cloud Object Stores

### Abstract

Unfortunately, their(Cloud object stores) implementation as key-value stores makes it difficult to achieve ACID
transactions and high performance: metadata operations such as listing objects are expensive, and consistency guarantees
are limited.

In this paper, we present Delta Lake, an open source ACID table storage layer over cloud object stores initially
developed at Databricks. Delta Lake uses a transaction log that is compacted into Apache Parquet format to provide ACID
properties, time travel, and significantly faster metadata operations for large tabular datasets (e.g., the ability to
quickly search billions of table partitions for those relevant to a query)

### Introduction

It's possible to read and write data from cloud object storage using different tools, for example, BigQuery, Redshift,
Trino etc.

Unfortunately, although many systems support reading and writing to cloud object stores, achieving performant and
mutable table storage over these systems is challenging, making it difficult to implement data warehousing capabilities
over them. Unlike distributed filesystems such as HDFS [5], or custom storage engines in a DBMS, most cloud object
stores are merely key-value stores, with no crosskey consistency guarantees

The most common way to store relational datasets in cloud object stores is using columnar file formats such as Parquet
and ORC, where each table is stored as a set of objects (Parquet or ORC “files”), possibly clustered into “partitions”
by some fields (e.g., a separate set of objects for each date) [45].

This approach can offer acceptable performance for scan workloads as long as the object files are moderately large.
However, it creates both correctness and performance challenges for more complex workloads. First, because multi-object
updates are not atomic, there is no isolation between queries: for example, if a query needs to update multiple objects
in the table (e.g., remove the records about one user across all the table’s Parquet files), readers will see partial
updates as the query updates each object individually. Rolling back writes is also difficult:if an update query crashes,
the table is in a corrupted state. Second, for large tables with millions of objects, metadata operations are expensive.
For example, Parquet files include footers with min/max statistics that can be used to skip reading them in selective
queries. Reading such a footer on HDFS might take a few milliseconds, but the latency of cloud object stores is so much
higher that these data skipping checks can take longer than the actual query.

_The core idea of Delta Lake is simple: we maintain information about which objects are part of a Delta table in an ACID
manner, using a write-ahead log that is itself stored in the cloud object store._

### MOTIVATION: CHARACTERISTICS AND CHALLENGES OF OBJECT STORES

#### Object Sore APIs

Cloud object stores also provide metadata APIs, such as S3’s LIST operation [41], that can generally list the available
objects in a bucket by lexicographic order of key, given a start key. This makes it possible to efficiently list the
objects in a “directory” if using file-system-style paths, by starting a LIST request at the key that represents that
directory prefix(e.g., warehouse/table1/). Unfortunately, these metadata APIs are generally expensive: for example, S3’s
LIST only returns up to 1000 keys per call, and each call takes tens to hundreds of milliseconds, so it can take minutes
to list a dataset with millions of objects using a sequential implementation

When reading an object, cloud object stores usually support byterange requests, so it is efficient to read just a range
within a large object (e.g., bytes 10,000 to 20,000). This makes it possible to leverage storage formats that cluster
commonly accessed values.

Updating objects usually requires rewriting the whole object at once. These updates can be made atomic, so that readers
will either see the new object version or the old one.

#### Consistency Properties

The most popular cloud object stores provide eventual consistency for each key and no consistency guarantees across
keys, which creates challenges when managing a dataset that consists of multiple objects.In particular, after a client
uploads a new object, other clients are not necessarily guaranteed to see the object in LIST or read operations right
away. Likewise, updates to an existing object may not immediately be visible to other clients. Moreover, depending on
the object store, even the client doing a write may not immediately see the new objects.

#### Performance Characteristics

In our experience, achieving high throughput with object stores requires a careful balance of large sequential I/Os and
parallelism.1

Each read operation usually incurs at least 5–10 ms of base latency, and can then read data at roughly 50–100 MB/s, so
an operation needs to read at least several hundred kilobytes to achieve at least half the peak throughput for
sequential reads, and multiple megabytes to approach the peak throughput. Moreover, on typical VM configurations,
applications need to run multiple reads in parallel to maximize throughput.

LIST operations also require significant parallelism to quickly list large sets of objects. For example, S3’s LIST
operations can only return up to 1000 objects per requests, and take tens to hundreds of milliseconds, so clients need
to issue hundreds of LISTs in parallel to list large buckets or “directories”. In our optimized runtime for Apache Spark
in the cloud, we sometimes parallelize LIST operations over the worker nodes in the Spark cluster in addition to threads
in the driver node to have them run faster.

Write operations generally have to replace a whole object (or append to it). This implies that if a table is expected to
receive point updates, then the objects in it should be kept small, which is at odds with supporting large reads.

Implications for Table Storage. The performance characteristics of object stores lead to three considerations for
analytical workloads:

1. Keep frequently accessed data close-by sequentially, which generally leads to choosing columnar formats.
2. Make objects large, but not too large. Large objects increase the cost of updating data (e.g., deleting all data
   about one user) because they must be fully rewritten.
3. Avoid LIST operations, and make these operations request lexicographic key ranges when possible.

#### Existing Approaches for Table Storage

Based on the characteristics of object stores, three major approces are used to manage tabular datasets on them today.
We briefly sketch these approaches and their challenges.



---
Link
https://databricks.com/wp-content/uploads/2020/08/p975-armbrust.pdf
