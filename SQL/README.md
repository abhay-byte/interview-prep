### SQL Questions

### **Part 1: Conceptual SQL & DBMS Questions**

**1. Q: What are the main sub-languages of SQL?**
*   **A:**
    *   **DDL (Data Definition Language):** Defines the database schema. Commands: `CREATE`, `ALTER`, `DROP`, `TRUNCATE`.
    *   **DML (Data Manipulation Language):** Manipulates data within tables. Commands: `SELECT`, `INSERT`, `UPDATE`, `DELETE`.
    *   **DCL (Data Control Language):** Manages user access and permissions. Commands: `GRANT`, `REVOKE`.
    *   **TCL (Transaction Control Language):** Manages transactions. Commands: `COMMIT`, `ROLLBACK`, `SAVEPOINT`.

**2. Q: What is the difference between a `PRIMARY KEY` and a `UNIQUE KEY`?**
*   **A:** Both enforce uniqueness for a column. However, a table can have only **one** `PRIMARY KEY`, which cannot contain `NULL` values. A table can have **multiple** `UNIQUE KEY` constraints, and they can accept one `NULL` value.

**3. Q: What is a `FOREIGN KEY`?**
*   **A:** A `FOREIGN KEY` is a key used to link two tables together. It is a field (or collection of fields) in one table that refers to the `PRIMARY KEY` in another table. This enforces referential integrity, ensuring relationships between tables remain consistent.

**4. Q: What is database normalization?**
*   **A:** Normalization is the process of organizing tables and columns in a relational database to minimize data redundancy and improve data integrity. It involves dividing larger tables into smaller, well-structured tables and defining relationships between them.

**5. Q: Briefly explain 1NF, 2NF, and 3NF.**
*   **A:**
    *   **1NF (First Normal Form):** Ensures that table cells hold atomic (indivisible) values and each row is unique (has a primary key).
    *   **2NF (Second Normal Form):** Must be in 1NF. All non-key attributes must be fully dependent on the entire primary key (this applies to composite keys).
    *   **3NF (Third Normal Form):** Must be in 2NF. There should be no transitive dependencies, meaning non-key attributes cannot depend on other non-key attributes.

**6. Q: What are the ACID properties of a transaction?**
*   **A:**
    *   **Atomicity:** The entire transaction either completes successfully or fails completely (is rolled back).
    *   **Consistency:** The transaction moves the database from one valid state to another.
    *   **Isolation:** Concurrent transactions do not interfere with each other, producing the same result as if they were run serially.
    *   **Durability:** Once a transaction is committed, its changes are permanent and survive system failures.

**7. Q: What is a database index?**
*   **A:** An index is a special lookup table that the database search engine can use to speed up data retrieval. It works like an index in a book. By indexing a column, you create a data structure (commonly a B-Tree) that allows for faster searching on that column at the cost of slower writes (`INSERT`, `UPDATE`).

**8. Q: What is the difference between a Clustered and a Non-Clustered Index?**
*   **A:** A **Clustered Index** determines the physical order of data in a table. Because of this, a table can only have one clustered index. A **Non-Clustered Index** has a separate structure from the data rows which points back to them. A table can have multiple non-clustered indexes.

**9. Q: Explain the difference between `INNER JOIN` and `LEFT JOIN`.**
*   **A:**
    *   `INNER JOIN`: Returns only the rows where the join condition is met in **both** tables.
    *   `LEFT JOIN`: Returns **all** rows from the left table, and the matched rows from the right table. If there is no match in the right table, the result is `NULL` for columns from the right table.

**10. Q: Differentiate `DELETE`, `TRUNCATE`, and `DROP`.**
*   **A:**
    *   `DELETE`: A DML command that removes rows from a table one by one. It is slow, can be rolled back, and triggers `DELETE` triggers. A `WHERE` clause can be used.
    *   `TRUNCATE`: A DDL command that quickly removes all rows from a table by deallocating the data pages. It is fast, cannot be rolled back (in most systems), and does not fire triggers.
    *   `DROP`: A DDL command that completely removes the table's structure, data, and indexes from the database.

**11. Q: When do you use `GROUP BY` and `HAVING`?**
*   **A:** The `GROUP BY` clause is used with aggregate functions (`COUNT`, `SUM`, `AVG`, etc.) to group rows that have the same values in specified columns. The `HAVING` clause is then used to filter these groups based on the results of the aggregate function. `WHERE` filters rows *before* aggregation; `HAVING` filters groups *after* aggregation.

**12. Q: What is the difference between `UNION` and `UNION ALL`?**
*   **A:** Both combine the result sets of two or more `SELECT` statements. `UNION` removes duplicate rows from the final result set. `UNION ALL` includes all rows, including duplicates. `UNION ALL` is significantly faster as it doesn't need to check for duplicates.

---

### **Part 2: 20 Practical SQL Queries**

*Assume the following schema for all questions:*

