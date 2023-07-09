# Firestore in Native Mode

## Data Model

Firestore deals in documents and each document exists in a collection. Each document contains a set of key-value pairs. Firestore is optimized for storing large collections of small documents.Documents can contain subcollections and nested objects, both of which can include primitive fields like strings or complex objects like lists.

Collections and documents are created implicitly in Firestore. Simply assign data to a document within a collection. If either the collection or document does not exist, Firestore creates it.

### Documents

In Firestore, the unit of storage is the document. A document is a lightweight record that contains fields, which map to values. Each document is identified by a name.Complex, nested objects in a document are called maps.

### Collections

Documents live in collections, which are simply containers for documents. A collection contains documents and nothing else.It can't directly contain raw fields with values, and it can't contain other collections. The names of documents within a collection are unique. 

Firestore is schemaless, so you have complete freedom over what fields you put in each document and what data types you store in those fields. Documents within the same collection can all contain different fields or store different types of data in those fields. However, it's a good idea to use the same fields and data types across multiple documents, so that you can query the documents more easily.

### References

Every document in Firestore is uniquely identified by its location within the database.A reference is a lightweight object that just points to a location in your database. 

### Subcollections

A subcollection is a collection associated with a specific document.Notice the alternating pattern of collections and documents. Your collections and documents must always follow this pattern. You cannot reference a collection in a collection or a document in a document.Documents in subcollections can contain subcollections as well, allowing you to further nest data. You can nest data up to 100 levels deep.

### Hierarchical Data

As data in Firestore can only exists in documents; hierarchical data is modeled by keeping subcollections in the documents and hence maintaining the parent child relationship, required for hierarchy.

## Indexing

Index by it core means keeping a shortcut to the actual content of the data, which plays a very huge role in the database performance. If no index exists for a query, most databases crawl through their contents item by item, a slow process that slows down even more as the database grows. Firestore guarantees high query performance by using indexes for all queries. As a result, *query performance depends on the size of the result set and not on the number of items in the database*.

There are two types of indexes in Firestore:

1. Single-Field: A single-field index stores a sorted mapping of all the documents in a collection that contain a specific field. Each entry in a single-field index records a document's value for a specific field and the location of the document in the database. By default, Firestore automatically maintains single-field indexes for each field in a document and each subfield in a map. A field can be exempted from automatic indexing settings by creating a single-field index exemption.
2. Composite: A composite index stores a sorted mapping of all the documents in a collection, based on an ordered list of fields to index.Firestore uses composite indexes to support queries not already supported by single-field indexes.Firestore does not automatically create composite indexes like it does for single-field indexes because of the large number of possible field combinations.

---
Links

* <https://cloud.google.com/firestore/docs/data-model>
* <https://cloud.google.com/firestore/docs/concepts/structure-data>
* <https://cloud.google.com/firestore/docs/concepts/index-overview>
