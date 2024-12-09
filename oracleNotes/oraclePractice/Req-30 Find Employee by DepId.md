# Req-30: Find Employee ID based on Department ID
Develop a stored function 
- sf_get_emp_id_by_deptid 
- that accepts department id and 
- returns the employee ID working under that department. 
- In case of invalid department ID return -1, 
- more than one row is fetched return -2 and for 
- any other error return -3.
- invoke the function from anonymous block for department IDs 10, 20 and 25.

## Stored Function

```sql
CREATE OR REPLACE FUNCTION sf_employee_id(
    p_department_id employees.department_id%TYPE)
    RETURN NUMBER
IS
    v_employee_id employees.employee_id%TYPE;
BEGIN
    SELECT employee_id INTO v_employee_id
        FROM employees WHERE department_id = p_department_id;
    RETURN v_employee_id;
    EXCEPTION
    WHEN NO_DATA_FOUND THEN
        RETURN -1;
    WHEN TOO_MANY_ROWS THEN
        RETURN -2;
    WHEN OTHERS THEN
        RETURN -3;
END;
```

## Invoking stored functon

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_department_id employees.department_id%TYPE := 10;
    v_result employees.employee_id%TYPE;
BEGIN
    v_result := sf_employee_id(v_department_id);
    IF v_result >= 0 THEN
        DBMS_OUTPUT.PUT_LINE('Employee with id ' || v_result || ' works for department with id ' || v_department_id);
    ELSIF v_result = -1 THEN
        DBMS_OUTPUT.PUT_LINE('No employees for department with id ' || v_department_id);
    ELSIF v_result = -2 THEN
        DBMS_OUTPUT.PUT_LINE('More than 1 employee work for department with id ' || v_department_id);
    ELSIF v_result = -3 THEN
        DBMS_OUTPUT.PUT_LINE('Some error happened');
    END IF;
END;
``` 