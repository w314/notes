
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


## Stored Functions & Procedures

Must have `CREATE ROUTINE` privilige to create stored functions and stored procedures on the database.

### Stored Functions
> A set of SQL statements that perform a specific task and are stored on the server.

- it can be invoked using its name, like a method call
- can be used in SQL statements wherever an expression is used
- always returns a value


```sql
-- create stored procedure

-- set delimiter to // to avoid MySQl interpreting each ; as end of the function
DELIMITER //
CREATE FUNCTION calculate_total_price(order_id INT) RETURNS DECIMAL(10,2)
BEGIN
  DECLARE total_price DECIMAL(10,2);
  SELECT SUM(quantity * price) INTO total_price
  FROM order_items
  WHERE order_id = order_id;
  RETURN total_price;
END //
-- change delimiter back to ;
DELIMITER ;

-- call function
SELECT calculate_total_price(101);

-- delete function
DROP FUNCTION IF EXISTS calculate_total_price;
```

### Triggers


A trigger is a named SQL unit that is stored in the database and run in response to an event that occurs in the database or when there is a modification to the database.

- database object that activates when a particular event occurs on the table it is associated with
- a special kind of a store procedure that executes in response to certain action on the table like insertion, deletion or updation of data
- events are DML (insert, delete, update)
- You can specify the event, whether the trigger fires before or after the event, and whether the trigger runs for each event or for each row affected by the event.

The key difference between a `trigger` and `procedure`:

- a trigger is _called automatically_ when a data modification occurs in a table. A stored procedure must be invoked directly.
- Triggers have no chance of recieving parameters.
- A transaction cannot be committed or rolled back inside a trigger.

#### Types of Triggers:

- AFTER INSERT activated after data is inserted into the table.
- AFTER UPDATE: activated after data in the table is modified.
- AFTER DELETE: activated after data is deleted/removed from the table.
- BEFORE INSERT: activated before data is inserted into the table.
- BEFORE UPDATE: activated before data in the table is modified.
- BEFORE DELETE: activated before data is deleted/removed from the table.

#### Trigger Syntax

```sql
-- create trigger
CREATE TRIGGER [trigger_name] [BEFORE | AFTER]
{INSERT | UPDATE | DELETE}
ON [table_name]
[for each row]
[trigger_body]

-- delete trigger
DROP TRIGGER [IF EXISTS] trigger_name
```

Example:

```sql
CREATE TRIGGER student_grade
BEFORE INSERT
ON Student
for each row
SET Student.total = Student.subj1 + Student.subj2 + Student.subj3, Student.perc = Student.total * 50 / 100;
```

### Stored Procedures

> What is a stored procedure in SQL?

A stored procedure is a MySQL program that is stored inside a database schema and which can be invoked from within a MySQL program or SQL command.

- callable block of code that takes in parameters
- does not use a return statement
- can include DQL and DML (and DDL but not used often in function)
- can contain TCL
- `CallableStatement` is used in Java to call a stored procedure

- A stored procedure provides additional layer of security between the user interface and the database.
- It supports security through data access controls because end users may manipulate data, but doesn't write procedures.
- It offers advantages over embedding queries in a graphical user interface.

#### Stored Procedures vs. Functions

- Stored procedures and functions can be used to accomplish the same task.
- Both can be user-defined as part of any application,
- functions are defined to send their output to a query
- Stored procedures are designed to return outputs to the application
- a user-defined function returns table variables and cannot change the server environment or operating system environment.

### Procedure Parameters

- `IN`: input parameter. default (and only) type for functions. works like Java parameters (value is used but modifications do not modify original value/variable itself)
- `OUT`: value from procedure is passed to caller. user defined variable needed.
- `INOUT`: caller passes in value and CAN be modified by procedure and modification is reflected outside of procedure. user defined variable needed.

#### Stored Procedure Syntax

```sql
-- create procedure
CREATE PROCEDURE procedure_name ( IN | OUT | INOUT parameter_name parameter_datatype (length), … )
BEGIN
SQL statements
END//

--  execute procedure
CALL stored_procedure_name([IN parameter],@[OUT parameter]);

-- drop procedure
DROP PROCEDURE [IF EXISTS] stored_procedure_name;
```

Example:

```sql
-- Example 1
-- create:
CREATE PROCEDURE get_product( IN prod_id int )
BEGIN
SELECT * FROM products WHERE product_id = prod_id; END //
-- execute
CALL get_product(1);
-- result
-- product_id	product_name	cost
-- 101	iPhone	450


-- Example 2 :
-- create
CREATE PROCEDURE get_count( IN prod_id int, OUT total INT )
BEGIN
SELECT COUNT(*) INTO total FROM products WHERE product_id = prod_id;
END //
-- execute
call get_count(4,@total);
select @total;
-- result
-- @total
-- 4


-- Example 3 :
-- create
CREATE PROCEDURE counter( INOUT count INT, IN increment INT )
BEGIN
SET count = count + increment;
END //
-- execute
SET @count = 5;
call counter(@count, 2);
select @count;
-- result
-- @count
-- 7
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
