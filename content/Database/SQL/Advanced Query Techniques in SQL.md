## 1. Subqueries

A subquery, also known as a nested query, is a query nested within another query. It allows you to perform operations based on the results of another query. Subqueries are used within conditions like `IN`, `EXISTS`, or directly in the `SELECT` clause.

Example: Find customers who have placed orders in the last month.

```sql
SELECT customer_name
FROM customers
WHERE customer_id IN (SELECT customer_id FROM orders WHERE order_date >= DATEADD(MONTH, -1, GETDATE()));
```

Example: Find Student with highest GPA

```sql
SELECT sName
FROM Student C1
WHERE not exists (SELECT * FROM Student C2
				 WHERE C2.GPA > C1.GPA);
```
NOTE: Get name of student that not exist in rank of all student. -> Get highest GPA

exist in C2.GPA > C1.GPA mean that 
## 2. Joins

Joins are used to combine data from multiple tables based on related columns. They enable you to retrieve data that exists in one or more tables and create a coherent result set.

Example: Retrieve order details along with customer names.

```sql
SELECT o.order_id, o.order_date, c.customer_name
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id;
```

## 3. Aggregation with GROUP BY

The `GROUP BY` clause is used to group rows that have the same values in specified columns. Aggregation functions like `SUM`, `AVG`, `COUNT`, etc., can then be applied to each group.

Example: Calculate the total order amount for each customer.

```sql
SELECT customer_id, SUM(order_amount) AS total_amount
FROM orders
GROUP BY customer_id;
```

## 4. Window Functions

Window functions perform calculations across a set of table rows related to the current row. They're commonly used for tasks like ranking, cumulative sums, and moving averages.
### Syntax

```sql
<window_function> (<column> [OVER <window_specification>])
```

Example: Rank products based on sales in descending order.

```sql
SELECT product_name, order_date, order_amount,
       RANK() OVER (ORDER BY order_amount DESC) AS sales_rank
FROM order_details;
```


| Window Function    | Description                                                 |
|--------------------|-------------------------------------------------------------|
| ROW_NUMBER()       | Assigns a unique row number to each row within a result set.|
| RANK()             | Assigns a unique rank to each distinct row, with gaps.     |
| DENSE_RANK()       | Assigns a rank to each distinct row, without gaps.          |
| NTILE(n)           | Divides result set into "n" buckets, assigns bucket number. |
| LAG(column, n)     | Accesses value of a column in the "n"th previous row.      |
| LEAD(column, n)    | Accesses value of a column in the "n"th next row.          |
| FIRST_VALUE()      | Returns value of a column


## 5. Common Table Expressions (CTEs)

CTEs provide a way to define temporary result sets that can be referenced within a query. They enhance readability and allow for modular query construction.

### Syntax

```sql
WITH cte_name (column1, column2, ...) AS (
    -- CTE query
)
SELECT * FROM cte_name;
```

Example: Find customers who have made multiple orders.

```sql
WITH CustomerOrders AS (
    SELECT customer_id, COUNT(order_id) AS order_count
    FROM orders
    GROUP BY customer_id
)
SELECT c.customer_name
FROM customers c
JOIN CustomerOrders co ON c.customer_id = co.customer_id
WHERE co.order_count > 1;
```

Example: the Recursive CTE (`WITH RECURSIVE`) is used to find the hierarchy of employees based on manager-subordinate relationships.

```sql
WITH RECURSIVE EmployeeHierarchy AS (
    SELECT employee_id, first_name, manager_id
    FROM employees
    WHERE manager_id IS NULL
    UNION ALL
    SELECT e.employee_id, e.first_name, e.manager_id
    FROM employees e
    JOIN EmployeeHierarchy eh ON e.manager_id = eh.employee_id
)
SELECT * FROM EmployeeHierarchy;
```


| CTE Name           | Description                                                |
|--------------------|------------------------------------------------------------|
| EmployeeHierarchy  | Recursive CTE to find the employee hierarchy.              |
| MonthlySales       | CTE to calculate monthly sales totals.                    |
| TopPerformers      | CTE to identify top-performing employees based on metrics. |
| OrderSummary       | CTE to create a summary of order data.                    |
| SubcategorySales   | CTE to analyze sales data for product subcategories.      |

## 6. Conditional Logic

Use `CASE` statements to introduce conditional logic within your queries. This allows you to perform different operations based on specific conditions.

Example: Categorize order amounts as 'High', 'Medium', or 'Low'.

```sql
SELECT order_id, order_amount,
       CASE
           WHEN order_amount > 1000 THEN 'High'
           WHEN order_amount > 500 THEN 'Medium'
           ELSE 'Low'
       END AS amount_category
FROM orders;
```