
## Data Retrieval Statements
#### SELECT
*Retrieve data* from tables based on conditions.
```sql
SELECT customer_name FROM customers;
```

![[Join-Diagram.png | center | 500]]
#### JOIN
*Combines data from multiple tables* based on *related columns*.
```sql
SELECT orders.order_id, customers.customer_name
FROM orders
JOIN customers ON orders.customer_id = customers.customer_id;
```

##### INNER JOIN
**return :** only rows where there is *match* in *both table* based on specific condition.

```sql
SELECT orders.order_id, customers.customer_name
FROM orders
INNER JOIN customers ON orders.customer_id = customers.customer_id;
```

##### LEFT JOIN (or LEFT OUTER JOIN)
**return :** all rows from the left table and matching rows from the right table.

If *no match* is found, **NULL** values are returned for columns from the right table.

```sql
SELECT customers.customer_name, orders.order_date
FROM customers
LEFT JOIN orders ON customers.customer_id = orders.customer_id;
```
##### RIGHT JOIN (or RIGHT OUTER JOIN)
**return:** all rows from the right table and matching rows from the left table. 

If no match is found, NULL values are returned for columns from the left table.

```sql
SELECT orders.order_id, order_details.product_id
FROM orders
RIGHT JOIN order_details ON orders.order_id = order_details.order_id;
```
##### FULL JOIN (or FULL OUTER JOIN)
**return:** all rows from both tables and combines matching rows. 

If no match is found, NULL values are returned for columns from the table without a match.

```sql
SELECT customers.customer_name, orders.order_id
FROM customers
FULL JOIN orders ON customers.customer_id = orders.customer_id;
```
##### CROSS JOIN
Produces a *Cartesian product* of rows from both tables.
Resulting in every possible combination of rows between the two tables.

```sql
SELECT employees.first_name, departments.department_name
FROM employees
CROSS JOIN departments;
```
![[cross-join-round.png | center | 400]]
## Data Modification Statements

#### INSERT INTO
*Add new rows* of data to a table
```sql
INSERT INTO orders (order_id, order_date, customer_id) VALUES (101, '2023-09-01', 123);
```
#### UPDATE
*Modifies existing records* in table
```sql
UPDATE employees SET salary = 60000 WHERE department_id = 3;
```

#### DELETE FROM
*Remove rows* from table
```sql
DELETE FROM orders WHERE order_date < '2023-01-01';
```

## Data Control Statements
#### CREATE TABLE
*Creates* a new table.
```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    email VARCHAR(255)
);
```
#### ALTER TABLE
*Modifies* an existing table's structure
```sql
ALTER TABLE employees ADD COLUMN birthdate DATE;
```
#### DROP TABLE
*Deletes* an existing table and its data.
```sql
DROP TABLE products;
```

#### CREATE INDEX
*Create an index* on one or more columns of a table
```sql
CREATE INDEX index_name
ON table_name (column1, column2, ...);
```