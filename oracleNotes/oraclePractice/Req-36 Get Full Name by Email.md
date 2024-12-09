# Req-36: Get full name of employee based on email

Develop a stored function sf_get_emp_name_by_email 
- that accepts email and 
- returns full name (<first_name><space><last_name>) of the given employee. 
- In case of exception, function returns -1.
- invoke the function from anonymous block for employee email 'JPATEL' and 'S_KING'.

## Stored Function

```sql
CREATE OR REPLACE FUNCTION sf_get_name_byEmail(
    v_employee_email employees.email%TYPE)
    RETURN VARCHAR2
IS
    v_first_name employees.first_name%TYPE;
    v_last_name employees.last_name%TYPE;
BEGIN
    SELECT first_name, last_name INTO v_first_name, v_last_name
        FROM employees WHERE email = v_employee_email;
    RETURN v_first_name || ' ' || v_last_name;
    EXCEPTION
    WHEN OTHERS THEN
        RETURN '-1';
END;
```

## Invoke Stored Function

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_email employees.email%TYPE := 'JPATEL';
    v_name VARCHAR2(100);
BEGIN
    v_name := sf_get_name_byEmail(v_employee_email);
    IF v_name = '-1' THEN
        DBMS_OUTPUT.PUT_LINE('Error');
    ELSE 
        DBMS_OUTPUT.PUT_LINE(v_employee_email || ' - ' || v_name);
    END IF;
END;
```