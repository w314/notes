# Req-16 Update manager of department

Develop a stored procedure sp_update_manager 
- that accepts department ID and 
- new manager ID to update the manager of given department.
- OUT parameter p_status should be set as
    - 0 for successful insertion
    - -1 if the passed manager_id is an invalid employee
    - -2 if department_id is invalid
    - -3 if new manager does not belong to that department 
    - -4 for any other exception.
- Invoke the created procedure to make David Austin, employee ID 105, the manager of IT department.


## Stored Procedure

```sql
CREATE OR REPLACE PROCEDURE sp_update_manager(
    p_department_name IN departments.department_name%TYPE,
    p_manager_id IN departments.manager_id%TYPE,
    p_status OUT NUMBER)
IS
    v_dept_name_count NUMBER(2);
    v_department_id departments.department_id%TYPE;
    v_dept_of_manager departments.department_id%TYPE;
BEGIN
    -- check if submitted manager is valid employee
    SELECT department_id INTO v_dept_of_manager
        FROM employees WHERE employee_id = p_manager_id;
    -- check if submitted department name is valid
    SELECT COUNT(department_name) INTO v_dept_name_count
        FROM departments WHERE department_name = p_department_name;
    IF v_dept_name_count != 1 THEN
        p_status := -2;
    ELSE
        -- check if manager is employee of the department
        SELECT department_id INTO v_department_id
            FROM departments
            WHERE department_name = p_department_name;
        IF v_department_id != v_dept_of_manager THEN
            p_status := -3;
        ELSE      
            UPDATE departments SET manager_id = p_manager_id
                WHERE department_id = v_department_id;
            COMMIT;
            p_status := 0;
        END IF;
    END IF; 
    EXCEPTION
    -- handle non-existent manager id
    WHEN NO_DATA_FOUND THEN
        p_status := -1;
    WHEN OTHERS THEN
        p_status := -4;
END;       
```

## Ivoke Stored Procedure

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_department_name departments.department_name%TYPE := 'IT';
    v_manager_id departments.manager_id%TYPE := 105;
    v_result NUMBER(1,0);
BEGIN
    sp_update_manager(v_department_name, v_manager_id, v_result);
    IF v_result = 0 THEN
        DBMS_OUTPUT.PUT_LINE('Manager successfully updated');
    ELSIF v_result = -1 THEN
        DBMS_OUTPUT.PUT_LINE('Invalid manager id');
    ELSIF v_result = -2 THEN
        DBMS_OUTPUT.PUT_LINE('Invalid department id');
    ELSIF v_result = -3 THEN
        DBMS_OUTPUT.PUT_LINE('Manager is not employee of department');
    ELSIF v_result = -4 THEN
        DBMS_OUTPUT.PUT_LINE('Other error occured');
    ELSE 
        DBMS_OUTPUT.PUT_LINE('Unexpected result ' || v_result);
    END IF;
END;
```


## OLD VERSIONS

VERSION A
Develop a PL/SQL program to make David Austin, employee ID 105, as the manager of IT department.

Business Rule: 105 should be a valid employee and should also belong to IT department.


VERSION B
update the manager ID of department with ID 70 to 333. Handle exceptions, if any, with appropriate message. 
- ORA-02291 is the error code for integrity constraint violated - parent key not found


#### VERSION A
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

####  VERSION B
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
