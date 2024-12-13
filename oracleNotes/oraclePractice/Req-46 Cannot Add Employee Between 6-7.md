pl-sql, trigger, statement trigger

# Req-46: HR Manager cannot add employees from 6 pm to 7 pm

EMS system will be down everyday 6PM to 7PM for maintenance. HR Manager should not be able to add any employee during this time.

Develop a trigger to check this before adding employees. If time is not valid, raise an exception with message "System is down, no operation cannot be done"

## Trigger

```sql
CREATE OR REPLACE TRIGGER trg_emp_insert_time
    BEFORE INSERT ON employees
DECLARE
    c_maintenance_hour CONSTANT NUMBER(2) := 18;
    v_current_hour NUMBER(2);
BEGIN   
    v_current_hour := EXTRACT(HOUR FROM SYSTIMESTAMP) + EXTRACT(TIMEZONE_HOUR FROM SYSTIMESTAMP);
    IF v_current_hour = c_maintenance_hour THEN
        RAISE_APPLICATION_ERROR(-20004, 'System is down, no operation cannot be done');
    END IF;
END;
```
 

