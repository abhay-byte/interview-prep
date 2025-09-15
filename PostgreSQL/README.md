### **PostgreSQL: 20 Theoretical & Conceptual Questions**

**1. Q: What is PostgreSQL? What are its key features?**
*   **A:** PostgreSQL is a powerful, open-source, object-relational database management system (ORDBMS). Key features include:
    *   **ACID Compliance:** Strong adherence to Atomicity, Consistency, Isolation, and Durability, making it highly reliable for transactional systems.
    *   **Extensibility:** Users can define their own data types, functions, and operators.
    *   **Concurrency Control:** It uses Multi-Version Concurrency Control (MVCC) to handle simultaneous requests with minimal locking.
    *   **Advanced Data Types:** Native support for a wide range of data types, including JSON/JSONB, arrays, and geometric types.
    *   **Rich Feature Set:** Supports advanced SQL features like window functions, Common Table Expressions (CTEs), and full-text search.

**2. Q: What is the difference between a Relational Database (RDBMS) and an Object-Relational Database (ORDBMS)?**
*   **A:** An RDBMS (like MySQL) strictly follows the relational model, storing data in simple tables with rows and columns. An ORDBMS, like PostgreSQL, is a hybrid model. It includes all the features of an RDBMS but also incorporates object-oriented concepts like user-defined types, inheritance, and polymorphism, allowing for the storage of more complex data structures.

**3. Q: What is MVCC (Multi-Version Concurrency Control)?**
*   **A:** MVCC is PostgreSQL's mechanism for handling concurrency. Instead of using locks to prevent readers and writers from conflicting, PostgreSQL maintains multiple "versions" or snapshots of each data row. When a transaction starts, it is given a snapshot of the database at that moment. This allows read operations to proceed without being blocked by write operations, leading to significantly higher concurrency.

**4. Q: What is the purpose of `VACUUM` in PostgreSQL?**
*   **A:** Due to MVCC, when a row is updated or deleted, the old version of the row is not immediately removed; it's just marked as "dead" and invisible to new transactions. The `VACUUM` command is a maintenance process that reclaims the storage occupied by these dead rows. It also updates data statistics used by the query planner and helps prevent transaction ID wraparound.

**5. Q: What is the difference between `JSON` and `JSONB` data types?**
*   **A:**
    *   `JSON`: Stores an exact, plain-text copy of the input JSON. It is faster to write but slower to process because the text must be parsed for every operation.
    *   `JSONB`: Stores the JSON in a decomposed binary format. It is slower to write (due to the conversion) but significantly faster to query and process because it supports indexing. In general, **`JSONB` is the preferred choice** for most applications.

**6. Q: What is an index, and what are the most common types of indexes in PostgreSQL?**
*   **A:** An index is a database structure that improves the speed of data retrieval operations on a table, at the cost of slower writes. The most common types are:
    *   **B-Tree:** The default and most widely used index. It is excellent for equality (`=`) and range (`<`, `>`, `BETWEEN`) queries on sortable data.
    *   **Hash:** Can only handle simple equality comparisons (`=`). They are generally not recommended over B-Trees.
    *   **GIN (Generalized Inverted Index):** Ideal for indexing composite values where elements can appear multiple times, such as arrays, full-text search documents (`tsvector`), and `JSONB`.
    *   **GiST (Generalized Search Tree):** A versatile index for more complex data types like geometric data and full-text search.

**7. Q: What is a transaction?**
*   **A:** A transaction is a single logical unit of work that consists of one or more SQL statements. Transactions are defined by the ACID properties. They begin with a `BEGIN` statement and end with either a `COMMIT` (to make the changes permanent) or a `ROLLBACK` (to undo all changes).

**8. Q: What are Transaction Isolation Levels in PostgreSQL?**
*   **A:** Isolation levels control the degree to which a transaction is protected from the effects of other concurrent transactions. The standard levels supported by PostgreSQL are:
    *   **Read Uncommitted:** (Implemented as `Read Committed` in PostgreSQL).
    *   **Read Committed:** The default level. A statement can only see rows that were committed before it began.
    *   **Repeatable Read:** Guarantees that if a transaction reads a row multiple times, it will see the same data. It can lead to serialization failures.
    *   **Serializable:** The strictest level. It guarantees that transactions will have the same effect as if they were run one after another, serially.

