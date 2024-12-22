pl-sql, trigger, statement trigger

# Req-51: No employee can be added on Sunday
Develop a trigger TRG_ADD_EMPLOYEE_SUNDAY to restrict adding employees on Sunday.

If so, raise an exception  with error code -20000 and the error message as 'Employee record cannot be inserted on Sunday' 

Hint: HIRE_Date should not be Sunday

```sql
create or replace TRIGGER trg_add_employee_sunday
    BEFORE INSERT ON employees
BEGIN
    IF TRUE THEN
        RAISE_APPLICATION_ERROR(-20001, 'test error');
    END IF;
    IF UPPER(TO_CHAR(SYSDATE, 'DAY')) = 'FRIDAY' THEN
        RAISE_APPLICATION_ERROR(-20000, 'Employee record cannot be inserted on Sunday');
    END IF;
END;
```