# Day 15 — SQL: Relational Thinking

## Topics Learned
- Primary Key
- Foreign Key
- One-to-Many Relationships
- Why databases use multiple tables
- Identifying relationships between Customers, Orders and Products tables

## Key Concepts

### 1. Primary Key
A Primary Key uniquely identifies each record in a table. It cannot contain duplicate or NULL values.

Example: `CustomerID` in the Customers table.

### 2. Foreign Key
A Foreign Key connects one table to another table by referencing its key.

Example: `CustomerID` in the Orders table.

### 3. One-to-Many Relationship
One customer can place multiple orders.

Example:
- Customer 101 → Order 501
- Customer 101 → Order 503

### 4. Why Multiple Tables?
Multiple tables help:
- Reduce duplicate data.
- Organise information.
- Maintain data consistency.
- Establish relationships between records.

## Practice Tables

| Table | Primary Key | Foreign Key |
|---|---|---|
| Customers | CustomerID | None |
| Orders | OrderID | CustomerID, ProductID |
| Products | ProductID | None |

## What I Learned
I understood how relational databases organise information using primary keys and foreign keys. I also learned how multiple tables are connected through relationships.

**Day 15 Status:** Completed
