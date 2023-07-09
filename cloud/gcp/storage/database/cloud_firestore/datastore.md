# Datastore Data Model

## Entity

Data objects in Firestore in Datastore mode are known as entities. An entity has one or more named properties, each of which can have one or more values. Entities of the same kind do not need to have the same properties, and an entity's values for a given property do not all need to be of the same data type.Each entity in a Datastore mode database has a key that uniquely identifies it.

## Kinds and identifiers

Each entity is of a particular kind, which categorizes the entity for the purpose of queries. In addition to a kind, each entity has an identifier, assigned when the entity is created. Because it is part of the entity's key, the identifier is associated permanently with the entity and cannot be changed.

## Ancestor paths

Entities in a Datastore mode database form a hierarchically structured space similar to the directory structure of a file system. When you create an entity, you can optionally designate another entity as its parent; the new entity is a child of the parent entity (note that unlike in a file system, the parent entity need not actually exist). An entity without a parent is a root entity. The association between an entity and its parent is permanent, and cannot be changed once the entity is created.

## Entity groups

An entity group consists of a root entity and all of its descendants. Applications typically use entity groups to organize highly related data.
