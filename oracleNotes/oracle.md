# Oracle

## Sources
- [OracleTutorial (not official Oracle docs)](https://www.oracletutorial.com/)
- [Database Star](https://www.databasestar.com/oracle-database/)

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

In SQL Developer

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

