# Instance configurations

An instance configuration defines the geographic placement and replication of the databases in that instance.The instance configurations with fixed regions and replication topologies are referred to as base instance configurations.

1. Regional
2. Multi-Regional

## Regional Configuration

For any base regional configuration, Spanner maintains three read-write replicas, each within a different Google Cloud zone in that region. Each read-write replica contains a full copy of the operational database that is able to serve read-write and read-only requests. Spanner uses replicas in different zones so that if a single-zone failure occurs, the database remains available.

### Performance best practices for regional configurations

For optimal performance, follow these best practices:

* Design a schema that prevents hotspots and other performance issues.
* Place critical compute resources within the same region as your Spanner instance.
* Provision enough compute capacity to keep high priority total CPU utilization under 65%.
* For the amount of throughput per Spanner node, see performance for regional configurations.

## Multi-region configurations

Multi-region configurations allows to replicate the database's data not just in multiple zones, but in multiple zones across multiple regions, as defined by the instance configuration. These additional replicas enables to read data with low latency from multiple locations close to or within the regions in the configuration.

There are trade-offs though, because in a multi-region configuration, the quorum (read-write) replicas are spread across more than one region. Hence, they can incur additional network latency when these replicas communicate with each other to vote on writes. In other words, multi-region configurations enable your application to achieve faster reads in more places at the cost of a small increase in write latency.

### Multi-region replication

Each base multi-region configuration contains two regions that are designated as read-write regions, each of which contains two read-write replicas. One of these read-write regions is designated as the default leader region, which means that it contains your database's leader replicas. Spanner also places a witness replica in a third region called a witness region.

### Performance best practices for multi-region configurations

* Design a schema that prevents hotspots and other performance issues.
* For optimal write latency, place compute resources for write-heavy workloads within or close to the default leader region.
* For optimal read performance outside of the default leader region, use staleness of at least 15 seconds.
* To avoid single-region dependency for your workloads, place critical compute resources in at least two regions. A good option is to place them next to the two different read-write regions so that any single region outage will not impact all of your application.
* Provision enough compute capacity to keep high priority total CPU utilization under 45% in each region.
* For the amount of throughput per Spanner node, see performance for multi-region configurations.

---

Links

* <https://cloud.google.com/spanner/docs/instance-configurations#regional-performance>
