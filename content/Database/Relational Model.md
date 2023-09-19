## Components

#### Keys
They are one or more attributes that determine another attributes.

The role of keys is based on the concept of *determination*.

***Determination?***:
Know value of one attribute -> Possible to determine value of another.
Example: 
- (Math Determination) : revenue - cost = profit -> determine profit from cost and revenue.
- (Student Database): Giving Student_ID can determine Student_NAME

What are they use for?
- Used to ensure that each row in table is **uniquely identifiable**.
- Used to establish relationships among the table -> Ensure *integrity of data*.
	- Data integrity is the *overall accuracy, completeness, and consistency of data*
##### Type of Keys.
Before dive into type of key. Let see some buzz word in this section. 
1. Key Attribute: Attribute that is part of primary key.
2. Composite Key: Multiple-attribute key.
3. Superkey: Set of attribute that uniquely identify entity in table.

Let explore some types of key.
- Primary Key : One of more attributes that uniquely identify the rows.
- Foreign Key: Attribute in table used to define its relatioship with other table

**NOTE :** A primary key generally focuses on the uniqueness of the table. It assures the value in the specific column is unique. A foreign key is generally used to build a relationship between the two tables.

![[1 wr_PNTP9fQHxXeMydaSfnQ.png]]

## Relation Algebra
Defines the theoretical way of manipulating table contents using relation operator.

There are 8 main functions: 

SELECT, PROJECT, JOIN, INTERSECT, UNION, DIFFERENCE, PRODUCT, DIVIDE.

#### SELECT (RESTRICT)
Use one table as input -> Yield values for all rows found in table that satisfy given condition.

