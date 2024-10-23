
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

- Used for involving multipole steps or complex logic.
- Can modify database state
- can return mulitple result sets
- called using `CALL` or `EXEC`


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
