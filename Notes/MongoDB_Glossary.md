# MongoDB Glossary

## A

### Aggregation
A framework that processes data records and returns computed results. It's similar to SQL's GROUP BY and other aggregate functions. The aggregation pipeline consists of stages that process documents and transform them.

### Atlas
MongoDB's cloud database service that handles deployment, management, and scaling of MongoDB clusters.

### Authentication
The process of verifying the identity of a client attempting to connect to a MongoDB server.

### Authorization
The process of determining a client's access rights to database resources and operations.

## B

### B-tree
The data structure that MongoDB uses for its indexes.

### BSON
Binary JSON - the binary-encoded serialization of JSON-like documents that MongoDB uses for document storage and network transfer.

### Bulk Write
A feature in MongoDB that allows you to perform multiple write operations (inserts, updates, deletes) in a batch.

## C

### Collection
A grouping of MongoDB documents. Collections are analogous to tables in relational databases.

### Compound Index
An index that references multiple fields within a document.

### Covered Query
A query that can be satisfied entirely using an index without examining documents.

### CRUD
Create, Read, Update, Delete - the four basic operations for persistent storage.

### Cursor
A pointer to the result set of a query that allows iteration over the result set.

## D

### Database
A physical container for collections. Each database gets its own set of files on the file system.

### Document
A record in a MongoDB collection consisting of field-value pairs. Documents are analogous to rows in relational databases.

### Document Model
MongoDB's data model where information is stored in documents using a JSON-like structure.

### Driver
A client library that provides high-level API for applications to interact with MongoDB.

## E

### Embedded Document
A document that is nested within another document.

### Explain Plan
Information about how MongoDB executes a query, including which indexes are used.

## F

### Field
A name-value pair in a document. A document has zero or more fields.

### Find
A MongoDB operation to retrieve documents from a collection based on specified criteria.

### Flow Control
A feature in MongoDB that throttles write operations when secondaries fall too far behind their primary.

## G

### Geospatial Index
An index that supports queries for geospatial coordinate data.

### GridFS
A specification for storing and retrieving large files in MongoDB.

## H

### Hashed Index
An index that uses a hashing function to create a more balanced sharding.

### Horizontal Scaling
The ability to add more machines to a system to handle increased load.

## I

### Index
A data structure that improves the speed of data retrieval operations by helping MongoDB efficiently find documents.

### Indexing
The process of creating an index on a field to optimize query performance.

### Insert
A MongoDB operation to add documents to a collection.

## J

### JSON
JavaScript Object Notation - a text-based, human-readable format used for representing data structures.

## L

### Load Balancer
A component that distributes network traffic across multiple MongoDB instances to optimize resource utilization.

### Lock
A mechanism that limits access to a resource in a multi-threaded environment.

## M

### Map-Reduce
A data processing paradigm for processing large data sets with a parallel, distributed algorithm.

### Mongod
The primary daemon process for the MongoDB system.

### Mongos
A routing service for MongoDB shard configurations.

### Multikey Index
An index type for fields that contain arrays.

## O

### ObjectId
A 12-byte BSON type used as the default value for the _id field in MongoDB documents.

### Operation Log (Oplog)
A special capped collection that keeps a rolling record of all operations that modify the data stored in MongoDB.

## P

### Primary Key
A unique identifier for a document in a collection, stored in the _id field.

### Primary-Secondary Replication
A replication setup where the primary node receives all write operations and secondary nodes replicate the primary's oplog.

### Projection
Selecting specific fields to include or exclude in query results.

## Q

### Query
An operation that retrieves documents from a collection based on specified criteria.

### Query Optimizer
The component that determines the most efficient way to execute a query.

## R

### Read Concern
The level of read isolation for a query.

### Read Preference
A setting that determines which replica set members receive read operations.

### Replication
The process of synchronizing data across multiple servers.

### Replication Lag
The delay between an operation occurring on the primary and that same operation being applied on a secondary.

### Replication Set
A group of mongod instances that maintain the same data set, providing redundancy and high availability.

## S

### Schema
The organization of data as a blueprint of how a database is constructed.

### Schema Validation
Rules that enforce a specific structure and content for documents in a collection.

### Secondary Index
Any index that is not the primary index (_id field).

### Sharding
A method for distributing data across multiple machines to support deployments with very large data sets and high throughput operations.

### Slow Query Log
A log that records operations that took longer than a configured threshold to complete.

### Storage Engine
The component of the database that manages how data is stored on disk.

### Swappiness
A Linux kernel parameter that controls how much the system can swap memory to disk. For MongoDB, it should be set to 1 or 0.

## T

### TTL Index
Time-To-Live index - an index type that automatically removes documents from a collection after a specified amount of time.

### Text Index
An index type that supports text search operations on string content.

### Transaction
A logical unit of work that includes one or more operations, which either all succeed or all fail.

## V

### Vector Search
A search capability in MongoDB Atlas that enables similarity search based on vector embeddings.

### Virtual Memory
Memory that appears to exist as main memory (RAM) but is actually managed by the OS using both RAM and disk space.

## W

### WiredTiger
The default storage engine for MongoDB since version 3.2, offering document-level concurrency control and compression.

### Write Concern
The level of acknowledgment requested from MongoDB for write operations.

## Z

### Zero Downtime Migration
The process of upgrading or migrating a MongoDB cluster without service interruption. 