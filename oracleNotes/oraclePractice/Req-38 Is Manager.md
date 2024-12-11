# Req-38: Determine if an employee is a manager or not

Develop a stored function, sf_is_manager 
- that accepts employee ID and 
- returns true if he/she is a manager, else returns false. 
- In case of exception, function return Null.
- Invoke the function with employee ID 100 and 110.

 
## Stored Function
On second thought it is probably better to select into variable instead of count, as this can be faster in case of an index. (Maybe count is also fast in case of an index....)

```sql
CREATE OR REPLACE FUNCTION sf_is_manager(
    p_employee_id employees.employee_id%TYPE)
    RETURN BOOLEAN
IS
    v_manager_count NUMBER(3);
BEGIN   
    SELECT COUNT(manager_id) INTO v_manager_count
        FROM employees WHERE manager_id = p_employee_id;
    IF v_manager_count > 0 THEN
        RETURN TRUE;
    ELSE 
        RETURN FALSE;
    END IF;
    EXCEPTION
    WHEN OTHERS THEN
        RETURN NULL;
END;
```

## Invoke Stored Function

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.employee_id%TYPE := '110';
    v_is_manager BOOLEAN;
BEGIN   
    v_is_manager := sf_is_manager(v_employee_id);
    IF v_is_manager THEN
        DBMS_OUTPUT.PUT_LINE('Manager');
    ELSIF NOT v_is_manager THEN
        DBMS_OUTPUT.PUT_LINE('Not a manager');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Error');
    END IF;
END;
```

