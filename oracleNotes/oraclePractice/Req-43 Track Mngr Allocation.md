trigger, insert or update, when updating then, 

# Req-43: Keep track of the manager allocations for each department

HR Manager wants to keep track of all manager details of every department for auditing in the future. Whenever an HR Manager assigns a new manager, the following manager details should be recorded in DEPT_MANAGER_LOG table.

    department_id : department for which manager is getting assigned or getting modified

    manager_id : employee_id who is being assigned as manager

    start_date : date on which manager is getting assigned for a department

    end_date: end_date of manager (when a manager is assigned the end_date will be null)

    user_name: name of database user who is doing this modification 

## Create Log Table

```sql
CREATE TABLE dept_manager_log(
    department_id NUMBER(4),
    manager_id NUMBER(6),
    start_date DATE,
    end_date DATE,
    user_name VARCHAR2(30)
);
```

## Create Trigger

```sql
CREATE OR REPLACE TRIGGER trg_manager_log
BEFORE INSERT OR UPDATE OF manager_id ON departments
FOR EACH ROW
DECLARE
BEGIN
    IF UPDATING THEN
        UPDATE dept_manager_log 
            SET end_date = SYSDATE
            WHERE department_id = :old.department_id AND
                manager_id = :old.manager_id AND
                end_date IS NULL;
    END IF;
    INSERT INTO dept_manager_log
         (department_id, manager_id, start_date, end_date, user_name)
         VALUES
         (:new.department_id, :new.manager_id, SYSDATE, NULL, USER);
END;
```
