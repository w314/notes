# Req-26 View Department Name

- Develop a stored function sf_get_dept_id that accepts department name and returns department ID. In case of any error return -1.

- Invoke the function from anonymous block for 'Finance' and 'Sales' department and display appropriate messages.

### Stored Function

```sql
CREATE OR REPLACE FUNCTION sf_get_dept_id(
    p_department_name departments.department_name%TYPE)
    RETURN NUMBER
IS
    v_department_id departments.department_id%TYPE;
BEGIN
    SELECT department_id INTO v_department_id
        FROM departments WHERE department_name = p_department_name;
    RETURN v_department_id;
    EXCEPTION
    WHEN OTHERS THEN
        RETURN -1;
END;
```

### Invoke Stored Function

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_department_name departments.department_name%TYPE := 'Finance';
    v_department_id departments.department_id%TYPE;
BEGIN
    v_department_id := sf_get_dept_id(v_department_name);
    IF v_department_id = -1 THEN
        DBMS_OUTPUT.PUT_LINE('Some Error Occured');
    ELSE
        DBMS_OUTPUT.PUT_LINE('The id of department ' || 
            v_department_name || ' is ' || v_department_id);
    END IF;
END;
```