**9. Q: What is a Common Table Expression (CTE)?**
*   **A:** A CTE, defined using the `WITH` clause, allows you to create a temporary, named result set that you can reference within a larger `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement. CTEs are very useful for breaking down complex queries into simpler, more readable logical steps and for writing recursive queries.

**10. Q: What are Window Functions?**
*   **A:** Window functions perform a calculation across a set of table rows that are somehow related to the current row. Unlike aggregate functions, which group rows into a single output row, window functions perform the calculation for each row and do not collapse the result set. They are defined using the `OVER()` clause and are used for tasks like ranking, calculating running totals, and moving averages.

**11. Q: What is the difference between a Primary Key and a Foreign Key?**
*   **A:**
    *   **Primary Key:** A constraint that uniquely identifies each record in a table. It must contain unique values and cannot contain `NULL` values.
    *   **Foreign Key:** A key used to link two tables together. It is a field in one table that refers to the Primary Key in another table, enforcing referential integrity.

**12. Q: Explain the difference between `DELETE`, `TRUNCATE`, and `DROP`.**
*   **A:**
    *   `DELETE`: A DML command that removes rows from a table based on a `WHERE` clause. It is slow (logs each row deletion) and can be rolled back.
    *   `TRUNCATE`: A DDL command that quickly removes *all* rows from a table. It is much faster than `DELETE`, cannot be easily rolled back, and resets identity columns.
    *   `DROP`: A DDL command that completely removes the table itself, including its structure, data, and indexes.

**13. Q: What is a partial index?**
*   **A:** A partial index is an index built over a subset of a table's rows, defined by a `WHERE` clause. This is useful for improving performance and saving space when you only ever query a specific, small subset of the table. For example, indexing only `active` users: `CREATE INDEX ON users (id) WHERE status = 'active'`.

**14. Q: What is a connection pool?**
*   **A:** A connection pool is a cache of database connections maintained so that the connections can be reused for future requests. Establishing a new database connection is an expensive operation. A connection pool significantly improves the performance and scalability of an application by reusing a set of warm connections instead of creating a new one for every request.

**15. Q: What is a sequence in PostgreSQL?**
*   **A:** A sequence is a special kind of database object that generates a sequence of integers. They are commonly used to generate unique primary key values for new rows, typically via the `SERIAL` or `BIGSERIAL` pseudo-types, which automatically create a sequence and link it to the column.

**16. Q: What is the purpose of the `EXPLAIN` command?**
*   **A:** The `EXPLAIN` command shows the **execution plan** that the PostgreSQL query planner generates for a given SQL statement. It details how the tables will be scanned (e.g., sequential scan vs. index scan), the join algorithms used, and the estimated cost of the query. Using `EXPLAIN ANALYZE` executes the query and shows the actual time and rows, which is invaluable for diagnosing and optimizing slow queries.

**17. Q: What is table partitioning?**
*   **A:** Partitioning is the process of splitting one large logical table into smaller physical pieces called partitions. This is typically done for very large tables (VLDBs) to improve query performance (by scanning only relevant partitions) and simplify maintenance (like dropping old data). PostgreSQL supports partitioning by range, list, and hash.

**18. Q: What is a schema in PostgreSQL?**
*   **A:** A schema is a namespace that contains named database objects like tables, views, and functions. It allows you to group objects for organizational purposes and to avoid naming conflicts. By default, objects are created in the `public` schema.

**19. Q: What is the write-ahead log (WAL)?**
*   **A:** The WAL is a fundamental component of PostgreSQL's reliability and durability. Before any change is made to the actual data files (the "heap"), PostgreSQL first writes a record of the change to the WAL file on disk. This ensures that even if the server crashes before the changes are written to the main data files, the database can be recovered to a consistent state by replaying the WAL.

**20. Q: Differentiate between `UNION` and `UNION ALL`.**
*   **A:** Both operators combine the result sets of two or more `SELECT` statements.
    *   `UNION`: Removes duplicate rows from the final result set.
    *   `UNION ALL`: Includes all rows from all queries, including any duplicates.
    `UNION ALL` is significantly faster because it doesn't need to perform the extra work of identifying and removing duplicates.