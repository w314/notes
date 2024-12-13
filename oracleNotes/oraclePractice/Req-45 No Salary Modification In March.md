pl-sql, statement trigger, trigger

# Req-45: HR manager cannot modify the salary of employees in the month of March 
Financial year of company is from APRIL to next MARCH. At the end of financial year all balances has to be calculated. So, during this time no modification of salary should be allowed.

Develop Trigger

## Trigger

```sql
CREATE OR REPLACE TRIGGER trg_check_update_sal
    BEFORE UPDATE OF salary ON employees
DECLARE
    v_today DATE := TO_DATE('11-03-2022', 'DD-MM-YYY');
BEGIN
    IF TO_CHAR(v_today, 'MONTH') = 'March' THEN
        RAISE_APPLICATION_ERROR(-20003, 'Cannot modify salaries in March');
    END IF;
END;
```
