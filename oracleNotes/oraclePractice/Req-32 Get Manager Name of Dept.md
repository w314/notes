# Req-32 Get manager name of a department

Develop a stored function sf_get_manager_name 
- that accepts department ID and 
- returns manager's first name. 
- In case of exception function returns -1.

Invoke the function from anonymous block for department ID 30, 50 and 51.

## Stored Function

```sql
CREATE OR REPLACE FUNCTION sf_get_manager_name(
    p_department_id departments.department_id%TYPE)
    RETURN VARCHAR2
IS
    v_manager_id departments.manager_id%TYPE;
BEGIN
    SELECT manager_id INTO v_manager_id
        FROM departments WHERE department_id = p_department_id;
    DECLARE
        v_first_name employees.first_name%TYPE;
    BEGIN
        SELECT first_name INTO v_first_name
            FROM employees WHERE employee_id = v_manager_id;
        RETURN v_first_name;
    END;
    EXCEPTION
    WHEN OTHERS THEN
        -- returning -1 as a string as return type is VARCHAR2
        RETURN '-1';
END;
```

## Invoking Stored Function

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_department_id departments.department_id%TYPE := 50;
    v_manager_name VARCHAR2(100);
BEGIN   
    v_manager_name := sf_get_manager_name(v_department_id);
    IF v_manager_name = '-1' THEN
        DBMS_OUTPUT.PUT_LINE('Error retrieving manager name');
    ELSE 
        DBMS_OUTPUT.PUT_LINE(v_manager_name);
    END IF;
END;
```