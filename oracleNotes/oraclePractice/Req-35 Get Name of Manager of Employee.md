# Req-35: View name of manager of employee
Develop a stored function sf_get_emp_manager_name 
- that accepts employee ID and 
returns manager's full name of the given employee. ( Format: <FIRST_NAME><space><LAST_NAME> ) . 
- If employee ID is invalid return -1, 
- if no manager is associated with that employee return -2, 
- for any other error return -3.
- Also invoke the function from anonymous block for employee ID 100, 200 and 115.

## Stored Function
Uses already created stored function `sf_manager_id` created in Req-34

```sql
CREATE OR REPLACE FUNCTION sf_manager_name(
    p_employee_id employees.employee_id%TYPE)
    RETURN VARCHAR2
IS
    v_manager_id employees.manager_id%TYPE;
    v_first_name employees.first_name%TYPE;
    v_last_name employees.last_name%TYPE;
BEGIN
    v_manager_id := sf_manager_id(p_employee_id);
    IF v_manager_id = -1 THEN
        RETURN '-1';
    ELSIF v_manager_id IS NULL THEN
        RETURN '-2';
    END IF;
    SELECT first_name, last_name INTO v_first_name, v_last_name
        FROM employees WHERE employee_id = v_manager_id;
    RETURN v_first_name || ' ' || v_last_name;
    EXCEPTION
    WHEN OTHERS THEN
        RETURN '-3';
END;
```

## Invoke Stored Function

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.employee_id%TYPE := 115;
    v_manager_name VARCHAR2(100);
BEGIN   
    v_manager_name := sf_manager_name(v_employee_id);
    IF v_manager_name = '-1' THEN
        DBMS_OUTPUT.PUT_LINE('Invalid employee id');
    ELSIF v_manager_name = '-2' THEN
        DBMS_OUTPUT.PUT_LINE('Employee has no manager');
    ELSIF v_manager_name = '-3' THEN
        DBMS_OUTPUT.PUT_LINE('Other error.');
    ELSE 
        DBMS_OUTPUT.PUT_LINE('Manger name: ' || v_manager_name);
    END IF;
END;
```