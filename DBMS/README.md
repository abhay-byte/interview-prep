### **Database Management Systems (DBMS): 10 Theoretical Questions**

**1. Q: What are transaction isolation levels, and why are they necessary?**
*   **A:** Transaction isolation levels define the degree to which one transaction must be isolated from the data modifications made by any other concurrently running transaction. They are necessary to manage the trade-off between data consistency and performance. The standard levels are (from least to most strict): `Read Uncommitted`, `Read Committed`, `Repeatable Read`, and `Serializable`. Stricter levels prevent concurrency issues (like dirty reads, non-repeatable reads, and phantom reads) but can reduce system throughput.

**2. Q: How does a B-Tree index work at a high level, and why is it so effective for databases?**
*   **A:** A B-Tree is a self-balancing tree data structure that keeps data sorted and allows for efficient insertion, deletion, and searching. It is effective for databases because it is optimized for systems that read and write large blocks of data. Its "bushy" structure with a high branching factor minimizes the number of disk I/O operations required to locate a specific row, which is the primary bottleneck in database performance.

**3. Q: What is the role of a query optimizer?**
*   **A:** A query optimizer is a component of a DBMS that analyzes an SQL query and determines the most efficient "execution plan" to retrieve the requested data. It considers various factors, such as available indexes, table statistics (like size and data distribution), and different join algorithms (`Hash Join`, `Merge Join`, `Nested Loop`). Its goal is to to minimize the total resources (CPU, I/O, time) needed to execute the query.

**4. Q: What is the fundamental difference between SQL (Relational) and NoSQL databases?**
*   **A:** The fundamental difference lies in their data model and consistency guarantees. **SQL databases** use a structured schema with tables, rows, and columns, enforcing rigid data consistency (ACID properties). They are ideal for complex, query-intensive applications. **NoSQL databases** use a variety of flexible data models (document, key-value, graph) and typically prioritize availability and scalability over strict consistency (often following the BASE model), making them suitable for large-scale, unstructured data.

**5. Q: What is Multi-Version Concurrency Control (MVCC)?**
*   **A:** MVCC is a concurrency control method where the database creates a new version of a data item each time it is written to, rather than overwriting it in place. When a transaction reads a data item, the database shows it a "snapshot" or version of that item as it existed at the start of the transaction. This allows read operations to proceed without being blocked by write operations, significantly improving performance in read-heavy systems.

**6. Q: What is the difference between a materialized view and a standard view?**
*   **A:** A **standard view** is a stored virtual table that is generated dynamically when queried. It contains no data itself; it is simply a pre-defined `SELECT` statement. A **materialized view** is a physical copy of the data from the underlying query. The data is stored on disk and must be periodically refreshed. Materialized views provide much faster query performance for complex aggregations but consume storage and can have stale data.

**7. Q: Explain the CAP Theorem for distributed databases.**
*   **A:** The CAP Theorem states that it is impossible for a distributed data store to simultaneously provide more than two out of the following three guarantees:
    *   **Consistency:** Every read receives the most recent write or an error.
    *   **Availability:** Every request receives a (non-error) response, without the guarantee that it contains the most recent write.
    *   **Partition Tolerance:** The system continues to operate despite network partitions (messages being dropped between nodes).
    In modern systems, partition tolerance is a necessity, so designers must choose between strong consistency (CP systems like Google Spanner) and high availability (AP systems like Cassandra).

**8. Q: Why and when would you use denormalization?**
*   **A:** **Denormalization** is the process of intentionally adding redundant data to a database to improve read performance. While normalization reduces redundancy to improve data integrity, it often requires complex joins that can be slow. Denormalization is used in read-heavy systems (like data warehouses) where query speed is more critical than data consistency and storage efficiency.

**9. Q: What are the differences between OLTP and OLAP systems?**
*   **A:**
    *   **OLTP (Online Transaction Processing):** Designed for a large number of short, fast transactions (e.g., ATM, e-commerce). It is highly normalized, optimized for write operations (`INSERT`, `UPDATE`), and deals with current, operational data.
    *   **OLAP (Online Analytical Processing):** Designed for a low volume of complex analytical queries (e.g., business intelligence reports). It uses denormalized, aggregated, historical data and is optimized for fast read operations on large datasets.

**10. Q: Differentiate between database partitioning and sharding.**
*   **A:** Both are ways to break up a large database into smaller pieces.
    *   **Partitioning** is when you split a large table into smaller tables *within the same database instance*. This is often done to improve query performance or manageability (e.g., partitioning a logs table by date).
    *   **Sharding** is when you split the data across *multiple database instances* (servers). This is a horizontal scaling strategy used when a single server can no longer handle the load.