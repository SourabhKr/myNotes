# What is Cloud Spanner?

Cloud spanner is google's strongly-consistent, distributed, scalable relational database. Cloud spanner can be configured as regional or multi-regional, it maintains multiple copy of read-write and read replicas to maintain very high availability.

## Spanner instance

In cloud spanner the hierarchy goes like this:

* Instance
* Database
* Schema

Spanner instance is the actual resource that the databases in the instance uses. Instance creation includes two important choices: the *instance configuration* and the *compute capacity*. These choices determine the location and amount of the instance's serving and storage resources.

## Cloud Spanner history

There are some datasets that are too large to fit on a single machine. There are also scenarios where the dataset is small, but the workload is too heavy for one machine to handle. This means that we need to find a way of splitting our data into separate pieces that can be stored on multiple machines. Our approach is to partition database tables into contiguous key ranges called splits. A single machine can serve multiple splits, and there is a fast lookup service for determining the machine(s) that serve a given key range. The details of how data is split and what machine(s) it resides on are transparent to Spanner users. The result is a system that can provide low latencies for both reads and writes, even under heavy workloads, at very large scale.

We also want to make sure that data is accessible despite failures. To ensure this, we replicate each split to multiple machines in distinct failure domains. Consistent replication to the different copies of the split is managed by the Paxos algorithm. In Paxos, as long as a majority of the voting replicas for the split are up, one of those replicas can be elected leader to process writes and allow other replicas to serve reads.

Many previous distributed database systems have elected not to provide strong consistency guarantees because of the costly cross-machine communication that is usually required. Spanner is able to provide strongly consistent snapshots across the entire database using a Google-developed technology called TrueTime. Like the Flux Capacitor in a circa-1985 time machine, TrueTime is what makes Spanner possible. It is an API that allows any machine in Google datacenters to know the exact global time with a high degree of accuracy (that is, within a few milliseconds). This allows different Spanner machines to reason about the ordering of transactional operations (and have that ordering match what the client has observed) often without any communication at all.

---
Links

* <https://cloud.google.com/spanner/docs/whitepapers/life-of-reads-and-writes#aside-distributed-filesystems>