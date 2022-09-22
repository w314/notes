#postgres, #windows, #password

# Postgres

## Installation:
- Install postgres, during installation set password for postgres superuser and local port
- On windows after installation set the Path environmental variable. Search for environmental variables and edit Path.


To start postgres in terminal use: 
```bash
`psql -U postgres`
```
- It will ask for password
- if you forgot password: 
    - reset password:
    ```bash
    postgres reset password
    ```
    - find `pg_hba` configuration file stored in the database data directory (C:\Program Files\PostgreSQL\14\data )
    - backup `pg_hba` as `pg_hba.bk`
    - Edit the `pg_hba` file and change the method of all local connection (there are several change all of them)  to: trust
    start postgres in terminal
    - start postgres again
    ```bash
    psql -U postgres
    ```
    - it will let you log in without a password
    - set password for postgres user:
    ```bash
    ALTER USER postgres WITH PASSWORD ‘new_password’;
    ```
    - restore the original pg_dba.conf file

To exit postgres in the terminal enter: \q


## Postgres commands
<table>
<tr><td>\l</td><td>list databases</td></tr>
<tr><td>\c</td><td>connect to database</td></tr>
<tr><td>\dt</td><td>display tables in a database</td></tr>
<tr><td>\q</td><td>quit psql back to normal terminal</td></tr>
<tr><td>\du</td><td>list users</td></tr>
</table>


## Setup Scheema
- create user
```sql
CREATE USER <user_name> WITH PASSWORD '<password>';
```
- create database
```sql
create database <database_name>
```
```sql
GRANT ALL PRIVILEGES ON DATABASE <database_name> TO <user_name>;
```

- connect to database
```bash
\c <database_name>
```
- create tables
```sql
CREATE TABLE [IF NOT EXISTS] <table_name> (
id SERIAL PRIMARY KEY,
name VARCHAR(50),
count integer
);
```

## CRUD
> Use single quotes for strings

#### CREATE
```sql
INSERT INTO <table_name> (<column_name>, <column_name>) VALUES (<value>, <value>);
order of column names must match order of values
```
#### READ
```sql
SELECT * FROM <table_name>;
```

#### UPDATE
```sql
UPDATE <table_name> SET <column_name> = <value> WHERE id=1;
```
#### DELETE
```sql
DELETE FROM <table_name> WHERE id=1;
```

Double Quotes vs Single Quotes
quoting rules in postgres

double quotes are for used for identifiers (like table names), if in double quotes these identifiers are case sensitive, usually identifiers are used without quotes, in that case they are case insensitive
single quotes are used to indicate that a token is a string. If your string contains a single quote, use two single quotes instead of one. Both of these SQL commands are valid if my_table and it’s column text were created with lower case letters::
INSERT INTO my_table(text) VALUES (‘How ‘’s it going?’);
INSERT INTO “my_table”(“text”) VALUES (‘How’’s it going?’);


## Problems

INSERT Problem

Column "John" doesn't exists with:
`INSERT INTO <table> (name) VALUES ("John")

Solution:
Use single quotes. The issue is with the double quotes - postgres is interpreting them as "delimited identifiers" (i.e. the name of an object, such as a column in a table).




