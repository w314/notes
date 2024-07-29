sql

# SQL


### Constraints

> What are constraints and can you describe a few constraints?

`Constraints` are rules for columns to ensure validity of data. They are used to restrict the values of data which are inserted into a table.

`Constraints` are used to define a database schema and are the backbone for defining `integrity constraints` of the schema. They help validate data beyond just a simple data type.

- `NOT NULL` Ensures that a column's value is not null.
- `UNIQUE` Ensures that a column's value is unique in the table. (Can have one `NULL` value.)
- `PRIMARY KEY` Combines unique and not null. Uniquely identifies each row.
- `FOREIGN KEY` Links to a row in another table. Prevents the destruction of those links.
- `DEFAULT` Specifies a value for a column, if one is not given.
- `CHECK`
  - helps us to get only those values that are valid for the condition and our requirements.
- `CREATE INDEX` Create a sorted index of the column for faster searching.

```sql
create table content_meta (
	id int auto_increment primary key,
    content_type int not null,
    url varchar(500) not null unique,
    uploader int not null,
    size_in_bytes bigint default 1,
    uploaded_at timestamp default now(),
    constraint url_scheme_check check(instr(url, 'http://') > 0),
    constraint size_check check(size_in_bytes > 0), check(size_in_bytes < 10000000),
    foreign key(content_type) references content_type(id),
    foreign key(uploader) references users(id),
    index (content_type)
);
```

### Composite Key

`Composite Key` is combining two or more keys in a table to create a primary key to uniquly identify a record.

`Compound Key` is a `Composite Key` where each attribute creating a key is a `Foreign Key`.


## SQL Transactions

### SQL TCL - Transaction Control Language

> What is TCL?

TCL commands manage the transactions that take place in a database.

> What is a transaction?

- transaction: one or more DQL or DML operations performed on a database as a single unit

- a `transaction` is a set of SQL statements that are executed on the data stored in DBMS
- Whenever we perform any of the DDL command like -INSERT, DELETE or UPDATE, these can be rollback if the data is not stored permanently
- to make the changes permanent, we use TCL commands
- TCL commands are used to ensure the transaction satisfies all the ACID properties
- DDL can be included, but cannot be rolled back. Don't use DDL in a transaction mixed with other statements

### SQL Transaction Properties - ACID
  - **A**TOMICITY
    - All the operations performed within the transaction get executed or none of them.
  - **C**ONSISTENTENCY
    - Consistency ensures that your transaction takes a system from one consistent state to another consistent state.
  - **I**SOLATION
    - ensures that the transaction is isolated from other transactions.
    - isolation level can be changed
  - **D**URABILITY
    - Durability ensures that your committed changes get persisted.

### TCL Commands

- `START TRANSACTION` - notifies MySQL that the statements after Start should be cosidered as a single unit.
- `COMMIT` - used to save the data permanently
- `ROLLBACK` - used to get the data or restore the data to the last savepoint or last committed state
- `SAVEPOINT` - used to save the data at a particular point temporarily

### Example

```sql
START TRANSACTION;
INSERT INTO bankaccounts VALUES("ACC3", 10000);
SAVEPOINT sv;
INSERT INTO bankaccounts VALUES("ACC4", 900000);
ROLLBACK TO sv;
INSERT INTO bankaccounts VALUES("ACC4", 90000);
COMMIT;

-- BANK TRANSER TRANSACTION
START TRANSACTION or BEGIN; --statement1
UPDATE bankaccounts SET funds=funds-100 WHERE account_no='ACC1'; --statement2
UPDATE bankaccounts SET funds=funds+100 WHERE account_no='ACC2'; --statement3
COMMIT; --statement4
```

### Transaction Properties (`ACID`)

> What are the properties of a transaction?

- `Atomicity` - is combining all statements into a single unit. A transaction is considered to be atomic if it cannot be further broken down into individual operations and, all of the operations that occur within a transaction either succeed or fail as a single unit. If a single operation fails during a transaction, then everything is considered to have failed and must be rolled back.

- `Consistency` : One of the advantages of using a transaction is that, even if the transaction is a success or a failure, the database is consistent and the data integrity is maintained.
  All inconsistent data is removed, and all transactions that might cause inconsistency are aborted and an error is created or transcribed into an error log. Example: Consider two bank accounts ACC1 and ACC2 with funds of 10000$ and 9000, which is is total of 19000, after a transaction of transferring 50$ from ACC2 to ACC1 the funds in ACC1 is 10050$ and ACC2 are 8950$, which means the totals funds in AC1 and ACC2 adds up to 19000, So the funds in ACC1 and ACC2 are consistent before and after the Transaction.
- `Isolation`: Every transaction is isolated from other transactions. Therefore, a transaction shouldn't affect other transactions running at the same time. Stated another way, data modifications made by one transaction should be isolated from the data modifications made by other transactions. So, while a transaction can see data in the state it was in before another concurrent transaction modified it, as well as after the second transaction has completed, it cannot see any intermediate states. Example: Consider that the user A withdraws $100 and user B withdraws $250 from user ACC1 account, which has a balance of $1,000. Since both A and B draw from ACC1 account, one of the users is required to wait until the other user transaction is completed, avoiding inconsistent data.

- `Durability`:
  Transactions help with Durability in a few ways: data modifications that take place within a successful transaction may be safely considered to be stored in the database regardless of whatever else may occur. As each transaction is completed, a row is entered in the database transaction log. Thus, in the event of a system failure that requires the database to be restored from a backup you can use this transaction log to get the database back to the state it was in after a successful transaction.

  - once these transactions are successfully executed, the changes made to the database are permanent even if an unexpected system failure or an error occurs.

  The ACID property of DBMS plays a vital role in maintaining the consistency and availability of data in the database

