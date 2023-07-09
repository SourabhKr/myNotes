# What is Cloud Firestore?

Cloud Firestore is the NoSQL, document-oriented database. Firestore is a NoSQL document database built for automatic scaling, high performance, and ease of application development.

Firestore comes with two flavours:

1. Native (called Cloud Firestore)
2. Cloud Datastore

## Firestore in Native mode

Firestore is the next major version of Datastore and a re-branding of the product. Taking the best of Datastore and the Firebase Realtime Database.

Firestore introduces new features such as:

* A new, strongly consistent storage layer
* A collection and document data model
* Real-time updates
* Mobile and Web client libraries

## Firestore in Datastore mode

Firestore in Datastore mode uses Datastore system behavior but accesses Firestore's storage layer, removing the following Datastore limitations:

* Eventual consistency: Datastore queries become strongly consistent unless explicitly configured for eventual consistency.
* Queries in transactions are no longer required to be ancestor queries.
* Transactions are no longer limited to 25 entity groups.
* Writes to an entity group are no longer limited to 1 per second.

Datastore mode disables Firestore features that are not compatible with Datastore:

* The project will accept Datastore API requests and deny Firestore API requests.
* The project will use Datastore indexes instead of Firestore indexes.
* The Datastore client libraries with this project can be used but not Firestore client libraries.
* Firestore real-time capabilities will not be available.
* In the Google Cloud console, the database will use the Datastore viewer.

Here’s a high-level comparison of Datastore and relational database concepts:

![FilestoreRDBMSComparision](/asset/images/gcp/firestore_rdbms_comparision.png)

## Eventual Consistency

Eventual consistency is a theoretical guarantee that, provided no new updates to an entity are made, all reads of the entity will eventually return the last updated value. The Internet Domain Name System (DNS) is a well-known example of a system with an eventual consistency model. DNS servers do not necessarily reflect the latest values but, rather, the values are cached and replicated across many directories over the Internet. It takes a certain amount of time to replicate modified values to all DNS clients and servers

---

Links

* <https://cloud.google.com/datastore/docs/firestore-or-datastore>
* <https://cloud.google.com/datastore/docs/articles/balancing-strong-and-eventual-consistency-with-google-cloud-datastore>
x