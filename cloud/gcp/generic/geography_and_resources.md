# Overview Regions and Zones

Regions are independent geographic areas that consist of zones. Zones and regions are logical abstractions of underlying
physical resources. A region consists of three or more zones housed in three or more physical data centers.

A zone is a deployment area for Google Cloud resources within a region. Zones should be considered a single failure
domain within a region. To deploy fault-tolerant applications with high availability and help protect against unexpected
failures, deploy your applications across multiple zones in a region.

***Note***: **Google Cloud's services and resources can be zonal, regional, or managed by Google across multiple
regions.**

### Zonal resources

Zonal resources operate within a single zone. Zonal outages can affect some or all of the resources in that zone. An
example of a zonal resource is a Compute Engine virtual machine (VM) instance that resides within a specific zone.

### Regional resources

Regional resources are resources that are redundantly deployed across multiple zones within a region, for example App
Engine applications.

### Multiregional resources

Multiple Google Cloud services are managed by Google to be redundant and distributed within and across regions. These
services optimize availability, performance, and resource efficiency. As a result, these services require a trade-off
between either latency or the consistency model.These trade-offs are documented on a product specific basis.

The following services have one or more multiregional locations in addition to any regional locations:

* Artifact registry
* Bigtable
* BigQuery
* Others ...

---
Resources:

* https://cloud.google.com/docs/geography-and-regions#regional_resources
