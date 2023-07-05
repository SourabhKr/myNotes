# Compute Capacity

Compute capacity defines amount of server and storage resources that are available to the databases in an instance. Storage limits are automatically configured by Spanner based on the compute capacity.

On a higher level below are the configuration for storage.

* For instances smaller than 1 node (1000 processing units), Spanner allots 409.6 GB of data for every 100 processing units in the database.
* For instances of 1 node and larger, Spanner allots 4 TB of data for each node.
