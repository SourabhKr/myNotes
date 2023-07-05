# What is Cloud Spanner?

Cloud spanner is google's strongly-consistent, distributed, scalable relational database. Cloud spanner can be configured as regional or multi-regional, it maintains multiple copy of read-write and read replicas to maintain very high availability.

## Spanner instance

In cloud spanner the hierarchy goes like this:

* Instance
* Database
* Schema

Spanner instance is the actual resource that the databases in the instance uses. Instance creation includes two important choices: the *instance configuration* and the *compute capacity*. These choices determine the location and amount of the instance's serving and storage resources.