*   **Employees**(`emp_id`, `emp_name`, `salary`, `dept_id`, `manager_id`)
*   **Departments**(`dept_id`, `dept_name`)

**1. Select all employees who work in the 'Sales' department.**
```sql
SELECT * FROM Employees e
JOIN Departments d ON e.dept_id = d.dept_id
WHERE d.dept_name = 'Sales';
```

**2. List the names of all employees who have a salary greater than 60,000.**
```sql
SELECT emp_name FROM Employees WHERE salary > 60000;
```

**3. Count the number of employees in each department.**
```sql
SELECT d.dept_name, COUNT(e.emp_id) AS number_of_employees
FROM Employees e
JOIN Departments d ON e.dept_id = d.dept_id
GROUP BY d.dept_name;
```

**4. Find the average salary for each department.**
```sql
SELECT d.dept_name, AVG(e.salary) AS average_salary
FROM Employees e
JOIN Departments d ON e.dept_id = d.dept_id
GROUP BY d.dept_name;
```

**5. Find departments that have more than 5 employees.**
```sql
SELECT d.dept_name
FROM Employees e
JOIN Departments d ON e.dept_id = d.dept_id
GROUP BY d.dept_name
HAVING COUNT(e.emp_id) > 5;
```

**6. Find the name of each employee along with their manager's name.**
```sql
SELECT e1.emp_name AS employee_name, e2.emp_name AS manager_name
FROM Employees e1
LEFT JOIN Employees e2 ON e1.manager_id = e2.emp_id;
```

**7. Find the second highest salary in the Employees table.**
```sql
SELECT MAX(salary) FROM Employees
WHERE salary < (SELECT MAX(salary) FROM Employees);
```

**8. List all departments that have no employees.**
```sql
SELECT d.dept_name
FROM Departments d
LEFT JOIN Employees e ON d.dept_id = e.dept_id
WHERE e.emp_id IS NULL;
```

**9. Find all employees who have the same salary.**
```sql
SELECT e1.emp_name, e1.salary
FROM Employees e1
JOIN Employees e2 ON e1.salary = e2.salary AND e1.emp_id != e2.emp_id;
```

**10. Select the top 3 highest-paid employees.**
```sql
SELECT emp_name, salary FROM Employees
ORDER BY salary DESC
LIMIT 3;
```

**11. Find all employees who do not have a manager.**
```sql
SELECT emp_name FROM Employees WHERE manager_id IS NULL;
```

**12. Get the department with the highest total salary expenditure.**
```sql
SELECT d.dept_name
FROM Employees e
JOIN Departments d ON e.dept_id = d.dept_id
GROUP BY d.dept_name
ORDER BY SUM(e.salary) DESC
LIMIT 1;
```

**13. List employees who earn more than the average salary of their respective departments.**
```sql
SELECT e.emp_name, e.salary, d.dept_name
FROM Employees e
JOIN (
    SELECT dept_id, AVG(salary) as avg_sal
    FROM Employees
    GROUP BY dept_id
) AS dept_avg ON e.dept_id = dept_avg.dept_id
WHERE e.salary > dept_avg.avg_sal;
```

**14. Find the third highest salary using a window function.**
```sql
WITH SalaryRanks AS (
    SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) as rnk
    FROM Employees
)
SELECT salary FROM SalaryRanks WHERE rnk = 3 LIMIT 1;
```

**15. List the employees who are also managers.**
```sql
SELECT DISTINCT e2.emp_name
FROM Employees e1
JOIN Employees e2 ON e1.manager_id = e2.emp_id;
```

**16. Find the cumulative salary for each employee within their department, ordered by salary.**
```sql
SELECT emp_name, salary, dept_name,
       SUM(salary) OVER (PARTITION BY d.dept_name ORDER BY salary) AS cumulative_salary
FROM Employees e
JOIN Departments d ON e.dept_id = d.dept_id;```

**17. Find the employee who has the highest salary in each department.**
```sql
WITH RankedEmployees AS (
    SELECT e.emp_name, e.salary, d.dept_name,
           RANK() OVER (PARTITION BY d.dept_name ORDER BY e.salary DESC) as rnk
    FROM Employees e
    JOIN Departments d ON e.dept_id = d.dept_id
)
SELECT emp_name, salary, dept_name
FROM RankedEmployees WHERE rnk = 1;
```

**18. Delete all employees from the 'Marketing' department.**
```sql
DELETE FROM Employees
WHERE dept_id = (SELECT dept_id FROM Departments WHERE dept_name = 'Marketing');
```

**19. Update the salary of all employees in the 'Engineering' department by 10%.**
```sql
UPDATE Employees
SET salary = salary * 1.10
WHERE dept_id = (SELECT dept_id FROM Departments WHERE dept_name = 'Engineering');
```

**20. Find duplicate email addresses in a `Customers` table (assuming `email` column).**
```sql
SELECT email, COUNT(email)
FROM Customers
GROUP BY email
HAVING COUNT(email) > 1;
```