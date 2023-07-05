# What is Cloud sql?

Cloud SQL is a fully managed database of one of the flavours out of MySQL(Community Edition), Postgres or SQL Server. It can be configured as multi zonal, which is highly available, the failed instance available in a zone can be replaced by the zonal instance available on standby. The data is replicated between both the instances.

## Cloud SQL instance

A Cloud SQL instance corresponds to one virtual machine (VM). The VM includes the database instance and accompanying software containers to keep the database instance up and running.
![Cloud-sql](/asset/images/gcp/cloud_sql.png)

## Database Instance

A database instance is the set of software and files that operate the databases: MySQL, PostgreSQL or SQL Server.

## High availability

Cloud SQL instances using high availability (HA) provide greater reliability than non-HA instances.

HA in Cloud SQL works by having two synchronized instances: a primary instance and a standby instance. Each instance has exactly one VM. Each instance is in a different zone in the same region.

## Failover

A failover is when Cloud SQL switches serving from the original primary instance to the standby instance.

Autofailover is a mechanism that automatically triggers failover when a Cloud SQL instance didn't issue a heartbeat in the previous interval. The clients are connected to the static IP address, abstracting the end users from the actual resources being used, and hence if the instance is configured as Multi zonal, the autofailover automatically switches the resources to the standby resource.

## Cloud SQL Auth proxy client

The Cloud SQL Auth proxy client is open source software maintained by Cloud SQL. It connects to a companion process, the Cloud SQL Auth proxy server, running on your Cloud SQL instance. You run the Cloud SQL Auth proxy client on your own servers. The Cloud SQL Auth proxy client can be used to establish a secure SSL/TLS connection to the database instance, and/or to avoid having to open the firewall. Authentication is done through Identity and Access Management (IAM).

## Maintenance Window
A maintenance window must be predefined, for google to do the maintenance. Though the maintenance typically only takes place once every few months, the system need to be restarted after this, making it unavailable for the maintenance window.

---
Links

* <https://cloud.google.com/sql/docs/key-terms>
