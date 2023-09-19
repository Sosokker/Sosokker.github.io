## SQL Clauses for Data Manipulation

#### WHERE

The `WHERE` clause filters rows based on specified conditions.

**Use Case**: Retrieving specific rows that meet certain criteria.

```sql
SELECT * FROM employees WHERE salary > 50000;
```

#### SET

The `SET` clause is used in conjunction with `UPDATE` to specify new values for columns.

**Use Case**: Modifying specific columns with new values.

```sql
UPDATE employees SET salary = salary * 1.1 WHERE department_id = 3;
```

#### VALUES

The `VALUES` clause is used with `INSERT INTO` to specify values for new rows.

**Use Case**: Inserting new records with specific column values.

```sql
INSERT INTO products (product_name, price) VALUES ('New Product', 49.99);
```
## SQL Clauses for Data Retrieval
#### FROM

The `FROM` clause specifies the table or tables from which data is retrieved.

**Use Case**: Indicating the source tables for data retrieval.

```sql
SELECT order_id, order_date FROM orders;
```
## SQL Clauses for Aggregation

#### GROUP BY

The `GROUP BY` clause groups rows based on specified columns.

**Use Case**: Aggregating data and performing calculations on grouped data.

```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;
```

#### HAVING

The `HAVING` clause filters grouped results based on conditions.

**Use Case**: Filtering results of grouped data based on aggregated values.

```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;
```
## SQL Clauses for Sorting and Limiting

#### ORDER BY

The `ORDER BY` clause sorts the result set based on specified columns.

**Use Case**: Sorting query results in ascending or descending order.

```sql
SELECT product_name, price FROM products ORDER BY price DESC;
```
#### LIMIT

The `LIMIT` clause restricts the number of rows returned by a query.

**Use Case**: Fetching a limited number of rows for pagination or top-N queries.

```sql
SELECT customer_name FROM customers LIMIT 10;
```