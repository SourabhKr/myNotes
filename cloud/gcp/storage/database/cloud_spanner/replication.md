# Replication in Cloud Spanner

Spanner automatically replicates at the byte level. Spanner writes database mutations to files in this file system, and the file system takes care of replicating and recovering the files when a machine or disk fails.

Even though the underlying distributed file system that Spanner is built on already provides byte-level replication, Spanner also replicates data to provide the additional benefits of data availability and geographic locality. At a high level, all data in Spanner is organized into rows. Spanner creates multiple copies, or "replicas," of these rows, then stores these replicas in different geographic areas. Spanner uses a synchronous, Paxos-based replication scheme, in which voting replicas take a vote on every write request before the write is committed. 

Spanner creates replicas of each database split. A split holds a range of contiguous rows, where the rows are ordered by primary key. All of the data in a split is physically stored together in the replica, and Spanner serves each replica out of an independent failure zone

## Benefits of Cloud Spanner replication

* Data availability: Having more copies of your data makes the data more available to clients that want to read it. Also, Spanner can still serve writes even if some of the replicas are unavailable, because only a majority of voting replicas are required in order to commit a write.

* Geographic locality: Having the ability to place data across different regions and continents with Spanner means data can be geographically closer, and hence faster to access, to the users and services that need it.

* Single database experience: Spanner can deliver a single database experience because of its synchronous replication and global strong consistency.

* Easier application development: Because Spanner is ACID-compliant and offers global strong consistency, developers working with Spanner don't have to add extra logic in their applications to deal with eventual consistency, making application development and subsequent maintenance faster and easier.

### Replica types

* read-write replicas (Read-write replicas support both reads and writes)
* read-only replicas (Read-only replicas only support reads, but not writes)
* witness replicas (Witness replicas don’t support reads but do participate in voting to commit writes)

---

Links

* <https://cloud.google.com/spanner/docs/replication#read-write>