# Req-40: Keep track of salary changes of every employee

To keep track of salary changes of every employee for auditing in the future. Whenever an HR Manager modifies the salary of any employee, the below details need to be inserted in EMP_SALARY_LOG table
- employee_id: employee ID of whose salary is getting modified
- modified_time: at what time this modification takes place
- old_salary: existing salary of employee
- new_salary: modified salary
- user_name: database user who is making this modification 

## Create Table for log

```sql
CREATE TABLE emp_salary_log (
    employee_id NUMBER(6),
    modified_time TIMESTAMP,
    old_salary NUMBER(8,2),
    new_salary NUMBER(8,2),
    user_name VARCHAR2(30)
);
```

## Create Trigger

```sql
CREATE OR REPLACE TRIGGER trg_emp_salary_log
BEFORE UPDATE OF salary ON employees
FOR EACH ROW
DECLARE
    v_old_salary NUMBER := :old.salary;
    v_new_salary NUMBER := :new.salary;
BEGIN
    INSERT INTO emp_salary_log
        (employee_id, modified_time, old_salary, new_salary, user_name)
        VALUES
        (:new.employee_id, SYSTIMESTAMP, v_old_salary, v_new_salary, USER);
END;
```
