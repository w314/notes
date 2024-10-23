
# SQL Functions & Procedures

- callable block of code that takes in zero or more parameters and returns a value
- mainly used to perform and return calculations
- must RETURN value
- can be used as part of a SQL expression (since it returns a value)
- can include DQL and DML (and DDL but not used often in function)
- some are built-in and we can create our own
- to use a function use `SELECT`: `SELECT COUNT(*)...`
- Stored functions are very similar to stored procedures, except that a function returns a value to the environment in which it is called.


## SQL Functions
>A function in MySQL is a set of statements you can call by name.


### Scalar Functions
> A scalar function is a function that operates on scalar values. It takes one (or more) input values as arguments directly and returns a value.

- pre-defined functions in SQL
- operates on scalar values (not set of data)
- takes one or more input values as arguments
- output is always a single value

<br>
Most important scalar functions:

- `UCASE()` 
    - converts the value of a field to uppercase.
- `LCASE()` 
    - converts to lowercase
- `MID(string, start, number-of-characters-to-return)` 
    - returns substring
    - characters start with 1 (not 0 like with index)
- `LENGTH()`
- `ROUND(NumericalValue, Decimals)`
- `NOW()` 
    - returns the current system date and time
- `FORMAT(Value, Decimal)` 
    - rounds does not just cuts the digits

```sql
SELECT MID ("Hello World", 4, 8);
-- returns:"lo World"

SELECT ROUND(135.375, 2);
-- returns 135.38
SELECT ROUND(135.375, -1);
-- returns 140

SELECT FORMAT(250500.5664, 2);
-- returns 250,500.57
```


### Aggregate Functions
> An aggregate function is a function takes a complete set of data as input and returns a value that is computed from all the values in the set.

- retrieves a single value after performing a calculation on a set of values.
- In general, aggregate functions ignore null values.
- `GROUP BY` is used to group data based on the exact value in a specific field
    - groups rows that have the same values into summary rows
    - have to be used with aggregate functions like `COUNT`, `MAX`
- `HAVING` is used to filter out groups that meet a condition

Most important aggregate functions:

- `COUNT()` 
    - returns the number of rows
    - includes rows with NULL values
- `SUM()` 
    - returns the total summed values in a set 
- `AVG()` 
    - returns the average value
- `MIN()` 
    - returns the minimum (lowest) value in a set
- `MAX()` 
    - returns the maximum (highest) value in a set

```sql
-- get the minimum salary
SELECT MIN(salary) FROM employee;

-- list all departments and their employee counts 
-- where the department has at list 5 employees
SELECT department, COUNT(*) as employee_count
FROM employee
GROUP BY department
HAVING COUNT(*) > 5;
```


### Sequence (Not Creatable in MySQL)

A sequence is a user-defined schema bound object that produces a sequence of numeric values.

- database object that generates a series of integer values
- starting value must be positive
- increment can be custom

The `AUTO_INCREMENT` column attribute provides unique numbers in MySQL.

- AUTO_INCREMENT sequences start with 1 by default
- only one column per table can have this attribute

#### Sequence Syntax

```sql
CREATE SEQUENCE schema_name.sequence_name [OR] sequence_name
START WITH initial_value
INCREMENT BY increment_value
MINVALUE min_value
MAXVALUE max_value
CYCLE|NOCYCLE ;
```

- sequence_name: Name of the sequence.

- initial_value: starting value from where the sequence starts. Initial_value should be greater than or equal to minimum value and less than equal to maximum value.

- increment_value: Value by which sequence will increment itself. Increment_value can be positive or negative.

- minimum_value: Minimum value of the sequence.

- maximum_value: Maximum value of the sequence.

- cycle: When sequence reaches its set_limit it starts from beginning.

- nocycle: An exception will be thrown if sequence exceeds its max_value.

Example

```sql
CREATE SEQUENCE example_1 AS INT START WITH 10 INCREMENT BY 10;

CREATE SEQUENCE example_2 start with 100 increment by -1 minvalue 1 maxvalue 100 cycle;
```

## Questions

- What is a function in SQL?
- What is the difference between an aggregate and a scalar function?
- What are some aggregate functions and scalar functions in SQL? 
- What is a Stored Procedure? 
- What is a Trigger? 
- What is a Sequence? 
