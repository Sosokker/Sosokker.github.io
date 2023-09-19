# Summary of Commonly Used SQL Operators

| Operator   | Description                                       | Example                   |
|------------|---------------------------------------------------|---------------------------|
| Comparison |                                                   |                           |
| =          | Equal                                             | `price = 50.00`           |
| !=         | Not Equal                                         | `department_id != 3`      |
| <          | Less Than                                         | `salary < 50000`          |
| >          | Greater Than                                      | `price > 100.00`          |
| Logical    |                                                   |                           |
| AND        | Logical AND (all conditions must be true)        | `cond1 AND cond2`         |
| OR         | Logical OR (at least one condition must be true) | `cond1 OR cond2`          |
| NOT        | Logical NOT (negates a condition)                | `NOT condition`           |
| Arithmetic |                                                   |                           |
| +          | Addition                                          | `SUM(amount) + tax`       |
| -          | Subtraction                                       | `revenue - expenses`      |
| *          | Multiplication                                   | `quantity * unit_price`   |
| /          | Division                                          | `SUM(salary) / COUNT(*)`  |
| Concatenation |                                              |                           |
| ||         | String Concatenation                             | `first_name || ' ' || last_name` |
| IN         | Membership (value in a list)                     | `customer_id IN (1, 2, 3)` |
| LIKE       | Pattern Matching                                 | `product_name LIKE '%Phone%'` |