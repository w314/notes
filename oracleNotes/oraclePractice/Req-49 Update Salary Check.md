pl-sql, trigger

# Req-49: Employee salary should be greater than his existing salary
Whenever HR Manger is changing the salary of any employee, employee salary should be greater than his existing salary. Else, raise an exception with message "Employee salary should not be less than his current salary" and error code -20000.

Develop a trigger TRG_UPDATE_SALARY to check this requirement, before modifying salary of every employee.


```sql
CREATE OR REPLACE TRIGGER trg_update_sal
    BEFORE UPDATE OF salary ON employees
    FOR EACH ROW
BEGIN
.
    IF :NEW.salary < :OLD.salary THEN
        RAISE_APPLICATION_ERROR(
            -20000, 'Employee salary should not be less than his current salary');
    END IF;
END;
```
