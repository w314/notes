sql, index

# Index

> A database object. Used to quickly locate and access data in a database without having to serach every row.


## Key Characteristics
- performance improvement
- storage overhead
    - require additional storage space
    - to maintein the index data structure
- maintenance overhead
    - indexes need to be updated when data is modified

## Syntax

```sql
-- table
CREATE TABLE Employee (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);

-- create index on table
CREATE INDEX idx_employee_name ON Employee (name);

-- drop index
DROP INDEX idx_employee_name;
```