# Oracle

## Sources
- [OracleTutorial (not official Oracle docs)](https://www.oracletutorial.com/)
- [Database Star](https://www.databasestar.com/oracle-database/)
- [All Things SQL](https://blogs.oracle.com/sql/)

## Setup

Install Oracle Database XE from [Oracle](https://www.oracle.com/database/technologies/appdev/xe.html).

Install Oracle Developer from [Oracle](https://www.oracle.com/database/sqldeveloper/technologies/download/).

### Start Oracle DB

[source](https://docs.oracle.com/en/database/oracle/oracle-database/18/xeinw/connecting-oracle-database-xe.html)

When you install Oracle Database XE, your Windows user is automatically added to the ORA_DBA operating system group, which grants you the SYSDBA privileges.

```bash
cd C:/app/piros/product/21c/dbhomeXE/bin
sqlplus / as sysdba
```

## PDB vs CDB (Pluggable vs Container Database)

[Source](https://www.databasestar.com/oracle-pdb/)

- `CDB`
    - Oracle can function as `multitenant container database  = CDB`
- `PDB`
    - collection of schemas and object that act as a regular Db


### Oracle CDB structure

- has many containers
- container can be either a CDB or the root
- there are 2 containers by default
    - `CDB$ROOT`
        - root container
        - contains Oracle metadata
        - contains common users
    - `PDB$SEED`
        - template that can be used to create PDBs
        - cannot be modified
- Oracle XE comes with a PDB already created: `XEPDB1`

### View / Change  Containers

In `SQL Plus` (software installed with Oracle) run:
```sql
-- show container currently used
SHOW CON_NAME;

-- show available PDBs
SELECT pdb_name, status FROM cdb_pdbs;

-- change container
ALTER SESSION SET container = <container_name>;
```

### Create Pluggable DB

[Source: Oracle Docs](https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/CREATE-PLUGGABLE-DATABASE.html)





## Users

List all users in the database:<br>
`select username from dba_users;`

### Create User

DO NOT USE SYS SCHEMA. ([Source](https://stackoverflow.com/questions/15377346/why-cannot-i-create-triggers-on-objects-owned-by-sys))

DO NOT CREATE USER IN ROOT CONTAINER<br>
If getting error `ORA-65096: invalid common user or role name`
you probably try to create user in root container.

SET CONTAINER TO A PDB first.

Sources:
- [Create User - OracleTutorial](https://www.oracletutorial.com/oracle-administration/oracle-create-user/)
- [Grant Priviliges - OracleTutorial](https://www.oracletutorial.com/oracle-administration/oracle-grant/)
- [Grant All - OrcaleTutorial](https://www.oracletutorial.com/oracle-administration/oracle-grant-all-privileges-to-a-user/)
- [Invalid common user erro SOF](https://stackoverflow.com/questions/33330968/error-ora-65096-invalid-common-user-or-role-name-in-oracle-database)

```sql
CREATE USER <user_name> IDENTIFIED BY <password>;
GRANT ALL PRIVILEGES TO <user_name>;
```

Granting specific privileges
```sql
-- lets user log in
GRANT CREATE SESSION TO <user_name>
```


## `Listener`

[Source](https://www.oracletutorial.com/oracle-administration/oracle-listener/)

A `listener` is a separate database server process that establishes the connection between clients and the database instance.

If the `listener` stops working you cannot connect to the database, already established connection will not be affected.

If trying to connect you will get: `ORA-12541: Cannot connect. No listener` error.

Listener Command
- status: `lsnrctl status`
- start: `lsnrctl start`


## Usefull commands

```sql
-- view tables you have created
select table_name from user_tables;

-- view all object you have created
select object_name, object_type from user_objects;
```


## SQL Developer

DO NOT connect with user: `SYS AS SYSDBA` it uses cdb root, connect with user created and using a pbd container.


TO run sql scripts:
Select Tools > SQL Worksheets




