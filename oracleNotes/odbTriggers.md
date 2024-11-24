# PL/SQL Triggers

- When you execute a trigger it will be stored as a database object.
- You cannot explicitelly invoke a trigger


## Row Triggers

The trigger body is executed depending on how many rows were affected by the DML statement. (INSERT / UPDATE / DELETE)

`Row triggers` have the `FOR EACH ROW` clause.

Row trigger have 2 `pseudo records`:
- `:OLD` references the old row before UPDATE or DELETE
- `:NEW` references the new row after INSERT or UPDATE

General Syntax
```sql
CREATE [OR REPLACE] TRIGGER  <trigger-name> BEFORE | AFTER | INSTEAD OF
DELETE | [OR] INSERT | [OR] UPDATE [ OF <column> [, <column>...]] ON <table>
 
-- This section is called Triggering event
 
[ FOR EACH ROW [ WHEN  <condition>] ]
 
-- When clause will be triggering constraint
BEGIN
 
-- This PL/SQL block is Triggering action
 
/* PL/SQL Block */
...
END;
```

Runs automatically. You can only use 1 trigger for the same column. So if you wold want to check min salary before updating salary and inserting salary have to combine the checks in 1 trigger.

### Examples

#### Logging

Requirement: log every time salary is updated.

1. Create Log Table
```sql
CREATE TABLE emp_salary_log(
  employee_id NUMBER(6),
  modified_time TIMESTAMP,
  old_salary  NUMBER(6),
  new_salary  NUMBER(6),
  user_name VARCHAR2(30)
);
```

2. Create Trigger to Log Updates

```SQL
CREATE OR REPLACE TRIGGER trg_emp_salary_log
    BEFORE UPDATE OF salary
    ON Employees
    -- FOR EACH ROW makes it a Row Trigger
    -- that runs for each row affected by the DML statement
    FOR EACH ROW
BEGIN
    INSERT INTO emp_salary_log
        (employee_id, modified_time, old_salary, new_salary, user_name)
        VALUES
        -- :NEW and :OLD are pseudo records to retrieve old and new values of the record
        -- USER will retrieve the current user logged in to the db
        (:NEW.employee_id, SYSTIMESTAMP, :OLD.salary, :NEW.salary, USER);
END;
```
Run a salary update and check the log to see that the trigger has worked.

SEE COMPLEX EXAMPLE AT Triggering Contraints.


## Triggering Constraints

#### Checking / correcting parameters before update

Requirement: Employee salary should be in the range of minimum and maximum salary of his job except for the president (job_id: 'AD-PRES')
If the salary is less than the minimum salary, then employee's salary should be inserted with the minimum salary of his job. If salary is greater than maximum salary then raise an exception with message 'Employee salary cannot be more than max salary of his job'.

```sql
CREATE OR REPLACE TRIGGER trg_check_sal
    -- use trigger for each insert or update
    BEFORE INSERT OR UPDATE OF salary
    ON employees
    -- for all rows
    FOR EACH ROW
        -- ADD CONSTRAINT
        -- where the job_id is NOT 'AD_PRES'
        -- do NOT use `:` before NEW
        WHEN (NEW.job_id <> 'AD_PRES')
DECLARE
    v_min_salary jobs.max_salary%TYPE;
    v_max_salary jobs.max_salary%TYPE;
    e_greater_than_max_salary EXCEPTION;
BEGIN
    -- get minimum salary for the job
    -- use :NEW.job_id from the :NEW pseudo record
    SELECT min_salary, max_salary INTO v_min_salary, v_max_salary
        FROM jobs WHERE job_id = :NEW.job_id;
    -- if correct the :NEW.salary if needed
    IF :NEW.salary < v_min_salary THEN
        :NEW.salary := v_min_salary;
        DBMS_OUTPUT.PUT_LINE('Increased new salary to minimum salary of ' || v_min_salary);
    ELSIF :NEW.salary > v_max_salary THEN
        RAISE e_greater_than_max_salary;
    END IF;
    EXCEPTION
    WHEN e_greater_than_max_salary THEN
        DBMS_OUTPUT.PUT_LINE('Employee salary cannot be more than max salary of his job.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Other problem occured');
END;
```

## Statement Triggers
> Trigger body is executed only once irrespective of how many rows are affected by the DML statement.

Do **NOT** have the FOR EACH ROW clause.

Requirement: Financial year of company is from APRIL to next MARCH. At the end of financial year all balances has to be calculated. So no modification of salary should be allowed in March.

```sql
CREATE OR REPLACE TRIGGER trg_check_update_sal
    BEFORE UPDATE OF salary
    ON employees
DECLARE
    v_todays_date DATE;
BEGIN
    v_todays_date := SYSDATE;
    IF EXTRACT(MONTH FROM v_todays_date) = 3 THEN
        RAISE_APPLICATION_ERROR(-20001, 'Employee salary cannot be modified in March');
    END IF;
END;
```

Use Trigger
```sql
SET SERVEROUTPUT ON;

DECLARE
    v_emp_id employees.employee_id%TYPE := 200;
    v_new_salary employees.salary%TYPE := 100;
BEGIN
    UPDATE employees SET salary = v_new_salary WHERE employee_id = v_emp_id;
    EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Something went wrong');
        DBMS_OUTPUT.PUT_LINE('Error code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error message: ' || SQLERRM);
END;
```

When trigger raises exception:
```bash
Something went wrong
Error code: -20001
Error message: ORA-20001: Employee salary cannot be modified in March
ORA-06512: at "WP.TRG_CHECK_UPDATE_SAL", line 8
ORA-04088: error during execution of trigger 'WP.TRG_CHECK_UPDATE_SAL'
```
The last two ORA error codes are normal part of Oracle's debugging.


## Manage Triggers

View Trigger Details
```sql
SELECT trigger_name, trigger_type, triggering_event,
	table_name, referencing_names,
	status, trigger_body
FROM   user_triggers
WHERE  trigger_name = <triggername>;
```

Delete Triggers
```sql
DROP TRIGGER <triggername>;
```


