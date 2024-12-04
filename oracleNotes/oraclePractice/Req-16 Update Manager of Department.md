## Req-16 Update manager of department


VERSION A
Develop a PL/SQL program to make David Austin, employee ID 105, as the manager of IT department.

Business Rule: 105 should be a valid employee and should also belong to IT department.


VERSION B
update the manager ID of department with ID 70 to 333. Handle exceptions, if any, with appropriate message. 
- ORA-02291 is the error code for integrity constraint violated - parent key not found


### VERSION A
Primitive solution without exception handling.
```sql
SET SERVEROUTPUT ON;

DECLARE
    v_department_id departments.department_id%TYPE;
    v_department_name departments.department_name%TYPE := 'IT';
    v_employee_id employees.employee_id%TYPE := 105;
    v_employee_department_id employees.department_id%TYPE;
    v_employee_count NUMBER(2);
BEGIN   
    -- check if employee ID valid
    SELECT COUNT(employee_id) INTO v_employee_count
        FROM employees WHERE employee_id = v_employee_id;
    IF ( v_employee_count = 1 ) THEN
        -- check if employee belongs to IT department
        -- get id of department based on its name
        SELECT department_id INTO v_department_id 
            FROM departments WHERE department_name = v_department_name; 
        -- get department_id of employee
        SELECT department_id INTO v_employee_department_id 
            FROM employees WHERE employee_id = v_employee_id;
        -- check if employee belongs to the department    
        IF ( v_employee_department_id = v_department_id ) THEN
            -- update manager of department
            UPDATE departments SET manager_id = v_employee_id 
                WHERE department_id = v_department_id;
            DBMS_OUTPUT.PUT_LINE('Set manager_id of ' || v_department_name || ' department to ' ||  v_employee_id || '.');
        ELSE
            DBMS_OUTPUT.PUT_LINE('Employee does not belong to department ' || v_department_name);
        END IF;
    ELSE
        DBMS_OUTPUT.PUT_LINE('Invalid employee ID');
    END IF;
END;
```

### VERSION B
```sql
SET SERVEROUTPUT ON;

DECLARE
    v_department_id departments.department_id%TYPE := 70;
    v_employee_id employees.employee_id%TYPE := 333;
    e_invalid_manager_id EXCEPTION;
    PRAGMA EXCEPTION_INIT(e_invalid_manager_id, -2291);

BEGIN   
    UPDATE departments SET manager_id = v_employee_id 
        WHERE department_id = v_department_id;
    DBMS_OUTPUT.PUT_LINE('Succesfully set manager_id of ' || 
        ' to ' ||  v_employee_id || '.');
    EXCEPTION
    WHEN e_invalid_manager_id THEN
        DBMS_OUTPUT.PUT_LINE('Manager id ' || v_employee_id || ' is invalid.');
END;
```
