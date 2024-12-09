# Req-34: View id of manager of employee

Develop a stored function sf_get_emp_manager_id
-  that accepts employee ID and 
- returns manager ID of the given employee. 
- In case of exception function returns -1.
- invoke the function from anonymous block for employee ID 201 and 4444.

## Stored Function

```sql
CREATE OR REPLACE FUNCTION sf_manager_id(
    p_employee_id employees.employee_id%TYPE)
    RETURN NUMBER
IS
    v_manager_id employees.manager_id%TYPE;
BEGIN
    SELECT manager_id INTO v_manager_id 
        FROM employees WHERE employee_id = p_employee_id;
    RETURN v_manager_id;
    EXCEPTION
    WHEN OTHERS THEN
        RETURN -1;
END;
```

## Invoke Stored Function

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.employee_id%TYPE := 111;
    v_manager_id employees.manager_id%TYPE;
BEGIN
    v_manager_id := sf_manager_id(v_employee_id);
    IF v_manager_id = -1 THEN
        DBMS_OUTPUT.PUT_LINE('Error');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Employee with id ' || v_employee_id || 
            ' has manager with id: ' || v_manager_id);
    END IF;
END;
```