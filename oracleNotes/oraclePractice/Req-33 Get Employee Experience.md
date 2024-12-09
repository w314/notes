# Req-33: View experience of an employee in the company

Develop a stored function sf_get_experience_employee 
- that accepts employee ID and 
- returns total years of experience. 
- In case of exception function returns -1.
- Hint: Return type must be Number (3,1) and consider 365 days per year for calculation.
- Invoke the function with employee ID as 100 and 116.


## Stored Function

```sql
CREATE OR REPLACE FUNCTION sf_get_experience_employee(
    p_employee_id employees.employee_id%TYPE)
    RETURN NUMBER
IS
    v_hire_date employees.hire_date%TYPE;
    v_experience NUMBER(3, 1);
    c_days_in_year CONSTANT NUMBER(3) := 365;
BEGIN
    SELECT hire_date INTO v_hire_date
        FROM employees WHERE employee_id = p_employee_id;
    v_experience := (SYSDATE - v_hire_date) / c_days_in_year;
    RETURN v_experience;
    EXCEPTION
    WHEN OTHERS THEN
        RETURN -1;
END;
```

## Invoke Stored Function

```sql
SET SERVEROUTPUT ON;

DECLARE
    v_employee_id employees.employee_id%TYPE := 108;
    v_experience NUMBER(3,1);
BEGIN
    v_experience := sf_get_experience_employee(v_employee_id);
    IF v_experience = -1 THEN
        DBMS_OUTPUT.PUT_LINE('Error');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Employee with id ' || v_employee_id ||
        ' has ' || v_experience || ' years experience.');
    END IF;
END;
```