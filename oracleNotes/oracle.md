# Oracle

## Sources
- [OracleTutorial (not official Oracle docs)](https://www.oracletutorial.com/)
- [Database Star](https://www.databasestar.com/oracle-database/)
- [All Things SQL](https://blogs.oracle.com/sql/)

## Setup

Install Oracle Database XE from [Oracle](https://www.oracle.com/database/technologies/appdev/xe.html).

Install Oracle Developer from [Oracle](https://www.oracle.com/database/sqldeveloper/technologies/download/).

## Pluggable vs Container Database

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

### Manage / View Containers

In `SQL Plus` (software installed with Oracle) run:
```sql
-- show container currently used
SHOW CON_NAME;

-- show available PDBs
SELECT pdb_name, status FROM cdb_pdbs;

-- change container
ALTER SESSION SET container = <container_name>;
```

### Start Oracle DB

[source](https://docs.oracle.com/en/database/oracle/oracle-database/18/xeinw/connecting-oracle-database-xe.html)

When you install Oracle Database XE, your Windows user is automatically added to the ORA_DBA operating system group, which grants you the SYSDBA privileges.

```bash
cd C:/app/piros/product/21c/dbhomeXE/bin
sqlplus / as sysdba
```


## Create User

DO NOT USE SYS SCHEMA. ([Source](https://stackoverflow.com/questions/15377346/why-cannot-i-create-triggers-on-objects-owned-by-sys))

DO NOT CREATE USER IN ROOT CONTAINER<br>
If getting error `ORA-65096: invalid common user or role name`
you probably try to create user in root container.

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

If trying to connect you will get: `ORA-12541: TNS:no listener` error.

Listener Command
- status: `lsnrctl status`
- start: `lsnrctl start`


## Userful commands

```sql
-- view tables you have created
select table_name from user_tables;

-- view all object you have created
select object_name, object_type from user_objects;
```


## SQL Developer

Connect
user: `SYS AS SYSDBA`
password: as set at  installation for SYS


TO run sql scripts:
Select Tools > SQL Worksheets


```sql
SET SERVEROUTPUT ON
DECLARE
    v_first_name VARCHAR(20);
    v_last_name VARCHAR(20);
    v_date_of_joining DATE;
    v_current_salary NUMBER(8,2);
    v_incremented_salary NUMBER(8,2);
BEGIN
    SELECT first_name, last_name, hire_date, salary INTO v_first_name, v_last_name, v_date_of_joining, v_current_salary
        FROM employees WHERE employee_id = 103;
    IF(v_date_of_joining >= '01-Jan-95') THEN
        v_incremented_salary := v_current_salary * 1.1;
    ELSE
        v_incremented_salary := v_current_salary * 1.15;
    END IF;
    UPDATE employees SET salary = v_incremented_salary WHERE employee_id = 103;
    DBMS.OUTPUT.PUT_LINE('Name: '|| v_first_name || ' ' || v_last_name);
    DBMS.OUTPUT.put_line('Date of Joining: ' || v_date_of_joining);
    DBMS.OUTPUT.put_line('Current Salary: ' || v_current_salary);
    DBMS.OUTPUT.put_line('Incremented Salary: ' || v_incremented_salary);
END;
```

### Output ("Print") Results

```sql
-- if omitted it won't output anythin
SET SERVEROUTPUT ON;

-- print statemnt
DBMS_OUTPUT.PUT_LINE(v_variable_to_print |
| ' does not exist');
```


If encountering error: `PLS-00201: identifier 'DBMS.OUTPUT' must be declared`

Solve by running `GRANT EXECUTE ON DBMS_OUTPUT to PUBLIC;`

