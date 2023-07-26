MySQL

# MySQL

## `DDL` Data Definition Language

Create Database

```sql
CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] db_name;

```

```sql
CREATE DATABASE IF NOT EXISTS my_database;
```

### Tables

Create Table
MySQL it is necessary to select a database to which to apply statments. You should execute the USE db_name statement before the create statement

```sql
CREATE [TEMPORARY] TABLE [IF NOT EXISTS] table_name (create_definition, ...) [table_options] [partition_options]
```

```sql
USE my_database;
CREATE TABLE my_table (
	id int primary key,
    my varchar(10) not null,
    my_other_value float default 10.0
);
```

```sql
-- deletes table
DROP [TABLE] table_name

RENAME TABLE old_name TO new_name [, old2_name TO new2_name]

-- deletes all data from table
TRUNCATE [TABLE] table_name
```
