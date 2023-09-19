
# SQL Functions for Data Manipulation
## Mathematical Functions

#### SUM
The `SUM` function calculates the sum of values in a column.

**Use Case**: Calculating the total sales amount.
```sql
SELECT SUM(order_amount) FROM orders;
```
#### AVG

The `AVG` function calculates the average of values in a column.

**Use Case**: Finding the average salary of employees.

```sql
SELECT AVG(salary) FROM employees;
```
## String Functions

#### CONCAT

The `CONCAT` function concatenates two or more strings.

**Use Case**: Combining first and last names into a full name.

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM employees;
```

#### UPPER and LOWER

The `UPPER` function converts a string to uppercase, and `LOWER` converts it to lowercase.

**Use Case**: Changing the case of text data.

```sql
SELECT UPPER(product_name) FROM products;
```

# SQL Functions for Data Transformation

## Date and Time Functions

#### DATE_FORMAT

The `DATE_FORMAT` function formats a date or time value according to a specified format.

**Use Case**: Displaying dates in a customized format.

```sql
SELECT DATE_FORMAT(order_date, '%Y-%m-%d') AS formatted_date FROM orders;
```

## Case Functions

#### CASE

The `CASE` function performs conditional logic within a query.

**Use Case**: Categorizing order amounts into 'High', 'Medium', or 'Low'.

```sql
SELECT order_amount,
       CASE
           WHEN order_amount > 1000 THEN 'High'
           WHEN order_amount > 500 THEN 'Medium'
           ELSE 'Low'
       END AS amount_category
FROM orders;
```

## SQL Functions for Aggregation

#### COUNT

The `COUNT` function calculates the number of rows or non-NULL values in a column.

**Use Case**: Counting the number of orders placed by customers.

```sql
SELECT customer_id, COUNT(order_id) AS order_count FROM orders GROUP BY customer_id;
```

#### MIN and MAX

The `MIN` function returns the smallest value, and `MAX` returns the largest value in a column.

**Use Case**: Finding the earliest and latest order dates.

```sql
SELECT MIN(order_date) AS earliest_date, MAX(order_date) AS latest_date
FROM orders;
```