#### Transaction Isolation Levels (Supplementary)

- read uncommitted: transactions can read uncommitted changes made by others (dirty reads)
- read committed: selecting same data multiple times in a transaction and not getting the same information (nonrepeatable read) as other transactions commit modifications
- repeatable read: uses data in its state at the start of a transaction, prevents nonrepeatable read / updates to the data being read
- serializable: ensures, while a transaction is reading data, thatno data is removed or deleted that can cause a difference (phantom reads)

### DML

The `DML` (`Data Management Language`) sublanguage of SQL is utilized to create, update, and delete data in a database.

- `INSERT`
- `UPDATE`
- `DELETE`

```sql
INSERT INTO roles (id, name) values (1, 'ADMIN'), (2, 'OWNER'), (3, 'EDITOR'), (4, 'VIEWER');

UPDATE permissions set categoryId=1;

DELETE FROM roles where name='VIEWER';
```

### DROP vs TRUNCATE vs DELETE

<table>
<thead><td>DELETE</td><td>TRUNCATE</td><td>DROP</td></thead>
<tbody>
<tr>
<td>DML</td><td>DDL</td><td>DDL</td>
</tr>
<tr>
<td>WHERE clause can be used to filter and delete one or more rows</td>
<td>WHERE clause cannot be used</td>
<td>WHERE clause cannot be used</td>
</tr>
<tr>
<td>It is executed using <strong>row lock</strong>, and each row in the table is locked for deletion</td>
<td>It is executed using <strong>table lock</strong>, where whole table is locked while removing the records</td>
<td>It removes a table form the database</td>
</tr>
<tr>
<td>It maintains the log, so it is slower than TRUNCATE</td>
<td>Least amount of logging needed so it is faster in performace</td>
<td>It maintains the log, so it is slower than TRUNCATE</td>
</tr>
<tr>
<td>It can roll back the deleted data before committing it</td>
<td>It cannot be rolled back</td>
<td>It cannot be rolled back</td>
</tr>
</tbody>
</table>

## SQL DQL

`DQL` the `Data Query Language` is used to search, filter, group and aggregate stored data

- uses the `SELECT` statement
- retrieves a `Resultset`

```sql
SELECT [ALL | DISTINCT]
    select_expr [, select_expr] ...
    [into_option]
    [FROM table_ref]
    [WHERE where_condition]
    [GROUP BY {col_name | expr | position}]
    [HAVING having_condition]
    [ORDER BY {col_name | expr | position}]
        [ASC | DESC]
    [LIMIT {[offset,] row_count | row_count OFFSET offset}];

```

### Clauses

#### `WHERE` Clause

`WHERE` filters and extracts only records that match condition

- if using an aggregate function, WHERE filters before it is called
- `HAVING` is used only if an aggregate function is called
- HAVING filters after the function call

> Why would I use the WHERE clause?

The `WHERE` clause is not only used in `SELECT` statements, it is also used in `UPDATE`, `DELETE` as well

FILTERING: The filtering clause of a select statement is a `WHERE` clauses that defines how selected rows are filtered from the table.

##### WHERE Clause Operators

WHERE` clauses use to select records that meet specific conditions:

- logical operators
- comparison operators
- matching operators

Operators:

- `AND` true if both boolean expresions evaluate to true
- `IN` true if the operand is included in a list of expressions
- `NOT` Reverses the value of any boolean expression
- `OR` true if either or both boolean expressions is true
- `LIKE` true if the operand matches a pattern
  - `%` (percent) match any string of zero or more characters
  - `_` (underscore) match any single character
- `BETWEEN` true if the operand falls within a range
  Where Logical operators

#### `GROUP BY` Clause

> What is the GROUP BY clause used for?-

- used to group data based on the exact value in a specific field
- groups rows that have the same values into summary rows
- have to be used with aggregate functions like `COUNT`, `MAX`, `MIN`.
- `HAVING` is used to filter out groups that meet a condition.

#### `ORDER BY` Clause

> What is the ORDER BY clause used for?

- `ORDER BY` clause is used to sort the returned records by a specified column
- The records can be ordered either `ASC` (ascending) or `DESC` (descending).
- Ascending order is default if not specified.

### Other Clauses

- `LIMIT` clause restricts number of records returned from the select statement.
- `OFFSET` clause specifies from which record position to start counting from. This is often used in conjunction with the `LIMIT` clause. NOTE: Some SQL implementations use the `SKIP` keyword instead of offset

### Aliases

Aliases is used to give a temporary name to a table or a column in a table for the intention to support a specific query.

```sql
SELECT column_name AS alias_name FROM table_name;
```

Advantages:

- It provides a very useful feature that allows us to achieve complex tasks quickly.
- It makes column or table name more readable.
- It allows us to combine two or more columns
- It makes the table more user-friendly.

### Flow Control Statements (Supplementary)

- https://dev.mysql.com/doc/refman/8.0/en/flow-control-statements.html


## SQL Questions

>What is a Transaction? 

>What are the commands in TCL (Transaction Control Language)? 

>What are the ACID properties? 
 

>Be able to describe these alternate keys: 
>- Composite Key 

>- Unique Key 

>Be able to describe what these constraints accomplish: 

>- NOT NULL 

>- DEFAULT 

>- CHECK 
 


