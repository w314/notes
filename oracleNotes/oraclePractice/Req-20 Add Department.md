## Req-20 Add department

VERSION A

Develop a PL/SQL program to add a new department with
- DEPARTMENT_ID: 111
- DEPARTMENT_NAME: Sales
- MANAGER_ID: 222
- LOCATION_ID: 1500

In the program
- Declare, raise and handle a user-defined exception with an appropriate message if manager ID is not valid.
- Declare, raise and handle a user-defined exception with an appropriate message if location ID is not valid. 
- test location_id 150 for invalid location
- test manager_id 105 for valid manager

VERSION B
- omit department_name
- handle exception
- ORA-01400 is the error code for violation of not null constraint


### Version A
```sql
SET SERVEROUTPUT ON;

DECLARE
    v_department_id departments.department_id%TYPE := 111;
    v_department_name departments.department_name%TYPE := 'Sales';
    v_manager_id departments.manager_id%TYPE := 105;
    v_location_id departments.location_id%TYPE := 150;
    e_invalid_manager EXCEPTION;
    e_invalid_location EXCEPTION;
BEGIN
    DECLARE
        v_manager_count NUMBER(2);
    BEGIN
        SELECT COUNT(manager_id) INTO v_manager_count
            FROM employees WHERE employee_id = v_manager_id;
        IF v_manager_count = 0 THEN
            RAISE e_invalid_manager;
        END IF;
    END;
    DECLARE
        v_location_count NUMBER(2);
    BEGIN
        SELECT COUNT(location_id) INTO v_location_count
            FROM locations WHERE location_id = v_location_id;
        IF v_location_count = 0 THEN
            RAISE e_invalid_location;
        END IF;
    END;
    INSERT INTO departments
        (department_id, department_name, manager_id, location_id)
        VALUES
        (v_department_id, v_department_name, v_manager_id, v_location_id);
    DBMS_OUTPUT.PUT_LINE('New department created');
    EXCEPTION
    WHEN e_invalid_manager THEN
        DBMS_OUTPUT.PUT_LINE('Manager ID ' || v_manager_id || ' is invalid.');
    WHEN e_invalid_location THEN
        DBMS_OUTPUT.PUT_LINE('Location ID ' || v_location_id || ' is invalid.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Something went wrong');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```

### Version B

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_department_id departments.department_id%TYPE := 111;
    v_manager_id departments.manager_id%TYPE := 105;
    v_location_id departments.location_id%TYPE := 1500;
    e_invalid_manager EXCEPTION;
    e_invalid_location EXCEPTION;
    e_null_constraint_violation EXCEPTION;
    PRAGMA EXCEPTION_INIT(e_null_constraint_violation, -1400);
BEGIN
    DECLARE
        v_manager_count NUMBER(2);
    BEGIN
        SELECT COUNT(manager_id) INTO v_manager_count
            FROM employees WHERE employee_id = v_manager_id;
        IF v_manager_count = 0 THEN
            RAISE e_invalid_manager;
        END IF;
    END;
    DECLARE
        v_location_count NUMBER(2);
    BEGIN
        SELECT COUNT(location_id) INTO v_location_count
            FROM locations WHERE location_id = v_location_id;
        IF v_location_count = 0 THEN
            RAISE e_invalid_location;
        END IF;
    END;
    INSERT INTO departments
        (department_id, manager_id, location_id)
        VALUES
        (v_department_id, v_manager_id, v_location_id);
    DBMS_OUTPUT.PUT_LINE('New department created');
    EXCEPTION
    WHEN e_invalid_manager THEN
        DBMS_OUTPUT.PUT_LINE('Manager ID ' || v_manager_id || ' is invalid.');
    WHEN e_invalid_location THEN
        DBMS_OUTPUT.PUT_LINE('Location ID ' || v_location_id || ' is invalid.');
    WHEN e_null_constraint_violation THEN
        DBMS_OUTPUT.PUT_LINE('Cannot enter null value into column with NOT NULL constraint');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Something went wrong');
        DBMS_OUTPUT.PUT_LINE('Error Code: ' || SQLCODE);
        DBMS_OUTPUT.PUT_LINE('Error Message: ' || SQLERRM);
END;
```