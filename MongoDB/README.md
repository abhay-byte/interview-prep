### **MongoDB: 20 Theoretical & Conceptual Questions**

**1. Q: What is MongoDB, and what type of database is it?**
*   **A:** MongoDB is a popular, open-source **NoSQL database**. Specifically, it is a **document-oriented database**. It stores data in flexible, JSON-like documents with dynamic schemas, meaning that documents in the same collection do not need to have the same set of fields or structure.

**2. Q: What is the primary difference between a relational database (like PostgreSQL) and MongoDB?**
*   **A:** The primary difference is the data model.
    *   **Relational databases** use a structured schema with tables, rows, and columns. They enforce data integrity through relationships and are ideal for structured data.
    *   **MongoDB** uses a flexible, schema-less (or dynamic schema) model with collections and documents (BSON). It is designed for unstructured or semi-structured data and prioritizes scalability and flexibility.

**3. Q: What is a "document" in MongoDB?**
*   **A:** A document is the basic unit of data in MongoDB. It is a data structure composed of field-and-value pairs, similar in structure to a JSON object. Documents are stored in a binary-encoded format called **BSON** (Binary JSON), which supports more data types than standard JSON.

**4. Q: What is a "collection" in MongoDB?**
*   **A:** A collection is a grouping of MongoDB documents. It is the equivalent of a table in a relational database. A collection exists within a single database and does not enforce a strict schema; documents within a collection can have different fields.

**5. Q: What is BSON?**
*   **A:** BSON stands for Binary JSON. It is a binary-encoded serialization of JSON-like documents that MongoDB uses for storing data. It is designed to be lightweight, traversable, and efficient. BSON extends the JSON model to provide additional data types like `ObjectId`, `Date`, and binary data.

**6. Q: What is the `_id` field in a MongoDB document?**
*   **A:** Every document in a MongoDB collection must have a unique `_id` field, which acts as its **primary key**. If you don't provide an `_id` value when inserting a document, MongoDB automatically generates a unique 12-byte `ObjectId` for it.

**7. Q: What is an index in MongoDB?**
*   **A:** An index is a special data structure that stores a small portion of the collection's data set in an easy-to-traverse form. Indexes improve the speed of query operations by allowing the database to find documents without scanning every document in the collection. The `_id` field is automatically indexed.

**8. Q: What is a compound index?**
*   **A:** A compound index is an index on multiple fields. The order of fields in a compound index is very important. For example, an index on `{ "userId": 1, "score": -1 }` can efficiently support queries that filter on `userId` and then sort by `score`.

**9. Q: What is the aggregation pipeline?**
*   **A:** The aggregation pipeline is a powerful framework for performing data aggregation and analysis. It processes documents through a multi-stage pipeline where the output of one stage becomes the input for the next. Common stages include `$match` (filtering), `$group` (grouping), `$sort` (sorting), and `$project` (reshaping documents).

**10. Q: What is the purpose of the `$lookup` stage in the aggregation pipeline?**
*   **A:** The `$lookup` stage is used to perform the equivalent of a **left outer join** from a relational database. It allows you to de-normalize data by pulling in documents from another collection within the same database to enrich the documents in your pipeline.

**11. Q: Explain the concept of "embedding" vs. "referencing" in MongoDB data modeling.**
*   **A:**
    *   **Embedding (Denormalization):** Involves storing related data within a single document. For example, including an array of `comments` directly inside a `post` document. This is good for "has-many" relationships where the data is frequently accessed together, as it reduces the need for separate queries.
    *   **Referencing (Normalization):** Involves storing related data in separate collections and linking them using references (like an `_id`). For example, a `post` document would store an array of `comment_ids`. This is better for "many-to-many" relationships or when the referenced data is very large or frequently updated independently.

**12. Q: What is sharding in MongoDB?**
*   **A:** Sharding is the process of horizontally scaling a database by distributing data across multiple servers (or "shards"). Each shard holds a subset of the collection's data. A router process (`mongos`) directs application queries to the appropriate shard(s). Sharding is used to handle very large datasets and high throughput operations that exceed the capacity of a single server.

**13. Q: What is a replica set?**
*   **A:** A replica set is a group of MongoDB servers that maintain the same data set, providing redundancy and high availability. It consists of one **primary** node that receives all write operations, and one or more **secondary** nodes that replicate the primary's data. If the primary node fails, an automatic failover process elects one of the secondaries to become the new primary.

**14. Q: What is the difference between sharding and replication?**
*   **A:**
    *   **Replication** copies the *same* data across multiple servers to provide high availability and data redundancy.
    *   **Sharding** splits a *different* subset of data across multiple servers to provide horizontal scalability for large datasets.
    A production MongoDB deployment typically uses **both**—each shard is itself a replica set.

**15. Q: What is a "covered query"?**
*   **A:** A covered query is a query that can be satisfied entirely using an index, without having to examine any documents. This is the most performant type of query because it avoids reading from the collection itself. For a query to be covered, all the fields in the query filter and the fields returned in the projection must be part of the same index.

**16. Q: How does MongoDB ensure atomicity and transactions?**
*   **A:**
    *   **Single-Document Atomicity:** Write operations on a single document are always atomic. This is the most common use case.
    *   **Multi-Document Transactions:** Since MongoDB 4.2, it supports multi-document ACID transactions similar to relational databases. You can perform a series of operations on multiple documents across multiple collections and then commit or abort them as a single atomic unit.

**17. Q: What is the "projection" in a MongoDB query?**
*   **A:** Projection refers to specifying which fields to include or exclude in the documents returned by a query. This is useful for limiting the amount of data sent over the network. You can specify inclusion (`{ field: 1 }`) or exclusion (`{ field: 0 }`).

**18. Q: What is GridFS?**
*   **A:** GridFS is a specification for storing and retrieving files that exceed the BSON document size limit of 16 MB. It works by breaking the file into smaller chunks and storing each chunk as a separate document in a dedicated collection, along with a metadata document that describes the file.

**19. Q: What is a write concern?**
*   **A:** A write concern describes the level of acknowledgement requested from MongoDB for write operations. You can specify that a write is successful after it has been written to the primary only, or after it has been replicated to a specified number of secondaries, providing a trade-off between performance and data durability.

**20. Q: What are TTL (Time-to-Live) indexes?**
*   **A:** A TTL index is a special single-field index that MongoDB can use to automatically remove documents from a collection after a certain amount of time. This is ideal for managing data that has a limited lifespan, such as session data, logs, or temporary user records.