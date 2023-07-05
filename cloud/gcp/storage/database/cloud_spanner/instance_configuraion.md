# Instance configurations

An instance configuration defines the geographic placement and replication of the databases in that instance.The instance configurations with fixed regions and replication topologies are referred to as base instance configurations.

1. Regional
2. Multi-Regional

## Regional Configuration

For any base regional configuration, Spanner maintains three read-write replicas, each within a different Google Cloud zone in that region. Each read-write replica contains a full copy of the operational database that is able to serve read-write and read-only requests. Spanner uses replicas in different zones so that if a single-zone failure occurs, the database remains available.
