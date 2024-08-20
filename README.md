# MongoDBLearnings : My Learnings from MongoDB

**What is MongoDB?**
MongoDB is a document database designed for ease of application development and scaling.

You can run MongoDB in the following environments:
MongoDB Atlas  : The fully managed service for MongoDB deployments in the cloud
MongoDB Enterprise  : The subscription-based, self-managed version of MongoDB
MongoDB Community  : The source-available, free-to-use, and self-managed version of MongoDB

**Document Database**
A record in MongoDB is a document, which is a data structure composed of field and value pairs. MongoDB documents are similar to JSON objects. The values of fields may include other documents, arrays, and arrays of documents.

The advantages of using documents are:
  Documents correspond to native data types in many programming languages.
  Embedded documents and arrays reduce need for expensive joins.
  Dynamic schema supports fluent polymorphism.

MongoDB stores documents in collections. Collections are analogous to tables in relational databases.


**Time Series Collections**
  Time series collections are writable non-materialized views.Time series collections efficiently store time series data. 
  In time series collections, writes are organized so that data from the same source is stored alongside other data points from a similar point in time.
  Compared to normal collections, storing time series data in time series collections improves query efficiency and reduces the disk usage for time series data and secondary indexes.
  Time series collections use an underlying columnar storage format and store data in time-order. 
  Starting in MongoDB 6.3: if you create a new time series collection, MongoDB also generates a compound index on the metaField and timeField fields. To improve query performance, queries on time series collections use the new compound index. 
  The compound index also uses the optimized storage format.
  This format provides the following benefits:
    Reduced complexity for working with time series data
    Improved query efficiency
    Reduced disk usage
    Reduced I/O for read operations
    Increased WiredTiger cache usage

In addition to collections, MongoDB provides two different view types: standard views and on-demand materialized views. Both view types return the results from an aggregation pipeline.
**Read-only Views :**
  A MongoDB view is a read-only queryable object whose contents are defined by an aggregation pipeline on other collections or views.
  MongoDB does not persist the view contents to disk. A view's content is computed on-demand when a client queries the view.
**On-Demand Materialized Views:**
  An on-demand materialized view is a pre-computed aggregation pipeline result that is stored on and read from disk. On-demand materialized views are typically the results of a $merge or $out stage.

**Standard views** are computed when you read the view, and are not stored to disk.
**On-demand materialized views** are stored on and read from disk. They use a $merge or $out stage to update the saved data.

  **Indexes**
  Standard views use the indexes of the underlying collection. As a result, you cannot create, drop or re-build indexes on a standard view directly, nor get a list of indexes on the view.
  You can create indexes directly on on-demand materialized views because they are stored on disk.

  **Performance**
  On-demand materialized views provide better read performance than standard views because they are read from disk instead of computed as part of the query. This performance benefit increases based on the complexity of the pipeline and size of the data being aggregated.

  **Read Only**
  Views are read-only. Write operations on views return an error.

  **Snapshot Isolation**
  Views do not maintain timestamps of collection changes and do not support point-in-time or snapshot read isolation.

  **View Pipelines**
  The view's underlying aggregation pipeline is subject to the 100 megabyte memory limit for blocking sort and blocking group operations.


**Key Features of Mongo DB:**

**High Performance**
  MongoDB provides high performance data persistence. In particular,
  Support for embedded data models reduces I/O activity on database system.
  Indexes support faster queries and can include keys from embedded documents and arrays.


**Query API**
  The MongoDB Query API supports:
    read and write operations (CRUD)
      CRUD operations create, read, update, and delete documents.

  **Create Operations**
    Create or insert operations add new documents to a collection. 
    If the collection does not currently exist, insert operations will create the collection.
    MongoDB provides the following methods to insert documents into a collection:
      db.collection.insertOne()
      db.collection.insertMany()

  **Read Operations**
    Read operations retrieve documents from a collection; i.e. query a collection for documents. MongoDB provides the following methods to read documents from a collection:
      db.collection.find()

  **Update Operations**
    Update operations modify existing documents in a collection. MongoDB provides the following methods to update documents of a collection:
      db.collection.updateOne()
      db.collection.updateMany()
      db.collection.replaceOne()

  **Delete Operations**
    Delete operations remove documents from a collection. MongoDB provides the following methods to delete documents of a collection:
      db.collection.deleteOne()
      db.collection.deleteMany()

  **Bulk Write**
  **Retryable Writes**
  **Retryable Reads**
  **SQL to MongoDB**
  **Text Search :**  MongoDB provides different text search capabilities depending on whether your data is hosted on MongoDB Atlas or a self-managed deployment.
  **Geospatial Queries :** In MongoDB, you can store geospatial data as GeoJSON objects or as legacy coordinate pairs.
  **Read Concern :** The readConcern option allows you to control the consistency and isolation properties of the data read from replica sets and sharded clusters.
  **Write Concern :** 

 **Ordered vs Unordered Operations**
  Bulk write operations can be either ordered or unordered.
    With an ordered list of operations, MongoDB executes the operations serially. If an error occurs during the processing of one of the write operations, MongoDB will return without processing any remaining write operations in the list. See ordered Bulk Write
    With an unordered list of operations, MongoDB can execute the operations in parallel, but this behavior is not guaranteed. If an error occurs during the processing of one of the write operations, MongoDB will continue to process remaining write operations in the list. See Unordered Bulk Write Example.
    Executing an ordered list of operations on a sharded collection will generally be slower than executing an unordered list since with an ordered list, each operation must wait for the previous operation to finish.
    By default, bulkWrite() performs ordered operations. To specify unordered write operations, set ordered : false in the options document.
    In MongoDB, update operations target a single collection. All write operations in MongoDB are atomic on the level of a single document.

    Data Aggregation
    Text Search and Geospatial Queries.
