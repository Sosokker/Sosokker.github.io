Consider a table named `products` with the following structure:

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10, 2)
);
```

Let's say you have a query to retrieve all products in a specific category:

```sql
SELECT * FROM products WHERE category = 'Electronics';
```

Without an index on the `category` column, the database would need to scan the entire table to find the matching rows. As the table grows, this can lead to slower query performance.

To optimize this query, you can create an index on the `category` column:

```sql
CREATE INDEX idx_category ON products (category);
```

With the index in place, the database can quickly locate the rows that match the 'Electronics' category, resulting in faster query execution.

It's important to note that while indexes improve read performance, they also have some trade-offs. Indexes consume additional storage space and can slightly slow down write operations (such as INSERT, UPDATE, and DELETE). Therefore, it's essential to consider the balance between read and write operations when deciding which columns to index.