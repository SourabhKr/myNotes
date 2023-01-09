## Cloud Storage
Cloud storage is the service from gcp, used to store objects. An object is an immutable piece of data consisting of file of any format. Buckets are the containers that can be used to store the objects. The buckets are associated with a project of an organization. 
i.e., A bucket will be stored in an Organization, project and a bucket.
Each object in gcp is referred as a resource. 

Security around cloud storage:  
* IAM to manage fine grained access to principals
* Data Encryption, server side encryption is enabled by default for all the objects stored in GCP. It can further be controlled by providing customer encryption keys.
* Authentication: Ensures that anyone who access the data has proper credentials.
* Bucket Lock: Retention period of objects in the bucket.
* Object Versioning: Different versions can live simultaneously, allowing deleted files to be recovered.

### Cost classes around cloud storage:
1. Storage Costs
2. Data Processing 
    * Operation Charges
    * Inter region-replication charges
    * Autoclass Management fees
3. Each tag that is attached to a bucket is charged at $0.005 per month.
4. Network Charges: 
    * Egress represents data sent from Cloud Storage in HTTP responses. Data or metadata read from a Cloud Storage bucket is an example of egress.
    * Ingress represents data sent to Cloud Storage in HTTP requests. Data or metadata written to a Cloud Storage bucket is an example of ingress.

    1. Network egress within Google Cloud: when egress is to other Cloud Storage buckets or to Google Cloud services.
    2. Specialty network services: when egress uses certain Google Cloud network products
    3. General network usage: when egress is out of Google Cloud or between continents.


### Storage Classes
Basically there are around four classes:
1. Standard
2. Nearline 
3. Coldline
4. Archive

#### Standard
* Default storage class, usually called as hot layer.
* Used for most accessible data.
* No minimum storage duration
* Storage Costs 
    1. Around 0.020 dollar per gb per month
    2. Custom metadata charges +  XML API multipart upload


#### Nearline
* Used to store data, that lives for at least 30 days and accessed infrequently.
* Use-case would be backups of historical data that only need be processed once a month.
* Storage Costs
    1. Around 0.013 dollars per gb per month
    2. Early deletion costs can incur. .i.e, if the object is deleted or overwritten or the object class is changed, within 30 days of object creation. Early deletion charges do not apply in the following cases:
        * When Object Lifecycle Management changes an object's storage class.
        * When the object exists in a bucket that has Autoclass enabled.

#### ColdLine
* Coldline storage is a very-low-cost, highly durable storage service for storing infrequently accessed data.
* A minimum of 90 days object retention is required. 
* Stroage Costs:
    1. Around 0.006 dollars per gb per month
    2. Early deletion costs as explained above.

#### Archive
* Archive storage is the lowest-cost, highly durable storage service for data archiving, online backup, and disaster recovery.
* Storage Costs
    1. Around 0.0025 dollars per gb per month
    2. Early deletion costs as explained above.

Reference:  
1. https://cloud.google.com/storage/docs/introduction
2. https://cloud.google.com/storage/docs/storage-classes 
3. https://cloud.google.com/storage/pricing#europe